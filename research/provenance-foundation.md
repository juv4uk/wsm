# The research question, reframed: provenance, not derivation

**Status: OPEN, a reframing not a conclusion.** Follows
`hypothesis-a-repetition.md` (both `REPEAT` and `BRANCH` attacked and
broken). This document records a structural result the owner reached
by pushing the attack one level further — not a fourth hypothesis to
attack, but a change in what kind of question is even being asked.

## The structural result

Any step `() -> X` where `X` carries content beyond bare presence must
import something `()` does not contain: an operation, a relation, a
distinction, a rule, an observer, a transition. `()` has no
description by the project's own founding axiom ("`()` не визначаємо.
Ми лише не дозволяємо машині його втратити.") — so nothing can be
validly derived from it alone. This is not a failure of ingenuity. It
is structural, close to *ex nihilo nihil fit*: a thing defined as
having no content cannot, by derivation alone, produce content.

The owner's own reframing of the honest form of any real step:

```text
()
+
A
|
v
X
```

where `A` is the **first explicitly introduced assumption** — never
hidden, never smuggled. The research question changes from "how do we
get mathematics out of `()` with nothing extra" (now known to be
impossible) to:

> **Яка найменша передумова, яку ми готові внести відкрито, після якої
> математика стає можливою?** (What is the smallest assumption we are
> willing to introduce openly, after which mathematics becomes
> possible?)

## `t` reframed: provenance, not absolute truth

```text
2 + 2 = 4
    |
    v
    t
```

becomes, conceptually (not literal syntax):

```text
A
|
...
|
2 + 2 = 4
|
t[A]
```

`t` is not claimed as absolute metaphysical truth, and not weakened
into probability or "possibly so." It is **formal truth with known
provenance** — true *within the explicitly built system of
assumptions*, with the dependency chain back to `A` never discarded.
`2 + 2 = 4` would carry its own lineage (`depends on addition, which
depends on ..., which ultimately depends on A`), inspectable, not
asserted as free-floating fact.

**This is the same epistemology this whole project already runs on,
applied one level deeper.** `STATIC-CONFIRMED` / `LIVE-CONFIRMED` /
`predicted` labeling, and the standing rule that a claim's evidence
must never be discarded once it's been used, already govern how this
project investigates the machine (`hardware/`, `probe/` in the sibling
`wsm-os` repo). The provenance-boundary proposal is not a new invention
— it is the same discipline promoted from "how we know things about
WSM" to "how WSM will know things about itself."

## What this changes about the standing four criteria

Criterion 2 ("not stolen from ready-made mathematics") cannot mean "no
external content at all" anymore — that is now known to be impossible
for any nontrivial step. It must mean something sharper: **`A` is
allowed mathematical content, but that content must be shown to be the
smallest sufficient amount, not merely convenient, and its origin must
never be hidden.**

## A candidate for the smallest explicit `A`: distinction

Looking at the dependency closures of the two broken hypotheses side by
side:

```text
REPEAT:        individuation, sequence, termination
BRANCH:         distinction, plurality, modality
this/not-this: distinction, identity, negation
```

**`distinction` is the one thing common to all three.** Not sequence,
not plurality, not negation alone — every broken candidate quietly
needed *some* notion that things can be told apart before it needed
anything else. This suggests a candidate for `A` narrower than any of
the three original hypotheses: not "this/not-this" (which already
bundles identity and negation on top), just the bare, not-yet-decomposed
**possibility of distinction itself** — no claim about how many things
are distinguished, no negation, no identity relation asserted, only
that telling-apart is possible at all.

**Not committed.** Whether "distinction" is itself atomic or further
decomposable is exactly what the next round of attack should test.

## The open measurement question

"Smallest assumption" is not yet a criterion with teeth. Without a way
to actually measure the size of `A` — by its dependency-closure size,
by some other principled metric — "smallest" collapses into aesthetic
judgment. This is the sharpest open question left standing: **how is
the size of a foundational assumption actually measured**, so that
comparing candidate `A`s is a real research procedure and not a taste
contest.
