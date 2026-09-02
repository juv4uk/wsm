# Three relations formalized: requires / equivalent / co-primitive

**Status: OPEN.** Follows `distinction-attacked.md`'s cycle finding.

## Contributors

```text
Author:   GPT-5.6 Sol (OpenAI), relayed by Volodymyr
Role:     WSM Foundations Research collaborator
Content:  the "not a new candidate, formalize three relations" move,
          the CLOSURE/SUFFICIENCY/IRREDUCIBILITY tests for a joint
          basis, the observation that a cycle may signal bedrock
          rather than error

Author:   Claude Sonnet 5 (Anthropic)
Role:     WSM Foundations Research collaborator
Content:  the definitional test distinguishing the three relations,
          applying it to distinction/plurality, the CLOSURE caveat
```

Per GPT-5.6 Sol's own next move — not a new candidate, but a formal
distinction between three things that were being conflated.

## The three relations

**1. `A requires B` (asymmetric dependency).** Already in use: `A ⪯ B`
holds if there is an explicit construction of `B`'s structure from `A`
alone, introducing no new independent primitive. Asymmetric when the
reverse construction does not exist.

**2. `A ~ B` (equivalent in strength, but still two things).** `A ⪯ B`
and `B ⪯ A` both hold, **and `A` and `B` remain two independently
statable primitives** — each has a definition that does not reference
the other, even though each turns out to be derivable from the other.
Example from outside WSM, for illustration only, not as imported
content: NAND alone and `{AND, NOT}` together are equivalent in
expressive power, but they remain two genuinely different vocabularies
— either could be written down without the other.

**3. Co-primitive (two names for one irreducible joint introduction).**
Formally distinguished from case 2 by a definitional test, not a
derivational one:

> Can `A`'s bare definition be written without already containing `B`'s
> content — even setting aside what could later be *derived* from `A`?

If the answer is no in **both** directions simultaneously, `A` and `B`
are not two equivalent-strength primitives — they are one primitive,
artificially split into two names. This is a stronger and different
claim than case 2: case 2 is about derivational power; case 3 is about
whether independent *definition* is even possible at all.

## Applying the test to distinction / plurality

- Attempted to define `distinction` without presupposing `plurality`:
  fails. `distinction-attacked.md`'s own vector 1 already showed this
  — for distinction to mean anything, at least something and some
  *other* thing must be presupposed, which is already plurality.
- Attempted to define `plurality` without presupposing
  distinguishability: also fails. "Many undifferentiated things"
  collapses into "one thing" without some way to tell instances apart
  — the same discreteness problem `() ()` had back in the very first
  `REPEAT` round (`hypothesis-a-repetition.md`).

**Both definitional directions fail independently.** This is case 3,
not case 2: `distinction` and `plurality` are not two
equivalent-strength primitives — they are one joint introduction, named
twice.

## Honest caveat: the joint basis is not yet closed

Confirming co-primitivity does **not** mean `A* = {distinction,
plurality}` has passed all three tests GPT-5.6 Sol set for a minimal
joint basis:

```text
SUFFICIENCY    -- claimed, not yet actually constructed/shown
CLOSURE        -- FAILS as currently stated: vector 4 from the
                  DISTINCTION attack (observer/action -- is
                  distinguishing an act, not a static fact?) was never
                  resolved. If distinguishing requires an act, process/
                  time leaks in -- the same unhealed wound shared by
                  REPEAT and BRANCH from the very first rounds.
IRREDUCIBILITY -- follows fairly directly from co-primitivity itself
                  (removing either name removes the one joint concept
                  both name), but this is not yet independently checked.
```

**So the honest status is**: `{distinction, plurality}` is very likely
one co-primitive unit, not two — but that unit, as currently stated,
may not yet be self-contained. A third element (something like
process/observer) may need to join it before `A*` actually closes. The
next real question is not "is the cycle real" (answered: yes, by the
definitional test above) but **whether closure requires growing `A*`
to include a process/observer component, and whether that component is
itself further reducible or genuinely irreducible alongside
distinction/plurality.**
