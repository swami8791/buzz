# Nehal Brand OS

This directory documents the personal-brand operating system built on top of Buzz and RobinReach.

## Goal

Create a system where agents do roughly 99% of the research, topic development, writing, editing, fact-checking, repurposing, and draft preparation, while Nehal retains editorial control over what ideas get developed and explicit control over anything that is scheduled or published.

## Positioning

Primary positioning:

> Founder building high-stakes startups across AI, data, and real-world systems

Healthcare is proof of operating rigor and experience, not the limit of the brand.

## Core workflow

The intended production workflow is:

1. Brand Researcher
2. Audience Analyst
3. Content Director
4. Hook Master
5. Main Ghostwriter
6. Claims Guard
7. Cynical Editor
8. RobinReach Draft
9. Nehal review and explicit post-specific approval
10. Scheduling/publishing only after explicit approval

The Brand OS is exposed in Buzz as a single user-facing agent. Internal agents stay behind the scenes.

## Executive interface

The user-facing command is:

`Run my brand`

The command should first produce an editorial slate for Nehal to choose from, not immediately decide Nehal's public narrative on its own.

Recommended interaction:

1. Brand OS researches source material, audience fit, recent performance, and content gaps.
2. Brand OS returns 5-8 editorial concepts with rationale.
3. Nehal selects the ideas to pursue.
4. Internal agents produce, fact-check, edit, and create unpublished RobinReach drafts.
5. Nehal reviews the drafts.
6. Scheduling or publishing requires explicit approval for a specific post ID.

## Safety model

The system is in DRAFT-ONLY mode by default.

Allowed without approval:

- research
- audience analysis
- topic generation
- hook development
- writing
- editing
- claims validation
- performance analysis
- recommended posting times
- creation of unpublished RobinReach drafts

Not allowed without explicit post-specific approval:

- scheduling
- rescheduling
- publishing
- deleting published/scheduled content

Examples of valid approval:

- `Approve post 933403`
- `Schedule post 933403 for Tuesday at 8:00 AM CT`
- `Publish post 933403`

Generic phrases like `Run my brand`, `continue`, or `approved` without a post ID are not sufficient permission.

## Current integrations

- Buzz Desktop: user-facing Brand OS interface
- buzz-acp: agent runtime bridge
- Codex: agent runtime
- RobinReach MCP: draft creation, account metadata, analytics, and posting infrastructure
- Notion: long-term source library for media, press releases, blog posts, case studies, publications, speaking history, projects, accomplishments, and related source material

## Current production state

Brand OS has successfully completed a live Buzz -> Brand OS -> RobinReach flow and created six unpublished RobinReach drafts while keeping:

- `SCHEDULED: 0`
- `PUBLISHED: 0`

The next product change is editorial-control-first behavior: Brand OS should present content concepts for approval before drafting them.