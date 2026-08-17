---
name: scrape
description: "Search job portals from the ai-job-search profile and present matches. Command: /scrape."
---

# /scrape

Load and follow `.claude/skills/job-scraper/SKILL.md` in the `ai-job-search` checkout.

That file is the source of truth (portal CLIs under `.agents/skills/`, dedup, fit preview). This skill does not replace it.

## Buzz overlay

1. Profile must already exist (`CLAUDE.md` is not still placeholders). If not, tell the user to run `/setup` first.
2. Present matches in the Buzz channel. Do not start `/apply` until they pick a URL or paste a posting.
3. Scraping is search only. It does not apply to jobs.
