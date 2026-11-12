# Third-party plugins

Nothing third-party is copied into this repo. Each plugin below is installed whole from its
own repository, as a dependency of `rakuu`, through an entry in
[`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json).

| Plugin | Upstream | Pinned commit | License |
|---|---|---|---|
| `emil` | [emilkowalski/skills](https://github.com/emilkowalski/skills) | `f7ce8c02d6e3` | MIT |
| `superpowers` | [obra/superpowers](https://github.com/obra/superpowers) | `22f0b463e7a5` | MIT |
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
| [Figma MCP](https://mcp.figma.com/mcp) | `.mcp.json`, Figma's remote server; signs in with your Figma account | Figma's terms |
