# The observer gap: every prior round assumed one without naming it

**Status: external-vs-internal question DECIDED (external, always);
what "external observation" concretely requires for WSM remains OPEN.**
A meta-level finding, not another attacked hypothesis — applies
retroactively to every document in `research/`.

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
without an external check): a genuinely harder problem. A system
attempting to verify its own consistency or the truth of its own
claims from entirely within itself runs into real, well-established
limits — Gödel's incompleteness theorems, named here as a real body of
existing work this direction would run into, not as content to import
into WSM.

## DECIDED: external, always

**Volodymyr's ruling, given directly**: external. His own reasoning,
verbatim: "бо інакше це буде пастка ілюзії" (because otherwise it would
be a trap of illusion). This is not a temporary simplification pending
a solution to the internal-verification problem — it is a deliberate
refusal to ever enter that territory. `t[A]` will never be true "for
itself, by itself" — it is witnessed from outside, always, by
construction.

This is not a new principle invented for this occasion. It is the same
standing discipline this whole ecosystem already applies to *code*
(the `testing-epistemic-status-builder-verifier-adversary` memory: an
agent may write tests, but must never be the sole authority on what
counts as correct — Builder and Verifier cannot be the same party
without collapsing the check) and to *hardware claims* (`wsm-os/probe`'s
external raw-serial witness for `RAW_CONTROL_REACHED`, never a
self-report from inside the crossing code). It is now adopted as WSM's
own foundational epistemology, not merely this project's research
methodology: a self-verifying system is definitionally unable to
distinguish being correct from merely being self-consistent, which is
exactly the illusion this rules out by never permitting it to arise.

## What this changes

Not a verdict on any prior candidate — `REPEAT`, `BRANCH`,
`DISTINCTION`, and the top-down logic floor all stand as previously
found. The `GIVEN` / `DERIVED` / `INTRODUCED` provenance triplet
(`provenance-foundation.md`) gains a fourth role, now a **standing
requirement, not merely a bookkeeping suggestion**: every `DERIVED`
step must carry an `OBSERVED-BY` that is external to WSM. A claim whose
only possible checker is WSM itself is not merely incomplete — it is
disqualified, by the ruling above, as the specific trap this decision
exists to close off.

## Round 2: is "external" enough, or does OBSERVED-BY need independence?

**Volodymyr's next proposal**: introduce "objects," not in the
programming sense, but in the sense of personhood — and call them
observers, or find a more fitting name.

**Claude's attack**: `PERSONHOOD` as stated is not lighter than
anything already found — it is heavier. For a "personal" observer to
be the *same* observer across checks, it needs identity-over-time (the
`REPEAT` wound). For it to tell itself apart from what it observes, it
needs distinction (the `DISTINCTION` wound). Add intentionality — a
subject that *does* something, not merely exists — and this enters
philosophy of mind, a territory with *less* formal consensus than first
order logic, not more. By the project's own partial-order methodology
(`three-relations-formalized.md`), `PERSONHOOD` sits above every prior
candidate's dependency closure, not below it — a "Path C" that is more
expensive, not a shortcut.

**What is likely real underneath the proposal, though not what was
named**: not personhood, but **genuine independence of judgment**.
"External" alone (the Round 1 ruling) is not sufficient — a mechanical
comparator is external too, and `physical-constants-as-given.md`
already showed a comparator just relocates semantics into transistors
rather than avoiding it. The sharper requirement `OBSERVED-BY` may
actually need: not merely *outside* the system, but **capable, in
principle, of disagreeing** — an independent basis for judgment, not a
passive echo of the system being checked. This is not abstract: it is
the exact reason this research thread itself works the way it does —
Claude and GPT-5.6 Sol attacking each other's proposals produces real
results specifically because they *can* disagree, not merely because
they are two different processes. The ecosystem already has this
principle recorded for verification generally (same-model forks give
role diversity, not independence; genuine cross-checking needs a
genuinely different model) — not yet carried into WSM's own foundation
until now.

**No name is adopted here.** "Observer," "personhood," and every other
candidate word in this thread that sounded right before being attacked
(`Boolean`, `branch`) turned out to carry hidden cost. This capability
— call it, for now, only `OBSERVED-BY-INDEPENDENT` until it survives
its own attack — stays unnamed on purpose.
