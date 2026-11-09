# Claude Code workflow

A Claude Code plugin: vetted community skills, one skill of my own, and the design plugins
and MCP servers they work with. One install sets up all of it.

## Install

```
/plugin marketplace add rakuu-exe/claude-workflow
/plugin install claude-workflow@rakuu-workflow
```

That one install brings the skills below, impeccable and taste-skill, and the Playwright
and Knip MCP servers. It needs Node.js on `PATH` (for `npx`) and Chrome (for Playwright and
taste-skill's checker).

Or by hand, without the dependencies and MCP servers:

```sh
git clone https://github.com/rakuu-exe/claude-workflow.git ~/claude-workflow
cp -r ~/claude-workflow/skills ~/.claude/
```

Restart Claude Code either way, so the skills register.

`claude plugin validate` reports the name `claude-workflow` as reserved, because it starts
with `claude-`. Installing and loading still work. Renaming the plugin would change the
install id and the `claude-workflow:` prefix on every skill.

## Skills

Community skills, copied unchanged from upstream at a pinned commit, plus one of this
repo's own. Sources, commits and licenses are in [`skills/THIRD_PARTY.md`](skills/THIRD_PARTY.md).
Claude loads each one on its own when the task matches its description.

### Engineering

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

### Design and motion (Emil Kowalski)

| Skill | Use it for |
|---|---|
| `emil-design-eng` | UI polish and the small details that make an interface feel right |
| `animate`, `choreograph` | Building one animation, or several elements moving together |
| `review-animations`, `improve-animations` | Reviewing motion code, or auditing a codebase's motion with a plan |
| `find-animation-opportunities`, `remove-animations` | Finding where motion is missing, or where it should go |
| `animation-performance`, `animation-vocabulary` | Keeping animations in the frame budget; naming a vaguely described effect |
| `gestures`, `apple-design` | Drag, swipe and sheet interactions; spring physics and fluid motion |
| `break-ui` | Stress-testing UI with worst-case data |
| `prototype`, `pick-ui-library` | Several variants behind a live picker; choosing a library for a task |
| `mobile-native` | Web apps that feel native on phones |

`review-animations`, `prototype` and `pick-ui-library` are slash commands only. Upstream sets
`disable-model-invocation: true` on them, so Claude never starts them unprompted.

### Project state

| Skill | Use it for |
|---|---|
| `project-tracker` | Keeping `docs/PROJECT-TRACKER.md`, `docs/IMPLEMENTED.md` and `docs/HANDOFF.md` current, so the next person or agent can pick the project up cold |

`project-tracker` is this repo's own skill. IDs are permanent and typed (`F` feature, `B` bug,
`C` internal change), status is a separate column, and nothing is marked done without a
verification that actually ran.

### Pulled in by the plugin

Installing the plugin also installs **impeccable** and **taste-skill** as dependencies,
fetched from their own repos, and starts two MCP servers from `.mcp.json`: **Playwright**
(a real browser) and **Knip** (unused files, exports and dependencies, used by
`configure-knip`). Sources are in
[`skills/THIRD_PARTY.md`](skills/THIRD_PARTY.md#pulled-in-by-the-plugin-not-copied).

## What this repo deliberately does not contain

It's built to live inside `~/.claude`, which also holds credentials, session transcripts and
telemetry. `.gitignore` therefore denies everything by default and un-ignores only the plugin
manifests, `.mcp.json`, and each skill folder by name. Skills are listed one by one rather
than as `skills/**`, because `~/.claude/skills/synced/` holds claude.ai's own synced skills
and their manifest. `settings.json` is excluded on purpose, since its `env` block is a common
place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.
