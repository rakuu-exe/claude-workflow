# Claude Code workflow

A Claude Code plugin that installs four community plugins in full and starts two MCP
servers. One install sets up all of it. The repo holds no skills of its own.

## Install

```
/plugin marketplace add rakuu-exe/claude-workflow
/plugin install rakuu@rakuu-workflow
```

That one install brings every plugin in the table below and the Playwright and Figma MCP
servers. It needs Node.js on `PATH` (for `npx`) and Chrome (for Playwright and taste-skill's
checker). Figma asks you to sign in the first time it is used. Restart Claude Code
afterwards.

The plugin was called `claude-workflow` until 2.0.0. That name is reserved, so it is now
`rakuu`. An install of the old name has to be removed and installed again under the new one.

## Plugins installed with it

Each one is installed whole from its own repository, unchanged. Skills carry the plugin's
name as a prefix, so Emil's `animate` is `emil:animate`. Sources, pinned commits and
licenses are in [`THIRD_PARTY.md`](THIRD_PARTY.md).

| Plugin | What it brings |
|---|---|
| `emil` | Emil Kowalski's design engineering skills: animation, choreography, gestures, performance, UI polish |
| `impeccable` | Paul Bakaus's design skill: critique, audit and polish |
| `taste-skill` | Leonxlnx's skill for whole websites and landing pages |
| `superpowers` | Jesse Vincent's skills: debugging, TDD, brainstorming, planning, verification |

Four of Emil's skills are slash commands only (`review-animations`, `prototype`,
`pick-ui-library`, `learn-taste`). Upstream sets `disable-model-invocation: true` on them,
so Claude never starts them unprompted.

## MCP servers

Started from `.mcp.json`: **Playwright** (a real browser) and **Figma** (reads designs and
their variables). Figma is a remote server, so no token is stored here.

## What changed in 3.0.0

Until 3.0.0 the plugin also carried a lead output style, five agents, three skills of its
own, five more plugins (`agent-skills`, `backend-development`, `security-audit`, `webpro`,
`simplify-codebase`) and the Knip and Context7 MCP servers. All of that was removed. The
git history still has it.

Updating from 2.0.0 does not remove the five dropped plugins from a machine that already
has them. Uninstall each one with `/plugin uninstall <name>@rakuu-workflow`.

## What this repo deliberately does not contain

It's built to live inside `~/.claude`, which also holds credentials, session transcripts and
telemetry. `.gitignore` therefore denies everything by default and un-ignores only the plugin
manifests, `.mcp.json`, this README and `THIRD_PARTY.md`. `settings.json` is excluded on
purpose, since its `env` block is a common place for API keys.

Before adding a `!` line to `.gitignore`, ask whether that path can ever hold a secret.
