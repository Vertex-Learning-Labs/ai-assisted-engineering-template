---
name: task
description: Turn a requirement into a normalized problem statement and an ordered task list before any implementation starts. Use when a new requirement, feature request, defect report, or vague ask arrives and it is not yet clear what should be built — including when the requirement seems obvious, since obviousness is usually where unexamined assumptions hide.
---

# Requirement understanding and decomposition

Covers brief requirements 1 (understanding), 2 (decomposition), and 3 (codebase reasoning).

Nothing gets implemented from this skill. Its output is a problem statement the engineer has
approved and a task list they can hold Claude to.

## Procedure

**1 · Restate the intent in one sentence.**
If it cannot be said in one sentence, the requirement is not understood yet. Say that rather
than papering over it with detail.

**2 · List every ambiguity, flat and unsorted.**
Concrete questions, not categories. "How much click history is retained?" — not "analytics
scope is unclear." Include the uncomfortable ones: retention, privacy, what counts as
success, who consumes this.

**3 · Escalate all of them. Sort none of them.**
Present the whole list to the engineer. They mark which items Claude may resolve. Delegation
is per item and does not carry to the next question. List every material ambiguity that could affect requirements, behavior, architecture, security, data, validation, scope, or acceptance — that sorting is a decision, and it buries whatever Claude kept.

**4 · Draft the normalized requirement.**
One sentence. Bounded, testable, and narrower than the original. State the assumptions it rests on explicitly. An assumption the engineer has not approved remains open. Present the normalized requirement to the engineer for approval before using it as the basis for task decomposition.

**5 · Decompose into tasks.**
Each task: intent, the modules it touches, and what it depends on. Record sequencing **only
where the order was genuinely contested** — a dependency table for obvious ordering is
decoration, and reviewers can tell. Where one ordering choice was load-bearing, say why in a
sentence.

**6 · Brownfield only — map the blast radius before editing anything.**
Name the impacted modules, APIs, and data flows. Then name what must stay **untouched**, and
what constraint protects it (usually: observable behaviour must not change). This list is
what makes the change reviewable.

**7 · Propose an impact level per task**, with reasoning, for the engineer to confirm.
Uncertain defaults to high.

**8 · Draft acceptance criteria** for each task and mark them **unapproved**. They do not
authorise anything until the engineer approves them.

## Output

Appended to that scenario's trace in `docs/SCENARIOS.md`. Open questions the engineer answers
become `DEC-00N` entries via `/decide` — this skill does not write decisions itself.

## Boundary

- Never resolve an ambiguity without explicit, per-item delegation for that question.
- Never sort open questions into "needs the engineer" and "I can handle this."
- Never start implementing, sketching code, or choosing a library.
- Never present an unapproved assumption as settled.
- If the requirement is clear enough that there are genuinely no ambiguities, say so — do not
  manufacture questions to look thorough.
