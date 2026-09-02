# DISTINCTION attacked; a possible circularity with plurality found

**Status: OPEN.** Follows `provenance-foundation.md`. Records: a
correction to that document's own phrasing, a methodology upgrade
(partial order over a scalar "size"), the requested attack on
`DISTINCTION`, and its result.

## Correction to the structural claim

`provenance-foundation.md` stated the negative result as "`()` has no
description... so nothing can be validly derived from it alone" — this
implicitly attributes a property ("contains no rules") *to* `()`,
which the project's own axiom forbids (`()` is not defined, not even
by negation). The owner's sharper, corrected formulation, which
supersedes the earlier phrasing:

```text
given: ()
and nothing else introduced
------------------------------
no justified nontrivial transition
```

This is a claim about the construction system, not about `()`'s
nature. Any honest step is `() + A -> X`, where `A` is the first
explicitly introduced assumption.

## Methodology upgrade: partial order, not scalar size

Counting a candidate's dependency-closure size (e.g. "REPEAT needs 3
things, BRANCH needs 3 things") is misleading — one concept can be
strictly stronger than three others combined. Replaced with a partial
order: `A ⪯ B` holds if `B`'s full foundational structure can be
constructed from `A` alone, introducing no new independent primitive.
If `A ⪯ B` and `B ⋠ A`, `A` is strictly weaker. If both hold, they are
equally fundamental, just different presentations. This is checkable,
not aesthetic — proving `A ⪯ B` is real derivation work, and doing that
work will itself likely require external mathematics as a research
tool (see below), not something WSM has to internalize.

Dependency closures (`REPEAT: individuation, sequence, termination`;
`BRANCH: distinction, plurality, modality`) are demoted from "measure"
to **diagnostic**: they say what to attack next, not how big a
candidate "is" — because those listed dependencies may themselves
decompose further, changing the closure.

## The attack on DISTINCTION

Formulated deliberately without smuggling content: not "this ≠ that"
(already has `this`, `that`, `≠`), not "A / not-A" (already has
negation), not "two different things" (already has number) — just the
working name `DISTINCTION` and the question "what minimally must be
introduced so that everything does not collapse into one
undifferentiated state?"

Four attack vectors, all posed by the owner, executed here:

1. **Relata — does it presuppose "what is distinguished"?** Yes, and
   this lands hardest. For distinction to mean anything, at least
   something and some *other* thing must be presupposed — which is
   already a form of plurality, the exact thing that broke `BRANCH`.
   `DISTINCTION` does not avoid plurality; it requires it directly to
   be coherent at all.
2. **Boundary — does it presuppose where the split occurs?** Weaker
   hit — a purely relational, non-spatial distinction seems at least
   conceivable without importing topology.
3. **Identity — does something have to remain itself while being
   distinguished?** Yes — the same individuation problem that broke
   `REPEAT`.
4. **Observer/action — does distinguishing require an act, not just a
   static fact?** If distinction is an act rather than a standing
   state, it imports process — the same unresolved sequence/time wound
   already shared by `REPEAT` and `BRANCH`.

**Verdict: three of four attacks land.** `DISTINCTION` does not
survive as a clean, atomic primitive in this formulation — vector 1
(relata/plurality) is close to fatal on its own.

## A possible circularity, not just another death

If `DISTINCTION` requires plurality (vector 1), and `BRANCH` also
required plurality directly, the lattice drawn earlier
(`() -> DISTINCTION -> {REPEAT, BRANCH}`) may not actually be a clean
partial order at all. Plurality arguably needs *some* notion of
distinguishability to mean "many" rather than one undifferentiated
blob — and distinction arguably needs plurality to have anything to
distinguish. If both readings hold, `DISTINCTION` and `PLURALITY` are
not one derived from the other but **mutually presupposing** — a cycle,
not a rung on a ladder. This is the actual finding of this round, more
than "a fourth candidate died": the lattice model itself may need to
admit cycles, not just a strict order.

## Adopted vocabulary going forward

**Provenance triplet** for any claim in this line of research:

```text
GIVEN       -- () itself
INTRODUCED  -- an assumption brought in explicitly (e.g. a candidate A)
DERIVED     -- constructed from GIVEN + INTRODUCED, with the derivation shown
```

**Minimality status ladder**, none of which may be overstated as the
next rung up without the work to back it:

```text
candidate
  -> sufficient                    (A -> M is shown to work)
  -> locally minimal               (no known strictly weaker A' suffices for M)
  -> minimal among known candidates
  -> proven minimal                (very strong claim: provably no weaker A exists at all)
```

"We don't know a weaker candidate" is not the same claim as "no weaker
candidate exists," and the two must never be conflated — proving global
non-existence of a weaker foundation may be extremely hard or
impossible, and claiming it prematurely would itself be the same
overclaiming discipline already enforced everywhere else in this
project.

## External mathematics as a research tool, not as WSM's content

A distinction worth keeping explicit, drawn directly from the
`wsm`/`wsm-os` split already in place: the mathematics, logic, proof
assistants, or dependency graphs *used to investigate* WSM's own
foundation are not thereby smuggled *into* WSM's semantics — the same
way QEMU helps investigate a machine without QEMU becoming part of that
machine's own meaning. Actually proving `A ⪯ B` relations, or that a
candidate `A` is a genuine milestone (sufficiency) versus that no known
weaker candidate works (minimality), will likely require exactly this
kind of external tooling, and that is legitimate — the same
observation-versus-self-report and STATIC/LIVE/predicted discipline
that governs hardware claims in `wsm-os` applies here too.

## Next, narrow question

Does `PLURALITY` decompose independently of `DISTINCTION`, or are they
genuinely co-primitive (each requires the other, neither reducible to
anything simpler alone)? If genuinely co-primitive, the honest next
move may be to stop looking for a single atomic `A` and instead treat
the *pair* `{DISTINCTION, PLURALITY}` as one candidate foundational
unit, and attack *that* as a whole.
