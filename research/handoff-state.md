# The handoff state

BIOS/firmware research does not matter to WSM for its own sake. It
matters only to the extent it answers one question:

> In what state is the hardware in the last moment before my code
> begins?

Three different levels of firmware research answer three different
questions, and they should not be conflated:

```text
1. STATIC IMAGE
   What physically sits in SPI flash?

2. BOOT BEHAVIOUR
   What does firmware actually do to the CPU?
   Modes, MSRs, memory map, APIC, microcode.

3. HANDOFF STATE
   What exact machine state exists at the moment
   control passes to WSM?
```

Level 1 was done first, on the owner's real F22e BIOS (Gigabyte
GA-H170-Gaming 3), and lives in the sibling `wsm-os` repository:
`wsm-os/hardware/bios-f22e/BINARY-ANALYSIS.md`. It is real, useful
provenance — a genuine Intel Flash Descriptor image, LZMA-compressed
UEFI firmware volumes, a directly embedded build string
(`BIOS Date: 03/09/2018 20:42:30`), board and NIC identity confirmed
from the binary itself, not a vendor page. It should not be discarded.
But it answers level 1, not level 3 — and level 3 is what WSM actually
needs. A month spent disassembling DXE drivers is still only level 1/2
work; a single small bare-metal probe reading real CPU/platform state
is level 3, and level 3 is worth more to WSM than exhaustive coverage
of level 1.

## A concrete demonstration that levels 1 and 3 really do diverge

**Update — now confirmed on both sides, not just the live side.** A
raw byte-pattern search for the embedded microcode blob (signature
`0x000506E3`) first found nothing, reported honestly as
`not-yet-verified`. The owner's own correction — prefer structural
lookup (the Firmware Interface Table) over raw scanning, and label
every claim `STATIC-CONFIRMED` / `LIVE-CONFIRMED` / `INFERRED` — led
directly to finding it: `wsm-os/hardware/bios-f22e/FIT-AND-STRUCTURE-ANALYSIS.md`
parses the real FIT table (found via the fixed pointer at flash-mapped
address `0xFFFFFFC0`) and locates three real Microcode Update entries,
one matching the owner's exact CPU: **revision `0xC2`, dated
2017-11-16** — independently cross-confirmed by a second tool finding
the same blob set inside a named `CPU_MICROCODE_FILE_GUID` FFS
container. The raw scan had failed only because the blob lives in a
different Firmware Volume than the one that pass had decompressed —
exactly the failure mode structural lookup avoids.

The live, currently-active microcode revision was read directly from
the real machine, separately:
Windows' own registry (`HKLM\HARDWARE\DESCRIPTION\System\CentralProcessor\0`,
`Update Revision`), populated by Windows itself from the real CPU at
boot, not a WSL2/Hyper-V virtualized view (WSL2's own `/proc/cpuinfo`
reports `microcode: 0xffffffff` — a sentinel meaning "not observable
through this virtualization boundary," confirmed empirically, not a
gap to work around with more tooling).

**Live-observed:** revision `0xD6` (214), CPU identifier
`Intel64 Family 6 Model 94 Stepping 3` — matching the CPUID signature
exactly.

