---
name: setup
description: "Build or update the candidate profile in the ai-job-search checkout. Command: /setup."
---

# /setup

Load and follow `.claude/commands/setup.md` in the `ai-job-search` checkout.

That file is the source of truth: Path A (documents folder), Path B (paste a CV), Path C (interview). This skill does not replace it.

## Buzz overlay

1. Confirm you are in the `ai-job-search` checkout before writing profile files.
2. Wait for the user to pick a path. Do not invent a profile from the Buzz channel history.
3. After setup, tell them to run `/scrape` or `/apply <job url>` in this same channel.
4. Do not start scraping or drafting until they issue that command.
