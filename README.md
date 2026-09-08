# Claude Code workflow

A gated multi-agent build pipeline, plus the commands that surround it. Installable
as a plugin or by copying two directories.

## Commands

| Command | What it does |
|---|---|
| `/master <task>` | Runs the full pipeline, judging each stage before the next and recording the run |
| `/scaffold <project>` | Starts a new project with the foundations already in — env config, error pages, page shell, `robots.txt` |
| `/debug <symptom>` | Finds a root cause by reproducing and narrowing, rather than guessing at fixes |
| `/launch-check` | Audits a project for the once-per-project standards that no single task owns |

## Agents

| Agent | Role |
|---|---|
| `planner` | Designs the approach against the real code. Writes none of it. |
| `implementer` | Executes the plan, stays in scope, reports deviations rather than forcing them |
| `refactorer` | Changes structure while holding behavior constant, with characterization tests as the net |
| `tester` | Tries to break it. Never edits production code to go green. |
| `reviewer` | Explains the change first, then critiques it, ranked by severity |

`/master` routes to `implementer` when behavior changes and `refactorer` when it must not.
Never both in one pass — a diff that moves code *and* changes what it does is the diff
nobody can review.

## Install

As a plugin:

```
/plugin marketplace add rakuu-exe/claude-workflow
/plugin install claude-workflow@rakuu-workflow
```

Or by hand:

```sh
git clone https://github.com/rakuu-exe/claude-workflow.git ~/claude-workflow
cp -r ~/claude-workflow/agents ~/claude-workflow/commands ~/.claude/
```

Restart Claude Code either way, so the commands register.

## Where standards live

Web and product standards are placed by **cadence**, never as one checklist injected
everywhere — a global rulebook contradicts "size the plan to the task" and leaks cookie
banners into CLI bugfixes.

| Cadence | Handled by |
|---|---|
| Once per project | `/scaffold` creates them; `/launch-check` audits them |
| Per change | The gated surface scan in `reviewer.md`, which fires only on the file kinds the diff touches |
| Design-time | One principle in `planner.md` — name what crosses a boundary — that no-ops on refactors |

## Worklog

`/master` appends to `.claude/worklog.md` in whatever project it runs in: the approach
and the rejected alternative, verification numbers, what was left undone, and what risk
was carried forward. Git records what changed; this records what was decided and what
was knowingly skipped. That file belongs to the project, not to this repo.

## What this repo deliberately does not contain

It lives inside `~/.claude`, which also holds credentials, session transcripts, and
telemetry. `.gitignore` therefore denies everything by default and un-ignores only
`agents/*.md`, `commands/*.md`, and the plugin manifests. `settings.json` is excluded on
purpose — its `env` block is a common place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.
