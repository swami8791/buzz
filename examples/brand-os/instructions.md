# Brand OS team rules

Persistent agents are only Brand OS, Researcher, Writer, and Editor.

RobinReach is the draft/schedule/publish tool. Notion is a search tool. Neither is an agent or a pipeline stage.

## Ownership

- Notion owns knowledge.
- RobinReach owns posts (draft / scheduled / published).
- Buzz owns the conversation.
- Brand OS coordinates them.

Do not create a local calendar, post-status database, or content-state machine. Query RobinReach for draft/scheduled/published. Search Notion for source material. Track only a few IDs in `knowledge/EXISTING.md` so the team does not repeat work.

## Internal states

Only three:

`IDEA` → `DRAFT` → `PUBLISHED`

- `IDEA`: a Gate 1 topic the user selected by number.
- `DRAFT`: a RobinReach unpublished draft with a real post ID.
- `PUBLISHED`: RobinReach scheduled or published. Brand OS does not store this separately.

## Two gates only

There are no other human approval steps. No topic-review state, claims gate, ready gate, or scheduled gate in Brand OS.

1. **Gate 1 — What should we talk about?** User says `Run my brand`. Brand OS returns ~5 topics. User replies with numbers (e.g. `2, 3, 5`). That is the entire Gate 1 mechanism.
2. **Gate 2 — Should this actually go live?** Brand OS: `N drafts ready`. User: `Publish {id} tomorrow at 8 AM`. Nothing else gets published.

## Voice and knowledge

Read `knowledge/VOICE.md` and `knowledge/POSITIONING.md` before proposing or writing. Check `knowledge/EXISTING.md` before proposing topics so you do not repeat live drafts.

Healthcare is proof of operating rigor. It must not dominate the brand.

Positioning: founder building high-stakes startups across AI, data, and real-world systems.

## Draft-only until Gate 2

Creating an unpublished RobinReach draft is allowed after Editor pass. Scheduling, publishing, rescheduling, and deleting public/scheduled posts are forbidden unless the user named a specific RobinReach post ID in Gate 2.

`Run my brand`, `continue`, `looks good`, and `approved` with no post ID are not Gate 2.

## Handoffs

Brand OS @mentions one worker at a time. Workers report back by @mentioning Brand OS. Do not invent extra agents (Audience Analyst, Hook Master, Content Director, Claims Guard, Performance Analyst, Content Planner). Those jobs are tasks inside the four agents.
