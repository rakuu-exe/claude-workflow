# Third-party plugins

Nothing third-party is copied into this repo. Each plugin below is installed whole from its
own repository, as a dependency of `rakuu`, through an entry in
[`.claude-plugin/marketplace.json`](../.claude-plugin/marketplace.json). The three skills in
this directory (`design-language`, `code-style`, `project-tracker`) are this repo's own.

| Plugin | Upstream | Pinned commit | License |
|---|---|---|---|
| `emil` | [emilkowalski/skills](https://github.com/emilkowalski/skills) | `f7ce8c02d6e3` | MIT |
| `superpowers` | [obra/superpowers](https://github.com/obra/superpowers) | `22f0b463e7a5` | MIT |
| `agent-skills` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | `301b02b12bff` | MIT |
| `backend-development` | [wshobson/agents](https://github.com/wshobson/agents), `plugins/backend-development` | `9c61ab243def` | MIT |
| `security-audit` | [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill) | `c1c8a8c14710` | MIT |
| `webpro` | [webpro/skills](https://github.com/webpro/skills) | `30e66c946d87` | ISC |
| `simplify-codebase` | [tt-a1i/simplify-codebase](https://github.com/tt-a1i/simplify-codebase) | `5da55efcb52d` | MIT |
| `impeccable` | [pbakaus/impeccable](https://github.com/pbakaus/impeccable), `plugin/` | not pinned, follows upstream | Apache-2.0 |
| `taste-skill` | [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill) | not pinned, follows upstream | MIT |

To update a pinned plugin, read what changed upstream, then replace its `sha` in
`marketplace.json` with the new full commit hash. Superpowers and impeccable run a hook at
session start, so their updates deserve a look before the pin moves.

The sources use full `https://` URLs on purpose. The `owner/repo` shorthand clones over SSH, which fails on a machine with no SSH key for GitHub.

## MCP servers

| Server | How the plugin gets it | License |
|---|---|---|
| [Playwright MCP](https://github.com/microsoft/playwright-mcp) | `.mcp.json`, `@playwright/mcp@0.0.84` via npx | Apache-2.0 |
| [Knip MCP](https://knip.dev) | `.mcp.json`, `@knip/mcp@0.0.37` via npx, for `webpro:configure-knip` | ISC |
| [Figma MCP](https://mcp.figma.com/mcp) | `.mcp.json`, Figma's remote server; signs in with your Figma account | Figma's terms |
| [Context7 MCP](https://context7.com) | `.mcp.json`, remote server for current library docs | Context7's terms |

## Considered and left out

- `netresearch/security-audit-skill` is PHP/TYPO3-focused, and `security-audit` above covers the general case.
- `code-yeongyu/oh-my-openagent` `remove-deadcode` is hard-wired to that project's own `src/`, Bun and OpenCode-only tools, so it doesn't run in Claude Code. `webpro:configure-knip` (by Knip's author) does that job for JS/TS.
- `garrytan/gstack` is a whole toolkit rather than a skill. It needs Bun, registers hooks, auto-updates every session, and replaces the browser tooling, so it belongs in a separate install.
