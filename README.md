# Claude Code workflow

Agent definitions and slash commands for a Planner → Implementer → Tester → Reviewer
pipeline, plus a pre-launch project audit.

## Contents

| File | Role |
|---|---|
| `commands/master.md` | `/master <task>` — runs the full pipeline, gates each stage, records the run |
| `commands/launch-check.md` | `/launch-check` — once-per-project audit before a site goes live |
| `agents/planner.md` | Designs the approach. Writes no code. |
| `agents/implementer.md` | Executes the plan, stays in scope, reports deviations. |
| `agents/tester.md` | Tries to break it. Never edits production code to go green. |
| `agents/reviewer.md` | Explains the change, then critiques it, ranked by severity. |

## Install on another machine

```sh
git clone git@github.com:<you>/<repo>.git ~/.claude-workflow
cp -r ~/.claude-workflow/agents ~/.claude-workflow/commands ~/.claude/
```

Restart Claude Code so the commands register.

## What this repo deliberately does not contain

It lives inside `~/.claude`, which also holds credentials, session transcripts,
and telemetry. `.gitignore` therefore denies everything by default and un-ignores
only `agents/*.md` and `commands/*.md`. `settings.json` is excluded on purpose —
its `env` block is a common place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.

## Worklog

`/master` appends to `.claude/worklog.md` in whatever project it runs in — the
decisions and the residue (what was rejected, what was left undone, what risk was
carried forward), which neither git history nor the transcript records. That file
belongs to the project, not to this repo.
