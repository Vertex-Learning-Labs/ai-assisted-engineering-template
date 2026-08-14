---
name: execute
description: Implement an approved task under a stated contract, and record what AI produced, what was edited, and what was rejected. Use when moving from an agreed task list into writing code, tests, or configuration, and when investigating a defect. Not for exploratory work — if the task or its acceptance criteria are not yet approved, this skill refuses and says which approval is missing.
---

# AI-assisted execution

Covers brief requirements 4 (AI-assisted execution) and 5 (output generation).

## Precondition

Requires an **approved** task from `/task` with **engineer-approved acceptance criteria**.
If either is missing, stop and name exactly which approval is absent. Do not proceed on a
task that looks obviously fine — auto-triggering on a task the engineer never approved is
the failure this precondition exists to prevent.

## Procedure

**1 · Restate the task contract, then stop for a one-line go.**

- **Intent** — what changes for a user of this system, in one sentence.
- **Constraints** — what must not change, what must not be touched, what must stay true.
- **Acceptance criteria** — the engineer's, verbatim.
- **Technical context** — the modules involved and how they connect.

Restating is not agreeing. The engineer's "go" is what authorises work, and this is where
silent decisions get caught — a constraint that reads two ways gets resolved here, in the
open, rather than quietly in the implementation.

**2 · Implement only what the contract covers.**
A fork discovered mid-task **halts the work** and invokes `/decide`. It is not resolved with
a reasonable-sounding default and mentioned afterwards.

**3 · Defect path** — when the task is a bug fix:
reproduce · isolate · **state the root cause before proposing a fix** · fix · regression test
that fails without the fix. A fix offered before the root cause is stated is refused, even
when it would work. The symptom fix that hides a wrong decision is the expensive kind — a
database path "corrected" when the real problem was the wrong data store entirely.

**4 · Report every artifact** as **generated**, **edited**, or **rejected**, with the rationale for each edit and rejection, and a **refined from** note where it took more thanone pass — what was wrong the first time.An artifact means a meaningful generated or modified file/output contributing to the task; intermediate edits within a single implementation pass do not require separate rows.

**5 · Append the `docs/AI_USAGE_LOG.md` row immediately.** Not at the end of the task, not in
a later documentation pass. The gap is where drift starts.

**6 · Change safety.** Small, reversible commits with a stated intent. Where existing
behaviour is being changed, the regression test that pins it comes **first**. State the
rollback line for anything high-impact.

**7 · Name the quality gates now due** and hand off to `/validate`.

## Boundary

- **No build, run, or test.** Supply the exact command for the engineer's terminal. Nothing
  enforces this mechanically — it holds because the rule is followed, which makes following
  it exactly when it is inconvenient the point.
- No scope expansion. No unrequested improvements, tidying, or "while I was in there."
- Existing tests are never edited to make a change pass. If they must change, that is a
  decision — stop and invoke `/decide`.
- Never omit an edited or rejected row to make the record look smooth. Those rows are the
  evidence of engineer ownership; a log where everything was accepted proves nothing.
- Never describe work as done. Report what was produced and which gates remain open.
- If unrelated issues are discovered, record them as observations or follow-up items without modifying them. Do not expand scope.
