# Claude Code workflow

A gated multi-agent build pipeline, the commands that surround it, and a set of vetted
community skills. Installable as a plugin or by copying three directories.

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

## Skills

Community skills, copied unchanged from upstream at a pinned commit. Sources, commits
and licenses are in [`skills/THIRD_PARTY.md`](skills/THIRD_PARTY.md). Claude loads each
one on its own when the task matches its description.

| Skill | Use it for | From |
|---|---|---|
| `systematic-debugging` | Any bug or failing test: reproduce, trace the root cause, then fix | obra/superpowers |
| `code-review-and-quality` | Reviewing a diff or PR across correctness, design, security and tests | addyosmani/agent-skills |
| `security-audit` | Security questions and focused reviews; a full multi-agent audit only when asked | cloudflare/security-audit-skill |
| `code-simplification` | Making working code clearer without changing behavior | addyosmani/agent-skills |
| `simplify-codebase` | Proving and removing dead code, duplicate state and needless layers | tt-a1i/simplify-codebase |
| `configure-knip` | Unused files, exports and dependencies in JS/TS, via Knip | webpro/skills |
| `clean-git-repo` | Pruning merged and stale branches, worktrees and tags (dry run first) | webpro/skills |
| `api-design-principles` | Designing or reviewing REST and GraphQL APIs | wshobson/agents |
| `architecture-patterns` | Backend structure: layers, boundaries, dependency direction | wshobson/agents |

`/debug` and `systematic-debugging` overlap on purpose. The command is the entry point
you type, and the skill is what Claude reaches for when a bug shows up mid-task.
`/launch-check` audits once-per-project standards, and `security-audit` looks for
vulnerabilities, so they don't replace each other.

## Install

As a plugin:

```
/plugin marketplace add rakuu-exe/claude-workflow
/plugin install claude-workflow@rakuu-workflow
```

Or by hand:

```sh
git clone https://github.com/rakuu-exe/claude-workflow.git ~/claude-workflow
cp -r ~/claude-workflow/agents ~/claude-workflow/commands ~/claude-workflow/skills ~/.claude/
```

Restart Claude Code either way, so the commands and skills register.

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
`agents/*.md`, `commands/*.md`, the plugin manifests, and each skill folder by name.
Skills are listed one by one rather than as `skills/**`, because `~/.claude/skills/synced/`
holds claude.ai's own synced skills and their manifest. `settings.json` is excluded on
purpose — its `env` block is a common place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.
