# Nehal Brand OS

Locked 2026-08-13. One orchestrator, three workers, two gates. Do not add agents, gates, or states beyond this document.

## Goal

Agents do the research, writing, editing, and unpublished draft work. Nehal chooses topics by number and names the post ID that may go live.

## Positioning

> Founder building high-stakes startups across AI, data, and real-world systems

Healthcare is proof of operating rigor, not the brand.

## Architecture

```text
                BRAND OS
             (Orchestrator)
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
   RESEARCHER    WRITER     EDITOR
        │          │          │
        └──────────┴──────────┘
                   │
                   ▼
             ROBINREACH
               DRAFT
```

Implementation: [`examples/brand-os/`](../../examples/brand-os/) (persona pack, prompts, skills, MCP tool wiring).

Persistent agents: **Brand OS, Researcher, Writer, Editor**. RobinReach is the publish/draft tool, not a fourth content agent. Notion is a search tool, not a workflow.

Writer tasks (not agents): analyze audience → generate 5 hooks → select strongest → write post. Editor challenges that hook choice.

## Two gates

### Gate 1 — What should we talk about?

User: `Run my brand`

Brand OS searches Notion + existing knowledge + current relevant information and returns ~5 topic options (examples: clinical product adoption vs AI adoption; biggest mistake building RealTime Clinic; why building with autonomous agents now; what founders misunderstand about real-world data; an old prediction that turned out wrong).

User replies with numbers (`2, 3, 5`). That is the entire Gate 1 mechanism.

Then: Researcher → Writer → Editor → RobinReach unpublished drafts.

### Gate 2 — Should this actually go live?

Brand OS: `N drafts ready`. User reviews. User: `Publish {id} tomorrow at 8 AM`. Nothing else gets published.

## Internal state

Only `IDEA` → `DRAFT` → `PUBLISHED`, plus a few IDs in `examples/brand-os/knowledge/EXISTING.md` so the system knows what already exists.

RobinReach already knows draft/scheduled/published. Do not build another database that duplicates it.

Notion owns knowledge. RobinReach owns posts. Buzz owns conversation. Brand OS coordinates them.

## Ownership of work

| Surface | Owns |
|---------|------|
| Buzz | Conversation, the two gates |
| Brand OS | Coordination, Gate 1 slate, Gate 2 dispatch |
| Notion | Source library (search) |
| RobinReach | Draft / scheduled / published |

## Runtime

One user-facing Buzz agent. buzz-acp + Codex. Command-driven. Draft-only until Gate 2 names a post ID.

## Not this system

Do not implement:

`IDEA → TOPIC_REVIEW → APPROVED_TOPIC → WRITING → EDITING → CLAIMS → READY → APPROVED → SCHEDULED → PUBLISHED → ANALYZED`

Do not add Audience Analyst, Hook Master, Content Director, Claims Guard, Performance Analyst, or Content Planner as persistent agents.

Three capable agents with good context beat eight agents handing JSON around. Simplify from here, not expand.
