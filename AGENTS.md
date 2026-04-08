# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is the **Datadog Cursor Plugin** — a declarative Cursor IDE plugin that registers a remote Datadog MCP server. It contains no application code, no buildable artifacts, no dependencies, and no test suites.

### Repository structure

- `.cursor-plugin/plugin.json` — Cursor plugin manifest (name, version, description, keywords)
- `mcp.json` — MCP server configuration pointing to remote Datadog MCP endpoint
- `skills/datadog-mcp-setup/SKILL.md` — AI skill for guiding users through domain configuration
- `README.md` — User-facing documentation
- `LICENSE` / `NOTICE` — Apache 2.0 license files

### Key caveats

- **No build/lint/test commands exist.** There is no `package.json`, `Makefile`, or any build system. Validation is limited to checking JSON syntax of `mcp.json` and `plugin.json`.
- **No local server to run.** The MCP server is hosted remotely by Datadog. The plugin just provides configuration for Cursor to connect to it.
- **`mcp.json` contains a `${DD_MCP_DOMAIN}` placeholder** that must be replaced with a region-specific domain (e.g. `mcp.datadoghq.com` for US1) before the plugin can function. See `skills/datadog-mcp-setup/SKILL.md` for the full domain list.
- **JSON validation** can be performed with: `python3 -c "import json; json.load(open('mcp.json')); json.load(open('.cursor-plugin/plugin.json')); print('All JSON valid')"`
