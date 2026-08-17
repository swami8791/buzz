# Job Search

One Buzz agent that ports the [ai-job-search](https://github.com/swami8791/ai-job-search) CV-tailor flow. Telegram is not required.

```text
/setup          /scrape              /apply <url>
  |                |                     |
  v                v                     v
Profile         Job matches          Tailored LaTeX
in checkout     (optional)           CV + cover letter
                                     (draft only)
```

This is a CV tailor, not a blank resume form. `/apply` never submits an application.

Runtime is buzz-acp + Codex or Claude Code — the same ACP path as Brand OS, with **one** persona and no workers.

## Validate

```bash
buzz pack validate ./examples/job-search
buzz pack inspect ./examples/job-search
```

## Attach in Buzz Desktop

Desktop import does not load this pack directory. Recreate the one persona from `buzz pack inspect` by hand.

1. Clone the project (once):

   ```bash
   git clone https://github.com/swami8791/ai-job-search.git
   ```

   Put that checkout where the agent can see it: the nest `REPOS/` directory, or a community repos-dir that already points at your working copies. Follow ai-job-search `SETUP.md` for Python, bun, and LaTeX if you want compiled PDFs.

2. In Buzz Desktop, create **one** agent named Job Search. Paste the inspect output (name, instructions, keywords `/setup` `/scrape` `/apply`, the three skills). Use Codex or Claude Code as the harness.

3. Attach that agent to a channel. Mentions and the slash-command keywords both trigger it.

4. In the channel:

   ```text
   /setup
   ```

   Pick Path A (documents folder), B (paste a CV), or C (interview). Wait until it says setup is complete.

   ```text
   /scrape
   ```

   Optional. Then pick a posting.

   ```text
   /apply https://example.com/jobs/123
   ```

   Review the drafted CV and cover letter in the checkout. Submit yourself if you want to. The agent will not.

## Not in this pack

Researcher / Writer / Editor, Notion pipelines, RobinReach, Brand OS, Telegram, or a job-application state machine. Extra ai-job-search commands (`/interview`, `/rank`, `/outcome`, …) stay in that repo; this pack only exposes `/setup`, `/scrape`, and `/apply`.
