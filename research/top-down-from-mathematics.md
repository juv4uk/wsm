# Top-down: strip existing mathematics toward (), see where it stops

**Status: OPEN.** A third methodological direction, alongside the
bottom-up attempts (`hypothesis-a-repetition.md`,
`distinction-attacked.md`) and the observation-grounded attempt
(`physical-constants-as-given.md`).

## Contributors

```text
Author:   Volodymyr
Role:     WSM project owner
Content:  the originating question -- "if we can't reach mathematics
          from (), can we descend from mathematics toward ()?"

Author:   Claude Sonnet 5 (Anthropic)
Role:     WSM Foundations Research collaborator
Content:  identifying first-order logic's own primitives as the floor
          this direction reaches, and the propositional-logic /
          single-truth-value observation
```

## The move

Every bottom-up attempt (`REPEAT`, `BRANCH`, `DISTINCTION`,
`this/not-this`) tried to *construct* something beyond `()` and kept
breaking on hidden imports. The reverse direction: start from
already-established mathematics (Peano arithmetic, ZFC, any known
formal system) and strip it down — remove everything that isn't
strictly necessary — and see what floor it bottoms out on. This is not
a new invention; it has real precedent (not claimed as identical, only
as a relevant precedent to be aware of, not smuggled in as WSM
content): Frege/Russell's logicist reduction of arithmetic to logic,
and the actual field of *reverse mathematics* (Friedman, Simpson),
which classifies theorems by the weakest subsystem sufficient to prove
them — the same "descend to the minimum" instinct, already studied.

## What the descent actually hits

Virtually all classical mathematics (PA, ZFC, type theory) is built on
top of **first-order logic**, and first-order logic does not derive its
own primitives from anything more basic — it takes them as given,
undefined within the system:

```text
domain of discourse   -- a set of "things" to talk about -- PLURALITY
equality (=)           -- IDENTITY / comparison
negation (¬)            -- the same negation that broke this/not-this
quantifiers (∀, ∃)      -- "there exists" presupposes a domain with
                           more than one possible element -- plurality again
```

**This is not an approximate analogy — it is the identical cluster**
that independently broke `REPEAT`, `BRANCH`, `DISTINCTION`, and
`this/not-this` from the bottom-up direction: plurality, identity,
negation. Formal logic does not derive these from something smaller —
it takes them as primitive, exactly the way our attempts kept needing
to.

## Why this matters even though it doesn't cross the wall

Bottom-up and top-down are independent methods. Both landing on the
same floor — plurality/distinction, identity, negation — is a form of
convergent confirmation stronger than anything produced by either
direction alone: it suggests this is genuinely where mathematics'
actual floor is, not an artifact of which specific hypotheses got
attacked from below. It does not give a way past the wall. It gives
much higher confidence the wall is real and precisely located.

## A sharper boundary: propositional logic and the single-truth-value case

Propositional logic (no domain, no quantifiers — just atoms and
connectives) still requires *at minimum two* truth values (true/false)
to be non-trivial — this is already plurality in its most minimal form.
A system with **exactly one** truth value, where everything is
automatically "so" and nothing can be otherwise, has no negation worth
having (¬true would have nowhere to go) and no distinction possible at
all. That single-value system looks like a plausible formal
description of `()` alone, with nothing added. **The moment a second
truth value becomes necessary is the same transition every other
direction of this research has been circling** — now visible from
mathematics' own side, not only from `()`'s side.

## What remains open

This direction confirms the location of the wall; it does not remove
it. The open question is unchanged in kind from the bottom-up work:
is there any way to introduce a second distinguishable state without
already presupposing plurality/distinction to state that a second
state exists at all? Nothing here answers that — it only shows the
question is the same question, reached from the opposite direction,
independently.
