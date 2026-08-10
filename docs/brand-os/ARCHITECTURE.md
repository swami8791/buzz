# Brand OS Architecture

## System boundary

Buzz is the executive interface, not the content database and not the publishing system.

RobinReach is the publishing/draft/analytics infrastructure.

Notion is the long-term source library and content memory.

The Brand OS orchestration layer coordinates internal agents and tools while presenting one simple Buzz-facing agent to Nehal.

## High-level architecture

```text
Nehal
  |
  v
Buzz Desktop
  |
  v
Brand OS
  |
  +--> Notion source library
  +--> RobinReach analytics
  +--> Brand Knowledge Base
  |
  v
Research / Audience / Editorial planning
  |
  v
Nehal topic selection
  |
  v
Hook Master -> Main Ghostwriter -> Claims Guard -> Cynical Editor
  |
  v
RobinReach unpublished draft
  |
  v
Nehal post-specific approval
  |
  v
Schedule / Publish
```

## Internal agents

### Brand Researcher

Purpose:

- discover source material
- verify claims
- identify stories, accomplishments, lessons, projects, research, grants, speaking, and company history
- maintain source provenance

Source priority:

1. Nehal-provided material
2. Verified Brand Knowledge Base
3. Notion source databases
4. Primary public sources
5. Nehal's public profiles/content
6. Reputable secondary sources

Claims can be marked VERIFIED, LIKELY, UNVERIFIED, or CONFLICTING. Only VERIFIED claims may flow automatically into public content.

### Audience Analyst

Purpose:

- determine who should care about an idea
- identify audience tension, relevance, objections, and likely value
- prevent content from being internally interesting but externally irrelevant

### Content Director

Purpose:

- maintain content range
- prevent topic repetition
- propose editorial concepts
- explain why each concept matters for Nehal's positioning

It should not unilaterally determine Nehal's public narrative. It should return an editorial slate for approval.

### Hook Master

Purpose:

- turn approved ideas into strong angles
- generate several hook options
- recommend the strongest framing
- avoid generic influencer hooks and empty contrarianism

### Main Ghostwriter

Purpose:

- write in Nehal's voice
- ground posts in approved source material and angle
- avoid invented experiences or unsupported claims
- keep the writing operator-first, human, direct, and credible

### Claims Guard

Purpose:

- validate specific personal claims against the Brand Knowledge Base and source records
- block unsupported metrics, company claims, awards, customer names, funding, outcomes, and historical assertions

### Cynical Editor

Purpose:

- reject generic AI copy
- reject corporate language, fake vulnerability, motivational fluff, obvious AI phrasing, weak hooks, overclaiming, repetition, and excessive hashtags
- enforce brand positioning and natural voice

Quality threshold used in the existing system: editor score >= 85 before a piece may become a RobinReach draft.

### Performance Analyst

Purpose:

- read RobinReach analytics
- learn from repeated evidence, not one-off performance
- avoid engagement bait
- feed useful patterns back into editorial planning

### Content Planner

Purpose:

- maintain a rolling content calendar
- recommend times and cadence
- never convert recommendations into scheduled/public posts without explicit post-specific approval

## Brand Knowledge Base

Existing local knowledge-base structure:

- `brand/PROFILE.md`
- `brand/VOICE.md`
- `brand/CLAIMS.md`
- `brand/CONTENT-PILLARS.md`
- `brand/SOURCES.md`
- `brand/RESEARCH-QUEUE.md`
- `brand/PERFORMANCE.md`
- `brand/CONTENT-CALENDAR.md`

Content pillars:

- BUILDING
- OPERATOR
- PROOF
- PERSPECTIVE

Healthcare should appear as evidence and experience but must not dominate simply because more historical healthcare material exists.

## Tool boundaries

### Buzz

Use for:

- direct conversation with Brand OS
- topic review and selection
- draft review commands
- status
- explicit approvals

### RobinReach

Use for:

- account/profile discovery
- analytics
- best-time recommendations
- post validation
- unpublished draft creation
- scheduling/publishing only after explicit approval

### Notion

Use for:

- media library
- press releases
- blog posts and essays
- case studies
- publications and research
- speaking/teaching history
- founder/company history
- current projects
- verified accomplishments and source material

## Editorial-control principle

Agents should do 99% of the work, but Nehal should retain two human gates:

1. Editorial direction: choose which proposed ideas represent him.
2. Public action: explicitly approve a specific draft before it can be scheduled or published.

This prevents the system from deciding both what Nehal believes and what gets publicly posted.