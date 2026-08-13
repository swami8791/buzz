# Brand OS

Locked 2026-08-13: one orchestrator, three workers, two gates.

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

The user talks to Brand OS in Buzz. Internal agents stay behind that conversation.

## Validate

```bash
buzz pack validate ./examples/brand-os
buzz pack inspect ./examples/brand-os
```

Runtime is buzz-acp + Codex (same conversion as the 2026-08-10 Brand OS agent). Recreate the four personas in Buzz Desktop from `buzz pack inspect`; desktop import does not load this pack directory yet.

Attach Notion MCP and RobinReach MCP to the Brand OS session. Point `NOTION_TOKEN` and `ROBINREACH_MCP_COMMAND` / `ROBINREACH_API_KEY` at the operator's servers. `.mcp.json` is the pack-level tool wiring — not another workflow.

## Gate 1

User: `Run my brand`

Brand OS searches Notion + `knowledge/` + current relevant information and returns ~5 numbered topics. User replies `2, 3, 5`. That is the entire Gate 1 mechanism.

Then: Researcher → Writer → Editor → unpublished RobinReach drafts.

## Gate 2

Brand OS: `N drafts ready` plus RobinReach IDs.

User: `Publish {id} tomorrow at 8 AM`

Only that ID is scheduled/published.

## Not in this pack

Audience Analyst, Hook Master, Content Director, Claims Guard, Performance Analyst, Content Planner. Writer does audience + five hooks. Editor challenges the hook. RobinReach owns post state. Notion is search.
