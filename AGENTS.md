# Agents

## Cursor Cloud specific instructions

### Repository overview

This is the **Datadog Cursor Plugin** — a configuration-only Cursor IDE plugin (v0.5.0, Preview). It contains no source code, no build system, no tests, and no installable dependencies.

**Files:**
- `mcp.json` — MCP server config with a `${DD_MCP_DOMAIN}` placeholder URL
- `.cursor-plugin/plugin.json` — Plugin manifest (name, version, description)
- `skills/datadog-mcp-setup/SKILL.md` — AI agent skill for guiding users through domain setup
- `README.md`, `LICENSE`, `NOTICE` — Documentation and legal

### Key caveats

- There is **no build step, no linter, no test suite, and no package manager**. Validation is limited to checking JSON well-formedness.
- The `mcp.json` file contains a `${DD_MCP_DOMAIN}` placeholder. This is intentional for distribution — do not replace it unless a user requests domain configuration.
- The plugin connects to a **remote Datadog MCP server** via OAuth; there are no local services to start.
- End-to-end testing requires the Cursor IDE (v2.6.0+) and a Datadog account — neither can be replicated in a headless cloud VM.

### Validating changes

Since there are no automated tests, validate changes by:
1. Checking JSON validity: `python3 -c "import json; json.load(open('mcp.json')); print('OK')"`
2. Checking plugin manifest: `python3 -c "import json; json.load(open('.cursor-plugin/plugin.json')); print('OK')"`
3. Reviewing Markdown rendering for documentation changes.
