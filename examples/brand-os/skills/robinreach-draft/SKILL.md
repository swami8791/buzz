---
name: robinreach-draft
description: "Create unpublished RobinReach drafts. Schedule or publish only after Gate 2 names an ID."
---

# RobinReach

RobinReach owns post state: draft, scheduled, published. Brand OS does not keep a second copy of that state.

## Allowed without Gate 2

- List accounts / profiles
- Read analytics (optional input to Gate 1)
- Validate post copy
- Create **unpublished** drafts
- Read a post by ID

## Forbidden without Gate 2

- Immediate publish
- Schedule / reschedule
- Delete scheduled or published posts
- Change already-published copy

Gate 2 is a user message that names a RobinReach post ID, such as `Publish 933403 tomorrow at 8 AM`.

## Creating a draft

Only after Editor `pass`.

1. Query RobinReach for existing drafts so you do not duplicate an ID or an already-used idea in `knowledge/EXISTING.md`.
2. Create an unpublished draft.
3. Keep the returned post ID. That ID **is** the draft. Do not also write a local calendar row.
4. Append one line to `knowledge/EXISTING.md`: topic, RobinReach ID, `DRAFT`.

A topic is not done until RobinReach returns a real unpublished post ID.

## Gate 2 publish / schedule

1. Confirm the ID exists and is still a draft in RobinReach.
2. Apply schedule or publish to **that ID only**.
3. Leave every other draft untouched.
4. In `EXISTING.md`, you may note the ID moved to RobinReach scheduled/published. Do not invent Brand OS states like READY, APPROVED, or ANALYZED.
