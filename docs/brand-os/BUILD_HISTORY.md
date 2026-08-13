# Brand OS Build History

This is a record of what shipped and what we stripped. The locked architecture is [`README.md`](README.md) and [`ARCHITECTURE.md`](ARCHITECTURE.md), plus [`examples/brand-os/`](../../examples/brand-os/).

## Locked architecture — 2026-08-13

Production with many handoffs, extra agents, and duplicated post state already felt like failure. The lock is:

- Persistent agents: Brand OS + Researcher + Writer + Editor
- RobinReach = draft/publish tool; Notion = search tool
- Two gates only: numbered topics, then `Publish {id} …`
- Internal states: IDEA → DRAFT → PUBLISHED
- No duplicate RobinReach store
- Writer does audience + 5 hooks; Editor challenges the hook
- Do not add Audience Analyst, Hook Master, or a giant state machine

What this revision **removed from the docs/config**: Audience Analyst, Hook Master, Content Director, Claims Guard, Performance Analyst, Content Planner as persistent agents; editor score >= 85 as a gate; local calendar as source of truth; SOURCE→CONTENT as a Notion pipeline; 5–8 concept slates that skip numbered-only Gate 1; IDEA→…→ANALYZED.

What this revision **kept**: one Buzz-facing agent; buzz-acp + Codex; `Run my brand`; draft-only until a named post ID; two human controls (topics and go-live); positioning; healthcare-as-proof; RobinReach IDs from the first live run; operational bugfixes (pubkey, timeouts, membership, owner tag, persona routing).

---

## Step 1 - Project bootstrap

Created the `nehal-brand-os` project structure, environment handling, and RobinReach MCP configuration scaffolding.

## Step 2 - Buzz to Codex smoke test

Created a minimal Buzz persona pack and a `brand-test` agent using Codex through `codex-acp`.

Verified response: `Brand OS connected successfully.`

## Step 3 - RobinReach MCP connection

Connected RobinReach to the Codex runtime through MCP. Read-only test passed.

## Steps 4–12 - Over-built creative team (retired)

The original build added strategist, LinkedIn writer, editor, researcher, content director, performance analyst, and content planner, plus later Audience Analyst and Hook Master as preferred extras.

That is the system the 2026-08-13 lock replaces. Useful leftovers: knowledge of voice/claims, draft-only after the planner auto-scheduled six posts, and Researcher / Writer / Editor as the only surviving creative roles.

## Step 13 - Master command

Created `run-my-brand` as the single orchestration command.

## Step 14 - Buzz Brand OS interface

Exposed orchestration through one Buzz-facing agent called `Brand OS`.

## Safety correction - Draft-only mode

After six posts were scheduled without explicit approval, scheduling and publishing require a specific post ID. Kept.

## Buzz Desktop integration fixes (kept)

- Null `pubkey` broke the managed-agent store — repair to string
- Idle timeout 1800s, max turn 3600s
- Admit Brand OS pubkey to the community
- Restore `BUZZ_AUTH_TAG` owner for owner-only DMs
- Load Brand OS persona, not generic debugging
- Execute `Run my brand` instead of acknowledging it

## RobinReach profile connection

Zero drafts until a LinkedIn profile was connected in RobinReach.

## First successful live production run

Unpublished drafts (still listed in `examples/brand-os/knowledge/EXISTING.md`):

- 933403 - Design the feedback capture workflow before improving the AI model
- 933404 - Why founders should budget integration and workflow change before approving a new AI capability
- 933405 - The four debts AI products accumulate: model, data, workflow, and governance debt
- 933406 - Why AI evaluations should show failure distributions, not just average performance
- 933407 - Run AI workflows in shadow mode before granting them production authority
- 933409 - Why founders should assign an explicit owner to every recurring operational bottleneck

`SCHEDULED: 0`, `PUBLISHED: 0`. Content mix was too AI-workflow-heavy because there was no Gate 1. Gate 1 is now the numbered slate.
