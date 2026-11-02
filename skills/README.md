# Plugin skills

Cursor treats a `SKILL.md` at the plugin root as a plugin skill when this `skills/` directory is absent and the manifest has no `skills` field. This directory is the plugin skill path (`./skills` in `.cursor-plugin/plugin.json`). It has no `SKILL.md`, so the Marketplace plugin ships the remote MCP server only.

The ClawHub package stays `/SKILL.md` at the repository root (agent API, `FYN_API_KEY`).
