# Third-party skills

Every skill in this directory is copied unchanged from its upstream repository at the
commit below. Each skill folder carries its upstream `LICENSE`. To update one, re-copy
it from upstream and bump the commit here; don't edit the copy in place, or the next
update will silently overwrite the change.

| Skill | Upstream | Path | Commit | License |
|---|---|---|---|---|
| `systematic-debugging` | [obra/superpowers](https://github.com/obra/superpowers) | `skills/systematic-debugging` | `22f0b463e7a5` | MIT |
| `security-audit` | [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | `skills/security-audit` | `c1c8a8c14710` | MIT |
| `code-review-and-quality` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | `skills/code-review-and-quality` | `301b02b12bff` | MIT |
| `code-simplification` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | `skills/code-simplification` | `301b02b12bff` | MIT |
| `simplify-codebase` | [tt-a1i/simplify-codebase](https://github.com/tt-a1i/simplify-codebase) | `SKILL.md`, `references/`, `visualization/` | `5da55efcb52d` | MIT |
| `configure-knip` | [webpro/skills](https://github.com/webpro/skills) | `skills/configure-knip` | `30e66c946d87` | ISC |
| `clean-git-repo` | [webpro/skills](https://github.com/webpro/skills) | `skills/clean-git-repo` | `30e66c946d87` | ISC |
| `api-design-principles` | [wshobson/agents](https://github.com/wshobson/agents) | `plugins/backend-development/skills/api-design-principles` | `9c61ab243def` | MIT |
| `architecture-patterns` | [wshobson/agents](https://github.com/wshobson/agents) | `plugins/backend-development/skills/architecture-patterns` | `9c61ab243def` | MIT |
| 18 design-engineering skills (see the README's Design section) | [emilkowalski/skills](https://github.com/emilkowalski/skills) | `skills/*` | `715c1807e08c` | MIT |

`project-tracker` is this repo's own skill, not third-party.

## Installed separately, not copied

These ship hooks, agents, binaries or large assets and update often, so they're installed from their own sources rather than vendored here:

| What | Install | License |
|---|---|---|
| [impeccable](https://github.com/pbakaus/impeccable) | `claude plugin marketplace add pbakaus/impeccable` then `claude plugin install impeccable@impeccable` | Apache-2.0 |
| [taste-skill](https://github.com/Leonxlnx/taste-skill) | `claude plugin marketplace add Leonxlnx/taste-skill` then `claude plugin install taste-skill@taste-skill` | MIT |
| [Playwright MCP](https://github.com/microsoft/playwright-mcp) | `claude mcp add playwright -s user -- cmd /c npx -y @playwright/mcp@0.0.84` (drop `cmd /c` on macOS/Linux) | Apache-2.0 |

## Considered and left out

- `netresearch/security-audit-skill` is PHP/TYPO3-focused, and `security-audit` above covers the general case.
- `code-yeongyu/oh-my-openagent` `remove-deadcode` is hard-wired to that project's own `src/`, Bun and OpenCode-only tools, so it doesn't run in Claude Code. `configure-knip` (by Knip's author) does that job for JS/TS.
- `garrytan/gstack` is a whole toolkit rather than a skill. It needs Bun, registers hooks, auto-updates every session, and replaces the browser tooling, so it belongs in a separate install, not copied here.
