# First step candidate: () → branch

**Status: ATTACKED, broken as stated.** Answers the standing open
question in `research/handoff-state.md` ("Який найменший додатковий
крок після `()`..."). Written by Claude (Sonnet 5) on request. The
owner turned the same rigor used against his own counter-proposal
(`hypothesis-a-repetition.md`) back onto this one: branch does not
avoid the number trap either (it relocates "how many repetitions" into
"how many alternatives" — "more than one possible continuation" already
uses "more than one"), and "possible" continuation additionally imports
modality, arguably a heavier import than arithmetic. See
`hypothesis-a-repetition.md` for the full exchange and the deeper,
still-unnamed third candidate it produced. `asm/` stays empty — nothing
here is materialized.

## Candidates considered and rejected first

- **Comparison/equality (`eq`)** — a direct import from logic/Lisp;
  equality is foundational to nearly all existing mathematics. Fails
  criterion 2 (not smuggled from ready-made math/logic).
- **Successor / counting (Peano-style "one more")** — literally the
  Peano axioms, taken ready-made. Fails criterion 2 more directly than
  `eq` does.
- **Pair / cons** — a concrete Lisp data structure, not something that
  *follows* from `()` itself; the same "manufactured primitive" trap
  already caught once this session (`Tag::True`).
- **Importing `lib/epistemic.my`'s vocabulary** (proposed/rejected,
  supports/contradicts) from the old `my-lisp` system — tempting
  because it already avoids Bool, but it is porting a finished answer
  from the old system, not a step that arises freshly from `()`.
- **A second, independent copy of `()` in another memory cell** —
  physically trivial, but empty as a *capability*: if WSM cannot ask
  "is `()` here or not," multiple copies are a hardware fact invisible
  to WSM's own semantics. Fails criterion 3 in substance, even though
  it looks like it satisfies criterion 4.

## The proposal

The first step is not a new value. It is **branch** — the capacity to
do one thing if something is `()`, and a *different, still completely
uninterpreted* thing if it is not.

```text
()
 |
 +-- if this is ()      -> path A
 +-- if this is not ()  -> path B  (NOT false, NOT 1, NOT error, NOT
                                     unknown-as-a-value -- no content
                                     assigned yet, only existence and
                                     difference from path A)
```

## Validation against the four criteria

1. **Does not define `()`.** `()` stays exactly `() = ()`; nothing new
   is said *about* `()` itself. What gets a name is the divergence, not
   `()`.
2. **Not stolen from ready-made mathematics.** Narrower than Lisp's
   `eq`: no general comparison of two arbitrary values, no Boolean
   result. It is exactly the one duty already assigned to the machine
   regarding `()` — "recognize it, distinguish it from non-`()`" —
   raised from a hardware-internal mechanism to something WSM's own
   semantics can refer to.
3. **Creates a real new capability.** Right now nothing can behave
   differently depending on anything. This is the first moment
   differing behavior becomes possible at all — branching itself, born
   before "true" or "false" exist as named values.
4. **Physically realizable on the boundary already opened.** This is
   literally a conditional jump (compare a tag, branch on
   equal/not-equal) — the single most primitive real operation in the
   ISA `wsm`/`wsm-os` already target. No new hardware capability is
   required.

## Honest open weakness, not hidden

Does "branch" itself already presuppose *sequence* — "what happens
next," time, process — pulling in something close to computability
theory before WSM has decided it wants that? This is not resolved here.
It is the actual weak point of this proposal, not a rhetorical
disclaimer.
