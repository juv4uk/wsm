# Grounding in real physical constants, not pure logical construction

**Status: OPEN, unattacked past the first pass below.** The owner's
own new direction: instead of trying to logically *derive*
distinction/plurality from nothing (repeatedly breaking into
circularity, see `three-relations-formalized.md`), can some part of
the foundation be grounded as an **observed physical fact** about the
real machine, rather than a constructed logical primitive?

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
