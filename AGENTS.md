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

### Adding labels to PRs

The default `gh` CLI token (`ghs_*`) in Cursor Cloud is **read-only** for issues/PRs. To add labels, you need a GitHub PAT with `issues:write` or `pull_requests:write` permission, provided via the `GH_PAT_LABELS` secret.

To add a label using the PAT:
```bash
gh api -X POST "repos/{owner}/{repo}/issues/{pr_number}/labels" \
  --header "Authorization: token $GH_PAT_LABELS" \
  -f "labels[]=label-name"
```

If `GH_PAT_LABELS` is not set, label operations will fail with 403. Ask the user to add the secret.
