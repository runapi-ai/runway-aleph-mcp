<h1 align="center">RunAPI Runway Aleph MCP Server</h1>

<p align="center">
  <strong>Runway Aleph historical task access for AI agents: query existing tasks through one focused MCP server.</strong>
</p>

<p align="center">
  <sub>Works with Claude Code, Codex, Cursor, Windsurf, VS Code, Roo Code, and any MCP-compatible host.</sub>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@runapi.ai/runway-aleph-mcp"><img src="https://img.shields.io/npm/v/%40runapi.ai/runway-aleph-mcp?style=flat-square&color=blue" alt="npm version"></a>
  <a href="https://github.com/runapi-ai/runway-aleph-mcp"><img src="https://img.shields.io/badge/GitHub-runapi--ai%2Frunway--aleph--mcp-24292f?style=flat-square" alt="GitHub repository"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue?style=flat-square" alt="Apache-2.0 license"></a>
  <img src="https://img.shields.io/badge/Type-MCP_Server-blue?style=flat-square" alt="MCP Server">
  <img src="https://img.shields.io/badge/Models-0-16a34a?style=flat-square" alt="0 models">
</p>

<p align="center">
  <a href="#install">Install</a> |
  <a href="#tools">Tools</a> |
  <a href="#models">Models</a> |
  <a href="#agent-prompts">Agent Prompts</a> |
  <a href="#configuration">Configuration</a> |
  <a href="#links">Links</a>
</p>

---

## Why This Package?

`@runapi.ai/runway-aleph-mcp` is a focused Model Context Protocol server for the **Runway Aleph** model line on RunAPI.
It gives MCP-compatible assistants direct access to 0 endpoints and 0 model variants without loading the full RunAPI catalog.

Use this per-model server when an agent should stay scoped to Runway Aleph. Use [`@runapi.ai/mcp`](https://github.com/runapi-ai/mcp) when one assistant should discover every RunAPI model line.

`runway-aleph` was retired on 2026-10-11T00:00:00Z. New requests return HTTP 410 before task creation or balance deduction. Existing tasks can still be queried. This model ID is not mapped to another model.

---

## Install

Add it to Claude Code:

```bash
claude mcp add runway-aleph -s user -- npx -y @runapi.ai/runway-aleph-mcp
```

Use project scope when the server should be shared with a repository:

```bash
claude mcp add runway-aleph -s project -- npx -y @runapi.ai/runway-aleph-mcp
```

Codex, Cursor, Windsurf, VS Code, Roo Code, and other MCP hosts can use the same stdio command:

```json
{
  "mcpServers": {
    "runway-aleph": {
      "command": "npx",
      "args": ["-y", "@runapi.ai/runway-aleph-mcp"]
    }
  }
}
```

No models in this package accept new tasks. `check_pricing` returns no supported model. For historical task lookup, ask your assistant to call the `login` tool. It opens a browser login and saves credentials to `~/.config/runapi/config.json`, the same file used by `runapi login`.
Headless and CI hosts can still set `RUNAPI_API_KEY` before starting the MCP host.

Ready-made examples are in [`examples/`](examples/) for Claude, Cursor, Windsurf, VS Code, and Roo Code.

---

## Tools

| Tool | Auth | Purpose |
|---|---|---|

| `get_task` | Yes | Fetch the current status and latest payload for an existing task. |
| `check_pricing` | No | Returns no supported model because this model line is retired. |

---

## Models

Runway Aleph covers 0 model variants across 0 endpoints. Each tool accepts the models listed for it:

| Tool | Models |
|---|---|


Model availability can change between releases. Use `check_pricing` or the [Runway Aleph model page](https://runapi.ai/models/runway-aleph) for the current catalog view.

---

## Agent Prompts

Query an existing task with `get_task`. New requests for this retired model return HTTP 410.

```text
Check the status of my existing Runway Aleph task with RunAPI.
```

The assistant calls `get_task` with the task id and returns its status and available result.

---

## Configuration

The server resolves auth in this order:

1. `RUNAPI_API_KEY` environment variable, useful for headless and CI hosts
2. `~/.config/runapi/config.json`, created by the MCP `login` tool or `runapi login`
3. No key, which still allows `check_pricing`

The config file is normally managed by login. A pre-provisioned headless config can use:

```json
{
  "apiKey": "your_runapi_key"
}
```

Do not commit real API keys.

---

## Links

| Resource | URL |
|---|---|
| Runway Aleph model page | [https://runapi.ai/models/runway-aleph](https://runapi.ai/models/runway-aleph) |
| npm package | [@runapi.ai/runway-aleph-mcp](https://www.npmjs.com/package/@runapi.ai/runway-aleph-mcp) |
| GitHub repository | [runapi-ai/runway-aleph-mcp](https://github.com/runapi-ai/runway-aleph-mcp) |
| RunAPI MCP overview | [runapi.ai/mcp](https://runapi.ai/mcp) |
| RunAPI docs | [runapi.ai/docs](https://runapi.ai/docs) |

---

## License

Licensed under the [Apache License, Version 2.0](LICENSE).
