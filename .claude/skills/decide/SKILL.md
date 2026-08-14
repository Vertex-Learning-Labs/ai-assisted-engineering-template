---
name: decide
description: Put a decision in front of the engineer and record their answer. Use whenever work reaches a fork between real alternatives — technology, API shape, data model, scope, trade-offs, document structure, anything touching security or privacy — and use it from inside other skills, not only when asked. If Claude notices it already passed such a fork without stopping, use this skill to report and log that.
---

# Controlled oversight

Covers brief requirement 7. This is the skill that makes the system engineer-led rather than
autonomous. Every other skill calls into it.

## Procedure

**1 · State the open question in one line.**
If it takes a paragraph, it is more than one decision — split it.

**2 · Give two or three real options.**
Each with **what it costs**, not only what it offers. An option nobody would choose is not an
option, it is a prop that makes the preferred answer look inevitable.

**3 · State what was considered and discarded, and why.**
Whoever writes the options controls the decision. Omitting a fourth option is a decision made silently. This step is what keeps authorship of the choice with the engineer, so it is not optional. Invite the engineer to add an option Claude did not raise. A recommendation is not a decision. The decision record must identify the engineer's selected option explicitly.

**4 · Recommend one, and say what would change the recommendation.**
The recommendation names what it gives up. If nothing would change it, it is not a
recommendation — it is a preference being laundered as advice, and it should be re-examined.

**5 · Stop.**
Silence is not consent. An unanswered decision blocks the work that depends on it; it does
not get resolved by a default. Do not begin adjacent work to fill the wait if that work
assumes an answer.

**6 · On the engineer's answer, draft the entry.**
Use the `DEC-00N` format from `CLAUDE.md`, including what was discarded. Propose the impact
level with reasoning; the engineer confirms it. Record sign-off for high impact.

## Output

`docs/DECISIONS.md` — the spine of the whole record. Everything else cites `DEC-00N` by ID
and never restates the reasoning.

## Boundary

- Never proceed on an unanswered decision.
- Never present a survey of every possibility; three real options beat seven.
- Never bury the recommendation, and never give one without its cost.
- Never assign an impact level unilaterally.
- **If Claude discovers it already passed a fork without stopping, that is a defect in the
  system, not a footnote.** Say so plainly, log the decision retroactively marked
  `reconstructed`, and let the engineer overturn it. A decision Claude made and the engineer
  merely tolerated is not the engineer's decision.
