# The observer gap: every prior round assumed one without naming it

**Status: OPEN — a meta-level finding, not another attacked hypothesis.**
Applies retroactively to every document in `research/`.

## Contributors

```text
Author:   Volodymyr
Role:     WSM project owner
Content:  "хто про це буде знати? нам потрібен спостерігач" -- the
          observer question, posed directly

Author:   Claude Sonnet 5 (Anthropic)
Role:     WSM Foundations Research collaborator
Content:  connecting it to the already-established external-witness
          discipline (wsm-os/probe/exit-boundary-probe.c) and to
          Gödel incompleteness as the internal-observer case
```

## What was missed

Every round in this research thread (`REPEAT`, `BRANCH`, `DISTINCTION`,
Path A/B, the top-down descent through logic) asked "does this
construction hold?" and someone — Claude, GPT-5.6 Sol, Volodymyr —
checked it. That checking was never itself named as part of what the
foundation needs to account for. Attack vector 4 on `DISTINCTION`
(`distinction-attacked.md`) — "does distinguishing require an
act, an observer?" — landed as a real hit at the time, but was treated
as one more cost specific to `DISTINCTION`. It was not: **every
candidate in every round implicitly relied on an observer to register
its success or failure, and none of them accounted for that reliance
as part of their own content.**

## This was already solved once, at the engineering layer, and forgotten here

`wsm-os/probe/exit-boundary-probe.c` already enforces exactly this
discipline: `RAW_CONTROL_REACHED` is confirmed over a raw serial
channel *external* to the code being witnessed, specifically because a
self-report from inside the crossing code would not be trustworthy —
the same observation-vs-self-report principle already standing
elsewhere in this ecosystem. This philosophical thread reinvented the
same question from scratch, several rounds in, instead of carrying the
discipline over from the sibling `wsm-os` work directly.

## Two different observer questions, not to be conflated

**External observer** (legitimate, and what has actually been
happening this whole time): Claude, GPT-5.6 Sol, and Volodymyr checking
each construction from outside — the same role QEMU or a proof
assistant plays when investigating `wsm-os`'s hardware claims without
becoming part of WSM's own semantics
(`research/hypothesis-a-repetition.md`'s "external mathematics as
research tool" section already named this pattern for math; it applies
identically here). This is fine, and does not need to be smuggled in —
it should simply be named honestly as what has been doing the checking
all along.

**Internal observer** (WSM verifying its own foundational claims,
without an external check): a genuinely harder problem, not yet
touched by anything in this thread. A system attempting to verify its
own consistency or the truth of its own claims from entirely within
itself runs into real, well-established limits — Gödel's incompleteness
theorems, named here as a real body of existing work this direction
would run into, not as content to import into WSM. If WSM is ever meant
to know `2 + 2 = 4` as *its own* verified fact, rather than as
something reported to it from outside, this is the actual territory
that question enters, and it has known hard limits already studied for
a century.

## What this changes

Not a verdict on any prior candidate — `REPEAT`, `BRANCH`,
`DISTINCTION`, and the top-down logic floor all stand as previously
found. What changes is the bookkeeping: the `GIVEN` / `DERIVED` /
`INTRODUCED` provenance triplet (`provenance-foundation.md`) needs a
fourth, previously silent role made explicit — **`OBSERVED-BY`** — who
or what checked that a `DERIVED` step actually holds, and whether that
checker is external (a research tool, legitimate) or is being asked to
be WSM itself (which raises the internal-observer problem above and
has not been attempted anywhere in this thread yet).
