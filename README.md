# archolith-audit — Claude Code Plugin

Live MCP token usage audit for Claude Code sessions. Tracks per-server token spend and waste patterns in real time.

## Install

### From GitHub (recommended)

```
/install-plugin github:archolith/archolith-audit-plugin-claude
```

Claude Code clones the plugin, registers the MCP server, and activates the hooks.
No `pip install` needed — the Python package is bundled inside the plugin directory.

### Manual install

1. Clone or download the plugin directory.
2. Run `/install-plugin /path/to/archolith-mcp-audit/plugins/claude`.
3. Restart Claude Code.

### Verify

After install, start a session and do some work. Then:

```
/audit
```

Should show per-server token usage. If it shows "No tool results observed yet," the
hook is not firing — check that `MCP_AUDIT_ENABLED=1` is set in the MCP server env
and that Python can import `archolith_mcp_audit` via the `PYTHONPATH` set in
`plugin.json`.

### Uninstall

```
/uninstall-plugin archolith-audit
```

## Structure

```
.claude-plugin/plugin.json    ← metadata + MCP server registration
hooks/hooks.json              ← async PostToolUse hook (.* matcher)
hook_observer.py              ← standalone hook wrapper (writes JSONL observations)
skills/audit/SKILL.md         ← /audit slash command
archolith_mcp_audit/          ← bundled core Python package (no pip install needed)
```

## Requirements

- Python 3.11+ on PATH (for MCP server + hook observer)
- Claude Code
