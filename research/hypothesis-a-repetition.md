# Hypothesis A: Mathematics from repetition — proposed, then attacked

**Status: HYPOTHESIS UNDER ATTACK, not accepted.** The owner's own
counter-proposal to `research/first-step-candidate.md` (branch), given
explicitly for critique, with his own sharpest question attached. This
document records the proposal, Claude's attack on it, and the
resulting synthesis — not a settled conclusion.

## The proposal, in the owner's own structure

```text
()
|
REPEAT
|
finite repetition
|
natural number
|
composition of quantities
|
arithmetic
|
2 + 2 = 4
|
t
```

Not: `() = 0` or `() = object` — no content is assigned to `()`
itself. Only one operation is admitted: `R(())` yields another
presence, `() -> () ()`. Numbers are proposed as *later names* for
these prior constructions (`1 ≔ ()`, `2 ≔ () ()`, ..., deliberately
using `≔` — "we later name this" — not `=`). `+` is proposed as literal
concatenation of constructions. `=` is proposed as *structural*
equivalence, distinct from physical/address identity — two
independently-built results at different memory addresses, same shape.

The owner's own sharpest question, stated before any defense was
offered: **"Чи можемо ми ввести 'повторення', не приховавши всередині
нього вже готові поняття тотожності, часу, порядку та числа?"** (Can
we introduce "repetition" without hiding inside it already-ready
concepts of identity, time, order, and number?) — with his own
explicit acceptance that "no" would be a good result, not a failure to
avoid.

## The attack

1. **Instance individuation smuggles in a weak form of identity.** The
   proposal carefully avoids claiming `()` differs from `()` — only
   that "the whole constructions differ." But for `() ()` to have any
   structure at all (rather than being one indistinct blob), the
   machine needs discreteness of parts — some way to say "this cell of
   presence ends, another begins." That discreteness is identity
   entering through a side door: not value-identity, but instance-
   individuation, which is still a form of the thing the proposal set
   out to avoid presupposing.
2. **"Then again" already imports sequence.** The word "потім" (then)
   in "потім знову присутнє" is not free. This is not a point in the
   repetition hypothesis's favor or against it specifically — it is
   the *same* open wound already flagged in `first-step-candidate.md`
   for the branch proposal ("does branch already presuppose
   sequence/time/process?"). Neither hypothesis has closed this; it is
   a shared vulnerability of both, not a discriminator between them.
3. **The number is already there, just unnamed.** Using `≔` instead of
   `=` for `1 ≔ ()`, `2 ≔ () ()`, etc. is an elegant move, but it does
   not escape the substance: iterated construction from the empty set
   is *structurally identical* to the von Neumann construction of the
   natural numbers (0=∅, 1={∅}, 2={∅,{∅}}, ...), just in unary rather
   than nested notation. A unary tally system is not "not yet
   mathematics, later given a name" — it is mathematics in a different
   notation. Renaming the structure does not un-import it.

## The synthesis: repeat may need branch, not replace it

The proposal's own diagram requires *finite* repetition. Finiteness
requires stopping somewhere — and the decision "repeat again, or stop"
is exactly a branch:

```text
REPEAT-to-finiteness = REPEAT + a decision ("again, or stop")
                                          |
                                          v
                                       BRANCH
```

Unbounded `REPEAT` alone does not produce finite numbers — it produces
an unbounded process. Finiteness only arrives because a branch decision
("enough") happens somewhere. If this holds, **repetition is not an
alternative to branch — it consumes branch as a prerequisite.** The
same applies to the proposal's own account of `=` (point 6): comparing
two constructions structurally requires traversal (a form of
repetition) and, at each step, a decision ("do they still match, have
we reached the end of both") — branch again.

**Working conclusion, itself not final:** the two hypotheses
(`first-step-candidate.md`'s branch, and this repetition hypothesis)
are not competitors at the same level. Branch looks more primitive;
repetition, at least in the finite form this proposal actually needs,
appears to be built from branch plus storage, not the reverse.

One thing this hypothesis contributes independently of its own
survival: **"physical identity != structural equivalence"** (two
results at different addresses, same shape) is a real, sharp insight,
and it is the exact same shape as the already-recorded
`readable != physically representative` principle
(`research/handoff-state.md`) applied one layer down — from "what a
probe reads" to "what a constructed value means regardless of where it
sits in memory." That observation survives even if the repetition
scheme as a whole does not.
