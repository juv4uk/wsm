# Can the machine discover its own constants without an external observer?

**Status: OPEN — real physics, real structural trap, not resolved.**

## Contributors

```text
Author:   Volodymyr
Role:     WSM project owner
Content:  the proposal -- an experiment without an external observer,
          the machine discovering real-world constants through its own
          hardware, citing semiconductor shot-noise research

Author:   Claude Sonnet 5 (Anthropic)
Role:     WSM Foundations Research collaborator
Content:  verifying the physics claim, the elementary-charge/Euler's-e
          notation trap, the structural attack on "no observer needed"
```

## The proposal

Rather than relying on trust in a designated external observer (Round
7's unresolved honesty problem), have the system itself discover real
physical constants through its own hardware's capabilities — an
experiment requiring no external observer at all. Cited candidate: a
scientific claim that weak current in semiconductors reflects Euler's
number `e`.

## The physics, checked, not assumed

Real and well-established: semiconductor **shot noise** (Schottky,
1918) — current fluctuations from the discreteness of electron charge —
genuinely follows **Poisson statistics**.

**A real notation trap found while checking**: the classic shot-noise
power spectral density formula, `S = 2eI`, uses `e` for the
**elementary electric charge** (≈1.6×10⁻¹⁹ C) — **not Euler's number**
(≈2.71828). These are different objects sharing one symbol in physics
notation, and conflating them here would be the exact category error
this project already caught once (`Tag::True` — mistaking a
representation for the semantic content it happens to share a name
with).

**The genuine connection, more indirect than "current reflects e"**:
the Poisson distribution's own formula, `P(k) = λᵏe^(−λ)/k!`, does
contain Euler's number, as the base of its exponential term. Shot
noise's event statistics take this form. So there is a real link — but
seeing it requires collecting many measurements, building a
distribution, and recognizing that distribution as Poissonian, not
reading `e` directly off a current trace.

## The structural attack: does this escape the observer requirement, or hide it?

If WSM's own hardware both *generates* the noise data and *concludes*
"this is Poissonian, therefore `e` is present here," that is
self-verification wearing a physics costume — the same Round 1 illusion
trap (`the-observer-gap.md`), not an escape from it. Being about real
physical noise rather than pure logical self-reference does not change
the structural fact: the checker and the checked are the same system.

## Where this actually fits in the architecture already built

Not a bypass of `SINGULAR EXTERNAL` — a input to `PLURAL INTERNAL`:

```text
hardware noise / real measurement  -> PLURAL INTERNAL (raw candidate data)
"this is Poissonian, e is present" -> still requires SINGULAR EXTERNAL
                                        confirmation, same as any other claim
```

Measuring real hardware phenomena is a genuinely valuable source of
*candidates* — arguably a richer one than pure internal disagreement
(Round 4), since it is grounded in real physics rather than only
argument. It does not remove the need for external confirmation that
the interpretation of the measurement is correct. `wsm-os`'s own probe
work (`handoff-probe.c`, `exit-boundary-probe.c`) already follows this
exact discipline for hardware state generally — real measurements,
always labeled by what confirmed them, never self-trusted.

## Update: a real probe was built and run, not left as talk

Per the owner's direct instruction to stop discussing and start
researching, `wsm-os/probe/entropy-source-probe.c` was built and run
for real — `RDSEED`/`RDRAND`, the concrete, testable version of this
idea (real Intel hardware entropy instructions, confirmed present on
the owner's own CPU). Full results in `wsm-os/probe/ENTROPY-RESULTS.md`.

Real finding, not a null result: under this lab's QEMU/TCG setup, 256
RDSEED calls succeeded with **zero** retries — real Intel silicon
documents occasional RDSEED failure as expected entropy-exhaustion
behavior, so zero failures strongly suggests TCG emulates RDSEED via
the host OS's random source rather than modeling real hardware entropy
behavior under load. **The specific retries-look-Poisson test this
document originally proposed is not currently testable in this QEMU/TCG
lab** — it needs real physical hardware, or a QEMU configuration that
actually models entropy exhaustion, neither attempted yet. This is a
structural limit of the current lab setup, found empirically rather
than assumed, not a dead end for the underlying idea.

## Not resolved

Whether physical hardware execution (separate, owner-authorized future
work) would show real RDSEED retry behavior worth statistically
analyzing for a Poisson/geometric shape, and whether shot-noise or
another hardware-native phenomenon is worth pursuing as a
physically-grounded `PLURAL INTERNAL` source more generally — separate,
in either case, from whether it could ever replace `SINGULAR EXTERNAL`
(it cannot, per the attack above).

## Sources

- [Wikipedia: Shot noise](https://en.wikipedia.org/wiki/Shot_noise)
- [UC Davis: Shot Noise -- History and Background](https://123.physics.ucdavis.edu/shot_files/ShotNoise.pdf)
- [arXiv: Shot Noise in Mesoscopic Conductors](https://arxiv.org/pdf/cond-mat/9910158)
