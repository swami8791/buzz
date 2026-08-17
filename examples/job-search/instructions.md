# Job Search pack rules

One user-facing Buzz agent. No Researcher, Writer, Editor, or other workers.

The project is a checkout of [ai-job-search](https://github.com/swami8791/ai-job-search). Canonical workflows live there under `.claude/commands/` and `.claude/skills/`. Do not duplicate them here. Do not invent a state machine.

## Commands

`/setup`, `/scrape`, `/apply <job url>` (or pasted posting). That is the whole surface.

## Draft-only

`/apply` writes a tailored LaTeX CV and cover letter and stops. Tracker status stays `drafted`.

Never submit an application, never send email, never click Apply on a portal, never call `/outcome` to mark `applied` unless the user explicitly says they already submitted it themselves.

Telegram is not part of this pack. Buzz is the conversation.
