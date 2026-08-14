# AI-Assisted Engineering Template

A governance system for using AI as an accelerator inside engineering tasks, where the engineer
keeps every decision and owns the result.

It is not a productivity harness. It exists to make AI-assisted work **defensible** — so that
months later, or in a review, you can show what was decided, why, what it cost, and who
approved it.

Proven on a real project rather than designed in the abstract. Notes on what actually held up
are at the bottom.

## What's in it

```
CLAUDE.md                    Standing rules — loaded on every turn
.claude/skills/
  task/SKILL.md              Requirement → ambiguities → normalized problem → tasks
  decide/SKILL.md            Options → engineer's call → recorded
  execute/SKILL.md           Contract → implement → traceability
  validate/SKILL.md          Gates → risks → review prep → sign-off
docs/DECISIONS.md            The spine: every decision with alternatives and cost
```

## The five rules that do the work

**The engineer decides; AI executes.** `CLAUDE.md` lists the classes of choice AI may never
settle alone — technology, API shape, scope, trade-offs, security, anything changing shipped
behaviour.

**Acceptance criteria come before implementation, and they are the engineer's.** Whoever defines
"done" has made the decision. AI may draft criteria; they authorise nothing until approved.

**AI does not build, run, or test the project.** It supplies commands; the engineer runs them
and reports results, recorded attributed to them. No gate is claimed on unverified output.

**Decisions are recorded when made, not reconstructed afterwards.** With alternatives, what was
discarded, and what the choice costs — not justifications assembled later to fit what happened.

**Read before you assert.** No value that exists in a file may be written from assumption.

## Using it

1. Copy `CLAUDE.md` and `.claude/skills/` into your repository.
2. Replace `[YOUR NAME]` in `CLAUDE.md` and delete the instruction block.
3. Adjust the document budget table to your project — and keep it listing only documents that
   exist.
4. Create `docs/DECISIONS.md` from the template here. It fills up fast.

Then work normally. Invoke the skills by name at each phase (`/task`, `/decide`, `/execute`,
`/validate`) — see the honest note below about what happens if you don't.

## What actually held up

From one full project — a service with three work streams, twenty-four recorded decisions, and
a full test suite.

**The execution boundary was the strongest rule by a distance.** Because the assistant could not
run anything, three defects reached the written record instead of being silently fixed: a
redirect that returned `500` for every request, a configured URL pointing at a port nothing
listened on, and — the instructive one — a solution file containing no projects, so every build
had reported success while compiling nothing. All three were found by the engineer running
commands, and all three are in the log.

**Recording decisions as they happen made the final documents writable.** The summary and
architecture documents were assembled from records rather than memory, which took an hour
instead of a day and contained no reconstruction.

**Stating gaps beats implying coverage.** Gates that were never run stayed recorded as not run.
That reads as rigour, not weakness — and it is the thing that makes the rest of the record
credible.

## What didn't

**The skills were often not invoked by name.** Work ran conversationally and the skills acted as
background principles. They still shaped behaviour, but a skill nobody invokes is a document
with extra steps. Either invoke them deliberately, or fold their refusals into `CLAUDE.md` and
keep fewer.

**Rules without a check get bent under time pressure.** "Do not proceed on silence" was violated
whenever momentum mattered — a one-word reply taken as approval for several open questions. The
`Ambiguous approval is not approval` rule exists because of that, and it is still only a rule.

**Documents drift the moment a rule changes.** The budget table listed two documents that had
been cancelled, for most of the project. Hence the `Before reporting completion` audit — which
should have existed from the start.

## Hooks

Deliberately none. Hooks enforce deterministically where a rule merely asks, and the obvious
candidate is blocking build and test commands to make the execution boundary mechanical. It was
considered and left out, on the grounds that the system should be judged on the clarity of its
boundaries rather than tooling that hides whether they would hold. Add one if you observe drift.
