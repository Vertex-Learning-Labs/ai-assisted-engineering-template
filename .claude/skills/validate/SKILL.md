---
name: validate
description: Run the quality gates, surface risks and failure modes, and prepare the change for review. Use when an implemented task claims to be done, before it is committed or called complete, and when a scenario is being closed out. Also use when asked what could go wrong with a change, or to prepare a reviewer-facing summary.
---

# Validation and risk control

Covers brief requirement 6, plus safe change management and review preparation from the
evaluation criteria.

## Precondition

An implemented task from `/execute`. Validating something not yet built produces a checklist,
not evidence — say so instead.

## Procedure

**1 · Walk all five gates.** Name each one explicitly, every time:

| Gate | What it means here |
|---|---|
| Build | Compiles clean, warnings included |
| Tests | Unit and integration suite |
| Static analysis | Analyzers / linting |
| Security | What this change exposes; input handling, data reaching a response |
| Performance | What it costs on the hot path; extra queries, extra round trips |

**2 · For each gate, supply the exact command in a copyable block — or record "not run, and
why."** An honest gap outscores a fabricated pass, and it survives a reviewer asking about it.

**3 · Record the engineer's reported result, attributed to them.**
"Engineer ran `X` — 24 passed." An unreported result stays **open**. It never becomes a pass
through optimism or the passage of time. Claude does not run these; the engineer does.

**4 · Propose risks with severity left unrated.**
What could fail, under what conditions, and what would be observed. Severity is the
engineer's call — it is a business judgment with consequences, not a technical label. An
unrated risk is an open item, not a closed one. Output to `docs/RISKS.md`, the sole owner of
risks, trade-offs, failure modes, and known gaps.

**5 · Change safety.**
Confirm that regression coverage preceded any change to existing behaviour. State the
rollback line for high-impact work: exactly how this is undone. Confirm no existing test was
edited to make the change pass.

**6 · Produce the reviewer-facing change summary.**

- What changed, and why
- **What to scrutinise** — the part most likely to be wrong
- What is deliberately **not** covered, and why that was acceptable
- Residual risk, in one sentence

This is what makes the work *reviewable*, which is the brief's own word for the outcome.

**7 · Request sign-off** where the change is high-impact.

## Boundary

- **Never assert a gate passed.** Claude did not run it and cannot know.
- Never call work complete on unverified output, and never let an open gate roll silently
  into the next task.
- Never rate a risk's severity, and never quietly drop a risk the engineer has not yet rated.
- Never propose a weak test to close a gap that is better documented. A stated limitation is
  a stronger artifact than a test that pretends to cover something it does not.
