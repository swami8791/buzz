# Brand OS Operations

## Normal operating mode

Brand OS is designed to be used from Buzz, not from Cursor, once the system is healthy.

Primary user command:

`Run my brand`

The preferred workflow is editorial-control-first:

1. Brand OS researches current source material and performance.
2. Brand OS proposes a short editorial slate.
3. Nehal chooses which ideas to pursue.
4. Internal agents create hooks, write, fact-check, and edit.
5. Approved pieces become unpublished RobinReach drafts.
6. Brand OS returns draft IDs for review.
7. Nehal explicitly approves a specific draft before scheduling or publishing.

## Recommended Brand OS responses

### Status

```text
BRAND OS: online
MODE: draft-only
DRAFTS READY: [number]
NEXT ACTION: [short description]
NEEDS YOU: none or exact issue
```

### Editorial slate

Each idea should include:

- title / topic
- content pillar
- target audience
- why it matters now
- why it fits Nehal's brand
- source material to draw from
- recommended format

The system should ask Nehal to choose by number/letter rather than requiring him to invent topics.

### Draft completion

```text
BRAND OS: complete
NEW DRAFTS: [number]
READY FOR REVIEW:
- [POST ID] | [topic]
RECOMMENDED TIMES:
- [time]
SCHEDULED: 0
PUBLISHED: 0
NEEDS YOU: Review drafts
```

## Approval rules

A public action requires explicit post-specific approval.

Valid examples:

- `Approve post 933403`
- `Schedule post 933403 for August 11 at 8:00 AM CT`
- `Publish post 933403`

Invalid as public-action authorization:

- `Run my brand`
- `continue`
- `looks good`
- `approved` with no post ID
- `handle LinkedIn`

## Draft-only invariant

The normal Brand OS workflow must not call scheduling or immediate-publication tools.

Normal run may:

- read analytics
- inspect account and audience timing
- research
- write
- validate
- create unpublished drafts

Normal run may not:

- use immediate publish
- schedule
- reschedule
- delete
- alter already-published content

## Duplicate protection

A content slot is complete only when a corresponding RobinReach post currently exists and is an unpublished draft with a valid RobinReach post ID.

Do not count as complete:

- planned topics
- recommended times
- stale local calendar entries
- deleted RobinReach posts
- previously scheduled posts that were removed
- stale post IDs

Before creating a draft, check both local calendar state and live RobinReach state.

## Performance learning

Performance analysis should prefer repeated patterns over one-off outcomes.

Do not optimize for impressions alone.

Useful signals may include:

- comments from desired audiences
- saves
- shares
- profile visits
- meaningful reactions
- topic/pillar patterns
- format patterns
- hook style
- posting time

The system should not chase engagement bait or turn Nehal into a generic AI-content account.

## Content diversity

Maintain range across:

- BUILDING
- OPERATOR
- PROOF
- PERSPECTIVE

Avoid producing multiple posts that are merely variations of the same AI-workflow thesis.

Use healthcare selectively as proof of difficulty, evidence, and operating experience.

## Failure modes encountered during setup

### Buzz Desktop agent store parse failure

Symptom:

`invalid type: null, expected a string`

Root cause:

Brand OS record contained a null `pubkey` where Buzz expected a string.

Fix:

Repair the managed-agent store record against the expected schema and validate the entire store.

### Harness timeout configuration

Symptom:

`idle_timeout (3600s) must be less than max_turn_duration (3600s)`

Fix:

- idle timeout: 1800 seconds
- max turn duration: 3600 seconds

### Relay membership failure

Symptom:

`Auth failed: restricted: not a relay member`

Fix:

Admit the Brand OS public key to the active Buzz community/relay membership list.

### DM messages received but no response

Root cause:

`respond_to=owner-only` had no resolved owner due to an invalid `BUZZ_AUTH_TAG`; inbound events were dropped. ACP text output also needed to be sent back as Buzz messages.

Fix:

Restore owner resolution, preserve owner-only access, and route agent output into the same Buzz thread.

### Generic Buzz debugging persona loaded

Symptom:

Brand OS responded as a Buzz debugging/support agent rather than a personal-brand manager.

Fix:

Ensure the active Buzz-managed Brand OS definition loads the Brand OS persona and routes `Run my brand` to the existing orchestration rather than a generic fallback prompt.

### Command recognized but orchestration not executed

Symptom:

Brand OS returned internal acknowledgement/debug text instead of executing the production workflow.

Fix:

Route the command into the actual `run-my-brand` orchestration and return the final executive summary to Buzz.

### Zero drafts despite successful planning

Causes encountered:

- an earlier foreground test was intentionally aborted by piping through `head`
- RobinReach initially had no LinkedIn profile connected

After the LinkedIn profile was connected, the live production flow created six unpublished drafts successfully.

## Current known behavior

A live Brand OS run successfully created six RobinReach drafts and returned IDs while keeping scheduling and publishing at zero.

The next behavior change should insert an editorial approval gate before draft creation, so Nehal chooses among proposed concepts before the creative pipeline runs.