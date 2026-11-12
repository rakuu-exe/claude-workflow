# Claude Code workflow

A Claude Code plugin that turns Claude into a lead: it talks the work through with you,
plans it, hands it to a team of agents and checks what comes back. The agents work with
nine community plugins, installed in full, three skills of my own, and four MCP servers.
One install sets up all of it.

## Install

```
/plugin marketplace add rakuu-exe/claude-workflow
/plugin install rakuu@rakuu-workflow
```

That one install brings the lead, the agents, my own skills, every plugin in the table
below, and the Playwright, Knip, Figma and Context7 MCP servers. It needs Node.js on `PATH`
(for `npx`) and Chrome (for Playwright and taste-skill's checker). Figma asks you to sign in
the first time it is used. Restart Claude Code afterwards.

The plugin was called `claude-workflow` until 2.0.0. That name is reserved, so it is now
`rakuu`. An install of the old name has to be removed and installed again under the new one.

## How it works

You talk to the lead. It is an output style (`output-styles/lead.md`) that turns on with
the plugin, so there is nothing to start.

1. **Discuss.** The lead settles what you want, and for UI agrees the look with you first.
2. **Plan.** It lists the tasks and which agent takes each.
3. **Dispatch.** Each agent gets a written brief and works in its own context.
4. **Review.** The reviewer checks the result against the brief, then for quality.
5. **Report.** The lead tells you what was built and what was checked.

| Agent | Job | Skills loaded at start |
|---|---|---|
| `scout` | Finds files and code. Read-only, runs on Haiku | none |
| `researcher` | Web and docs research, with sources. Runs on Sonnet | none |
| `frontend` | Builds UI and motion | `design-language`, `code-style`, `emil-design-eng`, `animate` |
| `backend` | Builds APIs and server code | `code-style`, `api-design-principles`, `architecture-patterns` |
| `reviewer` | Checks the work, cannot edit | `code-review-and-quality`, `code-style` |

Each agent file also carries a table of the other skills in its field and when to load
them, and every agent can use the MCP servers. To work without the lead, run
`/output-style default`.

## This repo's own skills

| Skill | Use it for |
|---|---|
| `design-language` | My visual taste: minimal black and white UI, the spacing scale, and the motion numbers that win over the other design skills |
| `code-style` | My code rules: simple, reusable, few comments, documented in `docs/` instead |
| `project-tracker` | Keeping `docs/PROJECT-TRACKER.md`, `docs/IMPLEMENTED.md` and `docs/HANDOFF.md` current, so the next person or agent can pick the project up cold |

## Plugins installed with it

Each one is installed whole from its own repository, not copied in pieces. Skills carry the
plugin's name as a prefix, so Emil's `animate` is `emil:animate`. Sources, pinned commits
and licenses are in [`skills/THIRD_PARTY.md`](skills/THIRD_PARTY.md).

| Plugin | What it brings |
|---|---|
| `emil` | Emil Kowalski's design engineering skills: animation, choreography, gestures, performance, UI polish |
| `impeccable` | Paul Bakaus's design skill: critique, audit and polish |
| `taste-skill` | Leonxlnx's skill for whole websites and landing pages |
| `superpowers` | Jesse Vincent's skills: debugging, TDD, brainstorming, planning, verification |
| `agent-skills` | Addy Osmani's engineering skills from spec to ship, with review agents |
| `backend-development` | Seth Hobson's API design and architecture skills, with backend agents |
| `security-audit` | Cloudflare's security guidance and audits |
| `webpro` | Lars Kappert's skills: Knip setup, git cleanup, JavaScript optimization, prose review |
| `simplify-codebase` | tt-a1i's skill for proving and removing dead code |

Four of Emil's skills are slash commands only (`review-animations`, `prototype`,
`pick-ui-library`, `learn-taste`). Upstream sets `disable-model-invocation: true` on them,
so Claude never starts them unprompted.

Together the plugins hold more skills than Claude Code's skill listing has room for, so it
shortens their descriptions. The lead and the agents name the skills they need, which does
not depend on the listing. To give the listing more room, raise
`skillListingBudgetFraction` in your settings, or turn off skills you never use with
`/skills`.

## MCP servers

Started from `.mcp.json`: **Playwright** (a real browser), **Knip** (unused files, exports
and dependencies), **Figma** (reads designs and their variables) and **Context7** (current
library docs). Figma and Context7 are remote servers, so no token is stored here.

## What this repo deliberately does not contain

It's built to live inside `~/.claude`, which also holds credentials, session transcripts and
telemetry. `.gitignore` therefore denies everything by default and un-ignores only the plugin
manifests, `.mcp.json`, `output-styles/`, `agents/`, and each skill folder by name. Skills
are listed one by one rather than as `skills/**`, because `~/.claude/skills/synced/` holds
claude.ai's own synced skills and their manifest. `settings.json` is excluded on purpose,
since its `env` block is a common place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.
