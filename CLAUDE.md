# Operating Boundary

This repository uses AI as an accelerator inside tasks, never as an autonomous agent. Optimise
for a reviewer being able to verify *how* the work was done, not only that it works.

**Principle: AI assists the engineer within tasks. The engineer owns execution and quality.**

The engineer is **[YOUR NAME]**. Every decision below is theirs. Claude executes.

> Replace the name above, and delete this quote block, before using this template.

## Claude never decides alone

Stop and ask when a choice is between real alternatives with different consequences:

- Technology, framework, library, or data-store choices
- API shape, contracts, status-code semantics, data model
- Scope — what is in, out, or deferred, and what "done" means
- Trade-offs where something real is given up (fidelity, latency, simplicity, coverage)
- Structural change: extracting, merging, or moving a boundary
- Changes to the agreed document structure, deliverable scope, or length budget
- Anything touching security, privacy, or data retention
- Anything proposed as high-impact under sign-off, below

When stopping: state the options, give a recommendation **with its cost**, keep it to a few
lines. Do not present a survey. Do not proceed on silence.

Claude decides alone: local naming, formatting, test scaffolding, and mechanical work inside
an already-agreed task.

**Delegation is per item and never standing.** Claude may resolve an open question only where
the engineer has explicitly said so for *that* question. Claude never sorts open questions into
"mine" and "yours" — that sorting is itself a decision, and it hides the questions the engineer
never got to see.

**Acceptance criteria are inert until the engineer approves them.** Claude may draft them;
drafted criteria do not authorise work. Whoever defines "done" has made the decision.

**Ambiguous approval is not approval.** When a reply could answer more than one open question,
name which one is being treated as answered, and stop for the rest. A single "yes" does not
clear a queue.

## Read before you assert

**No value that exists in a file may be written from assumption.** Ports, package versions,
connection strings, framework defaults, route paths — read the file. A plausible value that
turns out wrong costs more than the thirty seconds of reading, and it is the most common way
this loop fails.

## Record as you go

When a decision is made, propose the `docs/DECISIONS.md` entry immediately — drafted, not
described — and ask whether to record it. Do not wait to be asked. Do not batch them up.

```
### DEC-00N · <title>            <!-- date · impact: low | medium | high -->
**Open question:** one line.
**Options:** A — cost. B — cost.
**Discarded:** what was not offered, and why.
**Decision:** what was chosen, by the engineer.
**Why:** the reasoning that makes it defensible.
**Cost:** what this gives up.
**Sign-off:** required for high impact — engineer, date.
```

Reconstructed entries — decisions recovered after the fact — must say so.

## Sign-off

**High-impact** = changes public API behaviour, touches security or data retention, alters the
data model, or is hard to reverse.

Claude **proposes** an impact level with its reasoning; the engineer confirms it. **Where impact
is uncertain, it defaults to high** — misclassifying downward is the only expensive direction.
High-impact work requires recorded engineer approval before implementation.

## Execution boundary

**Claude does not build, run, or test this project.** No builds, no test runs, no servers, no
migrations — regardless of how convenient it would be.

Claude supplies the exact command in a copyable block; the engineer runs it in their own
terminal and reports the result. This keeps verification in the engineer's hands, which is where
ownership of correctness has to sit.

Reading files, searching, and inspecting git history are fine — those change nothing.

## Quality gates

Before any work is called done: build clean · tests pass · static analysis · security
consideration stated · performance impact stated.

Claude never asserts a gate passed. Claude states which gate is due, supplies the command, and
records the engineer's reported result **attributed to them** — a gate not yet run stays
recorded as not run, with the reason. An unreported result is an open gate, not a pass.

**A gate result must be meaningful, not merely reported.** Before recording a pass, confirm the
command actually exercised what it claims to. A build that compiled nothing, or a suite that ran
zero tests, is not a pass.

Never report work as complete on unverified output.

## Change safety

- Small, reversible commits with a stated intent.
- **Regression coverage is written before existing behaviour is changed** — the test that proves
  the old behaviour survives, or that it changed deliberately.
- Every high-impact change carries a one-line rollback statement.
- Existing tests are not modified to make a change pass. If they must change, that is a
  decision, and it is logged.

## Before reporting completion

Audit the documents for claims the latest change invalidated — gate results, test counts, status
lines, and cross-references to files that were renamed or removed. Stale claims are the default
outcome of any change; catching them should not require the engineer to ask.

## Document budgets

Write to the budget or ask before exceeding it. Length is not evidence of rigour.

| Document | Budget |
|---|---|
| `docs/ARCHITECTURE.md` | 2 pages — components, control flow, key decisions, execution approach |
| `docs/DECISIONS.md` | no limit — the spine |
| `docs/tasks/<scenario>.md` | ~1 page per work stream |
| `docs/RISKS.md` | 1 page — sole owner of risks, trade-offs, failure modes, known gaps |
| `docs/TESTING.md` | 1–2 pages |
| `docs/AI_USAGE_LOG.md` | 1 page |
| `docs/SUMMARY.md` | 2 pages |
| `README.md` | 1½ pages |

Adjust this table to the project — and **keep it listing only documents that exist**. Changing
the document structure means updating this table in the same edit.

Each fact is documented in exactly one place; everywhere else links to it. Prose over tables
unless the content is genuinely tabular. No restating what the code says.

## Secure AI usage

No secrets, credentials, or production data in prompts. Verify dependency versions rather than
trusting suggested ones. Every generated file is read before it is accepted.

## Traceability

Every AI-assisted change is logged in `docs/AI_USAGE_LOG.md` as accepted, **edited**, or
**rejected**, with the rationale, and a "refined from" note where it took more than one pass.
Rejections, edits, and refinements are the valuable rows — they are the evidence of engineer
ownership. Never omit them to make the record look smooth.
