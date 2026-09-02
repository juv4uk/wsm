# Grounding in real physical constants, not pure logical construction

**Status: OPEN, unattacked past the first pass below.** A new
direction: instead of trying to logically *derive* distinction/
plurality from nothing (repeatedly breaking into circularity, see
`three-relations-formalized.md`), can some part of the foundation be
grounded as an **observed physical fact** about the real machine,
rather than a constructed logical primitive?

## Contributors

```text
Author:   Volodymyr
Role:     WSM project owner
Content:  the originating question -- "can we reach mathematics
          through really-existing constants?"

Author:   GPT-5.6 Sol (OpenAI), relayed by Volodymyr
Role:     WSM Foundations Research collaborator
Content:  elaborating into Path A vs Path B, the dimensional/
          dimensionless-constant distinction, the invariant-before-
          number refinement, the comparator/threshold follow-up

Author:   Claude Sonnet 5 (Anthropic)
Role:     WSM Foundations Research collaborator
Content:  the hardware-import tension, the attacks on both rounds
```

## The appeal

`()` itself is not derived — it is `GIVEN`. Everything attempted so far
(`REPEAT`, `BRANCH`, `DISTINCTION`) tried to *logically construct* a
next step, and each construction imported hidden content. What if part
of the foundation does not need construction at all, because it is
already physically true of the substrate `wsm-os` has already proven
reachable and observable — the same `LIVE-CONFIRMED` status already
used for hardware claims (e.g. `handoff-probe.c` reading 121 real
memory descriptors — a real machine really does have more than one
addressable location, checked, not assumed)?

## The immediate tension this creates

This appears to collide directly with the standing two-way discipline
(`wsm-os/README.md`, `research/handoff-state.md`): **"wsm не імпортує
апаратні поняття як семантику лише тому, що x86 їх має."** Doesn't "the
machine physically has multiple cells, therefore WSM has plurality"
commit exactly the sin the earlier rule forbids — the same shape as
"x86 has ADD, therefore WSM has +"?

## A candidate way to draw the line, not yet validated

A proposed distinction between two different things that could both be
called "grounding in hardware":

- **Forbidden**: importing a ready-made hardware *operation* (e.g.
  `ADD`) as WSM semantics without independently justifying why WSM
  needs it.
- **Possibly legitimate**: treating a physical *fact about the
  substrate itself* (e.g. "this machine is not a single point — more
  than one distinguishable state physically exists") as `GIVEN` by
  observation, the same epistemic status `()`'s own presence already
  has — not derived, not constructed, simply checked and reported with
  the same `LIVE-CONFIRMED` discipline `wsm-os` already uses.

If this distinction holds, it does not solve the distinction/plurality
circularity directly — it changes what kind of answer is acceptable
for part of the foundation: not every element needs a derivation chain
back to `()`; some may be legitimately grounded in direct observation
instead, same as `()` itself is.

## The attack this has already received, not resolved

**Reporting** a physical fact as "there is more than one X" already
requires the observer to hold *some* notion of "more than one" before
observation even begins. Grounding plurality in hardware observation
does not obviously escape the same recursive problem
`distinction-attacked.md` found for the purely logical route — it may
just relocate the smuggling from "constructed from logic" to "presupposed
by the act of observing," which is not obviously an improvement.

## What actually needs settling next

1. Is there a way to state "this substrate is not a single point"
   without the observer already presupposing plurality to say it? (If
   not, this direction inherits the same circularity as
   `distinction-attacked.md`, just one level removed.)
2. If some foundational elements are allowed to be `GIVEN-by-observation`
   rather than `DERIVED`, what stops that category from becoming an
   escape hatch for smuggling in anything convenient, defeating the
   whole minimality discipline built up over the last several rounds?
   A criterion is needed for what counts as a legitimate physical
   `GIVEN` versus a disguised import — not yet proposed here.

Not committed either way. Recorded because the tension with the
two-way discipline is real and needs to be resolved explicitly, not
quietly ignored in either direction.

## Round 2: Path A vs Path B, and why B is not cheaper than A

GPT-5.6 Sol refined the direction into a named alternative path:

```text
PATH A: () -> explicit assumptions -> mathematics
PATH B: () -> contact with reality -> invariant -> mathematics
```

Path B, spelled out: `() -> OBSERVATION -> INVARIANT -> RELATION ->
QUANTITY -> MATHEMATICS`. He drew a real, useful distinction inside it:
dimensional constants (`c = 299792458 m/s`) are bad as a foundation
because they already depend on a chosen unit system — a hidden import.
Dimensionless constants or bare *ratios* are more interesting.
Cleanest of all: don't start from a numeric constant at all — start
from a repeated real experiment (a real circle, a real pendulum)
yielding the *same structural result* across repetitions, and only
later build the concept of ratio, then number, from that. GPT-5.6 Sol
posed its own sharp question against it before any defense: "що
мінімально потрібно WSM, щоб узагалі здійснити observation, не
вкравши вже distinction, identity, time і comparison?"

**Claude's attack, using GPT-5.6 Sol's own wording against its own proposal**:
"той самий структурний результат" already uses identity (`the same`)
— the exact problem that broke `REPEAT`. "Повторено" already imports
sequence/time — the unhealed wound shared by `REPEAT` and `BRANCH`.
"Стабільне відношення" requires *comparing* measurement A against
measurement B and judging them equal — this is `eq`/comparison, the
very first thing rejected back in the original `first-step-candidate.md`
round for being a direct import from Lisp/logic, before `REPEAT` or
`BRANCH` were even proposed.

**Path B is not a cheaper alternative to Path A — it is a strict
superset of Path A's already-broken requirements (distinction,
identity, time), plus comparison on top, which nothing before Path B
needed to add.**

**The obvious rescue, and why it fails**: let some external apparatus
(the observing machine, `wsm-os`) do the observing, and have WSM merely
*receive* the finished invariant. GPT-5.6 Sol's own proposal already
forbade exactly this ("не можна взяти готове число як старт — це буде
контрабанда") — if an external process already performed
distinction+identity+time+comparison and hands WSM only the result,
that is the identical contraband, wearing "observation" instead of
"axiom" as its label.

**Answered with GPT-5.6 Sol's own partial-order methodology**
(`three-relations-formalized.md`): since Path B's requirements are a
superset of Path A's, `Path A ⪯ Path B` and not the reverse — Path A is
no worse, and appears strictly better, under the minimality criterion
already established.

**One lead deliberately left open, not resolved**: could "comparison"
be reduced to a raw *physical* match (e.g. two voltage levels agreeing
within tolerance) rather than full logical `eq` — pre-semantic, prior
to any logic? This does not rescue Path B as stated, but it is the one
place worth attacking next, not yet attempted here.