**Cross-referenced against a real, dated, third-party record**
(Debian's own `intel-microcode` package changelog):

```text
sig 0x000506e3, pf_mask 0x36, 2019-10-03, rev 0x00d6, size 101376
```

Same signature, and a revision (`0xD6`) that is a real, different
number from the now-`STATIC-CONFIRMED` embedded revision (`0xC2`), on
top of a real date gap: `0xC2` dated 2017-11-16, `0xD6` independently
dated 2019-10-03 — almost two years later. `0xC2 != 0xD6` and
`2017-11-16 < 2019-10-03` together settle it: the live revision cannot
be what F22e itself loads at power-on. It is almost certainly a later,
OS-supplied override — most likely delivered through Windows Update's
own microcode-loading mechanism — layered on top of whatever F22e's
own image actually contains.

This is the level-1-vs-level-3 gap made fully concrete, both sides
directly read rather than one side inferred: the static image says
"embeds revision `0xC2`, built 2017-11-16"; the live machine says
"currently runs revision `0xD6`, independently dated 2019-10-03." Both
statements are now `STATIC-CONFIRMED`/`LIVE-CONFIRMED` respectively —
neither is guessed, and they genuinely disagree, because they are
answers to different questions. Only the second one describes what the
CPU is actually running right now.

One further honest limit, not yet closed: what was read is Windows'
*own* final view, after Windows' *own* microcode loader has already
run — one layer removed again from the true firmware-to-first-code
handoff state (before any OS has touched the CPU at all). Getting
*that* state requires something running before an OS's own microcode
override lands, closer to what a small bare-metal probe would see.

## What a WSM-bearing handoff state actually needs to record

Not BIOS archaeology. This list, read once, directly, at the true
handoff point:

```text
CPU mode       = ?
CR0            = ?
CR3            = ?
CR4            = ?
EFER           = ?
page tables    = ?
GDT            = ?
IDT            = ?
stack          = ?
RSP alignment  = ?
memory map     = ?
APIC           = ?
microcode rev  = ?
cores online   = ?
interrupts     = ?
framebuffer    = ?
ACPI tables    = ?
```

**Update — real, not sketched: a minimal UEFI probe now exists and
runs**, at `wsm-os/probe/handoff-probe.c` (built with clang/lld-link,
not gnu-efi's own toolchain — a real, documented compatibility bug was
found and worked around; see `wsm-os/probe/README.md` for the full
bisection). It reads most of the list above directly
(CR0/CR3/CR4/EFER/RSP+alignment/RFLAGS/GDTR/IDTR/CPUID/live-microcode-
revision/memory-map/ACPI-RSDP/SMBIOS/framebuffer) before
`ExitBootServices()`, and a real run is captured in that README.
**Scope, stated plainly: that run is `LIVE-CONFIRMED` for the QEMU/OVMF
virtual environment, not the owner's physical machine** — two concrete
divergences are already visible from the emulation boundary alone
(TCG's microcode-revision read is a stub value `0x1`, not a real
silicon reading; the reported CPUID signature is QEMU faithfully
echoing back the `-cpu Skylake-Client-v1` model it was told to
emulate, not independent confirmation). Running this probe on the real
i5-6400 is separate, owner-authorized future work — the tooling to do
it now exists; running it does not follow automatically. `cores
online` and `APIC` (beyond the single boot-strap-processor's initial
APIC ID) are not yet read — a real ACPI MADT walk would be needed for
those, not yet implemented.

## Two laws this pass earned

**`readable != physically representative`.** The live-microcode
reading of `0x1` under QEMU/TCG is a useful *negative* witness: the
probe genuinely read something real (no crash, no fault), but what it
read carries no claim to the same physical meaning a read on real
silicon would carry. A successful read is not, by itself, evidence the
value means what it would mean on the real machine — three separate
realities exist (STATIC firmware image, LIVE/VIRTUAL machine,
LIVE/PHYSICAL machine) and a fact established in one does not transfer
to the others without separately checking. The physical reading stays
`?`, deliberately, rather than filled in by assumption.

**A tool's failure is not a property of the machine.** The gnu-efi/GCC-16
incompatibility (see `wsm-os/probe/README.md`) looked exactly like "the
UEFI probe prints garbage" — a symptom easily misread as something
wrong with the machine, the disk, or the probe's own logic. Real
bisection (ruling out disk backend, ruling out a CPU fault via QEMU's
own exception log, ruling out probe-specific code via a bare
hello-world) showed it was none of those — a toolchain-version
mismatch. The same discipline that separated "the build pipeline
broke" from "the machine broke" here is the discipline the eventual
`() -> mathematics` work will need again.

## Step 10 — done: crossing ExitBootServices() for real

`wsm-os/probe/exit-boundary-probe.c` answers the follow-up question
directly: not more state-reading (MADT/APIC/SMP were explicitly
deferred), but proving control survives the one boundary that actually
matters. Real criterion, run twice from a clean rebuild both times:

```text
BEFORE_EXIT           <- UEFI ConOut, Boot Services still valid
ExitBootServices()    <- real call, stale-map-key retry loop, succeeded first attempt both runs
AFTER_EXIT             <- raw port I/O to the 16550 UART at 0x3F8 -- no UEFI API at all
WSM_0_REACHED           <- same raw channel, after `cli`, then halt
```

`()` itself is deliberately **not** encoded anywhere in that probe —
choosing its representation is real design work belonging here, in
`wsm`, not something to rush inside a wsm-os lab probe's halt loop just
because it needed something to do after crossing. What this step
proves is narrower and prior to that question: that a point of pure,
UEFI-independent control is reachable and externally provable at all.

**Architectural boundary, now stated where it actually lives**: the
whole UEFI bootstrap apparatus (gnu-efi headers, clang's COFF target,
OVMF, QEMU) stays in `wsm-os` — the laboratory. `wsm` should never need
to know any of that exists. Where `wsm`'s own machine would actually
begin is exactly the point right after `ExitBootServices()` succeeds —
not a file split to make today (a single boot flow cannot be split
across two repos at runtime), but the line future work here should
respect once something real gets built past this proof.

## A sketch, still not started past the boundary itself

```text
AMI/UEFI
   |
   | bootstrap only
   v
tiny loader
   |
   +-- records machine state
   +-- disables what WSM does not need
   +-- transfers control
           |
           v
         WSM-0
           |
           v
          ()
```

No Rust runtime. No libc. No heap. No Lisp. No Bool. No `Tag::True`.
Perhaps as little as:

```text
_start:
    ...
    mov <representation-of-()>, %rax
    ...
```

with an external probe (serial, debug port) confirming the machine
actually reached that state — an external witness, not a self-report,
per the same observation-vs-self-report discipline this whole
ecosystem already holds itself to elsewhere. **The external-witness
half of this is exactly what step 10 above already proved** (a raw
serial channel, external to and independent of the code being
witnessed, confirming `WSM_0_REACHED`); what remains not started is
everything upstream of that proof — an actual chosen `()`
representation, and `wsm`'s own code reaching it rather than a wsm-os
probe proving only that the reaching-and-confirming mechanism itself
works.

The rest of this sketch — an actual `wsm`-owned entry point, a chosen
`()` representation, WSM-0 itself — is not started. It is recorded here because it reframes
what BIOS research is *for*: not curiosity about AMI Aptio, but finding
the minimal boundary between the machine firmware hands us and the
machine WSM actually owns.

```text
BIOS analysis
      |
machine boundary
      |
WSM entry state
      |
      ()
```
