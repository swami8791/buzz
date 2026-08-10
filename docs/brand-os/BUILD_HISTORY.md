# Brand OS Build History

This document captures the implementation sequence and the verified milestones reached during the initial build.

## Step 1 - Project bootstrap

Created the `nehal-brand-os` project structure, environment handling, and RobinReach MCP configuration scaffolding.

## Step 2 - Buzz to Codex smoke test

Created a minimal Buzz persona pack and a `brand-test` agent using Codex through `codex-acp`.

Verified response:

`Brand OS connected successfully.`

Smoke test passed.

## Step 3 - RobinReach MCP connection

Connected RobinReach to the Codex runtime through MCP.

Read-only test passed and RobinReach tools were discovered, including account, post, analytics, media, style, comment, template, and repurposing operations.

## Step 4 - Brand Strategist

Created `brand-strategist`.

Initial test topic:

`How founders identify which failures in an AI product come from the model, the data pipeline, or the surrounding human workflow`

Test passed.

## Step 5 - LinkedIn Writer

Created `linkedin-writer` and verified strategist-to-writer handoff.

Initial hook:

`When an AI product fails, blaming the model is often the fastest way to fix the wrong problem.`

Test passed.

## Step 6 - Brand Editor

Created `brand-editor` with revision loops and a quality gate.

Initial pipeline score: 93.

Status: approved.

## Step 7 - RobinReach draft creation

Created a safeguarded RobinReach publisher component.

Verified creation of an unpublished draft with publishing safeguards active.

## Step 8 - Brand Knowledge Base

Created:

- PROFILE.md
- VOICE.md
- CLAIMS.md
- CONTENT-PILLARS.md

Updated strategist, writer, and editor to read the knowledge base.

Claims safety test passed.

## Step 9 - Brand Researcher

Created `brand-researcher` plus:

- SOURCES.md
- RESEARCH-QUEUE.md

Initial test added 4 verified claims and 13 research-queue items.

Conflict handling passed.

## Step 10 - Content Director

Created `content-director` and ran a full autonomous draft cycle.

Test topic:

`Why founders should define decision rights before adding another coordination meeting`

Editor score: 94.

RobinReach draft created successfully.

## Step 11 - Performance Analyst

Created `performance-analyst` and PERFORMANCE.md.

Initial analysis correctly concluded that there was not yet enough published LinkedIn engagement to declare winners.

Feedback loop passed.

## Step 12 - Content Planner

Created `content-planner` with a rolling 14-day calendar.

The initial implementation scheduled six posts automatically. This behavior was later identified as an approval-boundary mistake and reversed.

This led to the permanent DRAFT-ONLY safety model.

## Step 13 - Master command

Created `run-my-brand` as the single orchestration command.

Dry run passed, recognized six existing scheduled posts, and created zero duplicates.

## Step 14 - Buzz Brand OS interface

Exposed the orchestration through one Buzz-facing agent called `Brand OS`.

Internal pipeline agents remained hidden behind the interface.

## Safety correction - Draft-only mode

After six posts were scheduled without Nehal's explicit approval, the system was changed so that scheduling and publishing require explicit post-specific approval.

Verified:

- DRAFT-ONLY MODE: active
- scheduling block: passed
- publishing block: passed
- post-specific approval: required

## Buzz Desktop integration fixes

### Managed-agent visibility

Brand OS was registered in Buzz Desktop's managed-agent store.

### Agent-store parse error

A null `pubkey` caused the store to fail parsing.

The store was repaired, validated, and existing agents were preserved.

### Timeout configuration

Brand OS originally failed because idle timeout and max turn duration were both 3600 seconds.

Final settings:

- idle timeout: 1800 seconds
- max turn duration: 3600 seconds

Harness start passed.

### Relay authorization

Brand OS initially failed with:

`Auth failed: restricted: not a relay member`

Its public key was added to the active Buzz community. Relay authentication and harness startup then passed.

### Owner-only DM routing

Direct messages were received but dropped because `respond_to=owner-only` had no resolved owner due to an invalid `BUZZ_AUTH_TAG`.

The owner mapping and outbound Buzz response path were fixed while preserving owner-only access.

### Wrong persona / generic debugging response

Brand OS temporarily behaved like a generic Buzz debugging assistant.

The active persona and command routing were corrected so `status` and `Run my brand` route to Brand OS behavior.

### Command recognition vs execution

At one point Brand OS returned only `RUN_MY_BRAND_RECOGNIZED` instead of executing the workflow.

The command handler was corrected to invoke the existing production orchestration and return its executive summary to Buzz.

## RobinReach profile connection

The production pipeline initially created zero drafts because no LinkedIn profile was connected in RobinReach.

After the LinkedIn profile was connected, the live workflow succeeded.

## First successful live production run

Brand OS created six unpublished RobinReach drafts:

- 933403 - Design the feedback capture workflow before improving the AI model
- 933404 - Why founders should budget integration and workflow change before approving a new AI capability
- 933405 - The four debts AI products accumulate: model, data, workflow, and governance debt
- 933406 - Why AI evaluations should show failure distributions, not just average performance
- 933407 - Run AI workflows in shadow mode before granting them production authority
- 933409 - Why founders should assign an explicit owner to every recurring operational bottleneck

The run correctly reported:

- NEW DRAFTS: 6
- SCHEDULED: 0
- PUBLISHED: 0
- NEEDS YOU: Review drafts

## Product lesson from the first live run

The infrastructure worked, but the content mix exposed an important design problem: Nehal had no say in the editorial topics before drafts were created, and the ideas skewed too heavily toward AI workflow/governance.

The next planned revision is therefore an editorial approval gate:

1. agents research and propose 5-8 editorial concepts
2. Nehal chooses the ideas
3. the creative pipeline executes the selected ideas
4. RobinReach receives unpublished drafts
5. public action still requires post-specific approval

## Revised creative team direction

The preferred creative core is:

- Researcher
- Audience Analyst
- Hook Master
- Main Ghostwriter
- Cynical Editor

Existing infrastructure remains around that core:

- Content Director
- Claims Guard
- Performance Analyst
- Content Planner
- RobinReach integration
- Brand Knowledge Base

This structure is intended to maximize agent execution while preserving editorial and publication control.