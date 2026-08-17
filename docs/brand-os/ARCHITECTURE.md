# Brand OS Architecture

Locked 2026-08-13. This file is the architecture. [`BUILD_HISTORY.md`](BUILD_HISTORY.md) is how we got here, including the over-engineered version this lock replaces.

## System boundary

```text
Notion owns knowledge.
RobinReach owns posts.
Buzz owns conversation.
Brand OS coordinates them.
```

Buzz is the executive interface. It is not the content database and not the publishing system.

## Diagram

```text
Nehal
  |
  v
Buzz (conversation)
  |
  v
Brand OS (orchestrator)
  |
  +-- search --> Notion
  +-- read    --> knowledge/ (voice, positioning, existing IDs)
  +-- query   --> RobinReach (analytics, draft/scheduled/published)
  |
  |  after Gate 1 numbers:
  v
Researcher --> Writer --> Editor --> RobinReach unpublished draft
  |
  |  after Gate 2 named ID:
  v
RobinReach schedule / publish that ID only
```

## Persistent agents (four)

### Brand OS (user-facing)

- Runs Gate 1 and Gate 2 in conversation
- Searches Notion and knowledge for the topic slate
- Dispatches Researcher, Writer, Editor
- Creates unpublished RobinReach drafts after Editor pass
- Schedules/publishes only when Gate 2 names a post ID

Does not write the post, does not pick topics without Gate 1 numbers, does not add agents.

### Researcher

- Searches Notion, knowledge, and current public information
- Returns sourced findings and claim status (VERIFIED / LIKELY / UNVERIFIED / CONFLICTING)
- Does not write, hook, or publish

### Writer

- One pass: analyze audience → 5 hooks → select strongest → write the post
- Audience analysis and hooks are tasks inside this agent
- Grounds copy in the research pack and `knowledge/VOICE.md`

### Editor

- Challenges the selected hook, the claims, and the voice
- `pass` or `revise` — no numeric score gate, no third human gate
- Does not rewrite the post or call RobinReach

## Tools (not agents, not stages)

### Notion

Search tool for media, press, essays, case studies, publications, talks, company history, current projects, and accomplishments. See [`NOTION_CONTENT_LIBRARY.md`](NOTION_CONTENT_LIBRARY.md).

### RobinReach

Account discovery, analytics, unpublished draft creation, and — after Gate 2 — schedule/publish of a named ID. RobinReach is the post-state store.

## Human gates (two)

1. **What should we talk about?** `Run my brand` → ~5 options → user numbers.
2. **Should this actually go live?** Drafts listed → `Publish {id} tomorrow at 8 AM`.

## Internal states (three)

`IDEA` → `DRAFT` → `PUBLISHED`

A few IDs in `examples/brand-os/knowledge/EXISTING.md` record what already exists. No Brand OS duplicate of RobinReach scheduled/published.

## Explicitly out of architecture

| Removed | Where the work went |
|---------|---------------------|
| Audience Analyst | Writer task |
| Hook Master | Writer task (5 hooks, then select) |
| Content Director | Brand OS Gate 1 slate |
| Claims Guard | Researcher status + Editor challenge |
| Cynical Editor as extra agent | Editor |
| Performance Analyst | Optional RobinReach analytics read during Gate 1 |
| Content Planner / local calendar | RobinReach |
| Editor score >= 85 as a gate | Editor pass/revise |
| Giant content state machine | IDEA / DRAFT / PUBLISHED only |
