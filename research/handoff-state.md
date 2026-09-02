# The handoff state — what limits WSM, not how we found it

Firmware/BIOS/UEFI research only matters to WSM insofar as it answers
what state the hardware is in the moment control passes to WSM's own
code. All of that research — BIOS structure, the FIT table, real
microcode revisions, QEMU/OVMF/clang/gnu-efi tooling, the actual probe
code that crossed `ExitBootServices()` — lives in the sibling `wsm-os`
repository (`wsm-os/hardware/bios-f22e/`, `wsm-os/probe/`,
`wsm-os/docs/POWER-ON-SEQUENCE.md`), not here. This file keeps only the
conclusions that actually constrain `wsm`'s own design — not the
evidence, tooling, or narrative that produced them (own correction,
2026-09-02: this file had started accumulating exactly that duplicated
technical detail, and stopped).

## What is settled

- WSM begins after the firmware handoff, not before it and not as part
  of it.
- That handoff is reachable, not just theorized — `wsm-os` has crossed
  it for real (`ExitBootServices()`, then zero UEFI calls, confirmed
  over an independent raw hardware channel).
- `readable != physically representative`. A successful read from a
  virtual/emulated environment is not evidence the value carries the
  same physical meaning a real machine would give it. Three separate
  realities exist — STATIC firmware image, LIVE/VIRTUAL machine,
  LIVE/PHYSICAL machine — and a fact established in one does not
  transfer to the others without separately checking there too.
- A tool's failure is not a property of the machine. A broken build
  pipeline can produce a symptom indistinguishable from a broken
  machine; only real bisection tells them apart.
- Machine state is not the same claim as observable state. What a
  probe can read depends on what channel and privilege level it has,
  not only on what the machine actually is.
- A concrete representation for `()` has not been chosen. Nothing in
  the boundary-crossing work encodes it, and nothing there is entitled
  to.

## The two-way discipline this implies

> `wsm-os` does not invent capabilities. It only tests capabilities
> already formulated in `wsm`.
>
> `wsm` does not import a hardware concept as semantics just because
> the machine happens to have one.

```text
wsm:      "we need operation X"
              |
              v
wsm-os:   "can it be realized, and at what cost"

NOT:
x86 has ADD
    |
    v
    => WSM has +
```

`wsm-os/README.md` carries the same rule and an explicit list of what
it is not to add ahead of a real semantic need from here (scheduler,
allocator, SMP/interrupt framework, driver model, filesystem, heap,
runtime, ABI). `asm/` in this repo stays empty on the same principle —
its first file should be forced by a real semantic statement, not
filled in for the sake of activity.

## The one open question

```text
Який найменший додатковий крок після () можна ввести так, щоб:

1. він не визначав ();
2. він не був украдений з готової математики;
3. він створював реальну нову можливість;
4. його можна було фізично реалізувати на машині?
```

Only when a real candidate for this exists does `wsm-os` wake back up
to check point 4 against real hardware. Nothing here answers points
1–3 in advance.
