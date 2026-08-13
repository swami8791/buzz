# Brand OS Operations

Brand OS is used from Buzz. Config lives in [`examples/brand-os/`](../../examples/brand-os/).

## How to run Gate 1

1. Message Brand OS: `Run my brand`
2. Wait for ~5 numbered topics
3. Reply with numbers only, e.g. `2, 3, 5`

That reply is Gate 1. Brand OS then runs Researcher → Writer → Editor → unpublished RobinReach drafts for those numbers.

Do not also approve pillars, hooks, or outlines.

## How to run Gate 2

1. Brand OS reports `N drafts ready` with RobinReach IDs
2. Review the drafts in RobinReach (or the copy Brand OS posted)
3. Message Brand OS: `Publish {id} tomorrow at 8 AM` (or `Schedule post {id} for Tuesday at 8:00 AM CT`)

Only that ID goes live. Other drafts stay drafts.

Invalid as Gate 2: `Run my brand`, `continue`, `looks good`, `approved` with no post ID.

## Status

```text
BRAND OS: online
MODE: draft-only until Gate 2
DRAFTS READY: [N from RobinReach]
NEXT ACTION: Gate 1 numbers | pipeline | Gate 2
NEEDS YOU: none or the exact question
```

## Draft-only invariant

Until Gate 2 names an ID, Brand OS may:

- search Notion
- read knowledge and analytics
- research, write, edit
- create unpublished RobinReach drafts

It may not:

- publish
- schedule / reschedule
- delete scheduled or published posts

## Duplicate protection

A piece is a draft only when RobinReach currently has an unpublished post with that ID. Check RobinReach, not a local calendar. Record the ID in `examples/brand-os/knowledge/EXISTING.md` so Gate 1 does not re-propose it.

## Runtime (kept from the conversion)

- One user-facing Buzz agent, owner-only
- buzz-acp + Codex
- Idle timeout 1800s, max turn duration 3600s (idle must be less than max)
- Brand OS pubkey must be a relay member
- `BUZZ_AUTH_TAG` must resolve an owner or owner-only DMs are dropped
- Load the Brand OS persona, not a generic Buzz debugging prompt
- `Run my brand` must execute Gate 1, not only acknowledge the command

Attach Notion MCP and RobinReach MCP to the Codex session (`NOTION_TOKEN`, `ROBINREACH_MCP_COMMAND`, `ROBINREACH_API_KEY`). Recreate the four personas in Desktop from `buzz pack inspect ./examples/brand-os`.

## Failure modes worth remembering

These happened in production. They are bugs, not style:

- Too many handoffs: work died between extra agents. Fixed by four agents only.
- Too much state: local calendars drifted from RobinReach. Fixed by querying RobinReach.
- Silent failures: command recognized but not executed; generic persona; null pubkey; timeout config; not a relay member; no LinkedIn profile in RobinReach. Keep the checks above.

If Gate 1 returns no topics, the search failed — say that. Do not invent a slate. If RobinReach returns no draft ID, the slot is not done.

## Content range

Gate 1 should not dump six AI-governance variants. Use `knowledge/POSITIONING.md`. Healthcare is evidence, not the default topic.
