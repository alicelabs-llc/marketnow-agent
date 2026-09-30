# MarketNow — Agent Plugin (Claude Code · Cursor · Grok Build · Gemini CLI · Qwen Code · Codex)

MarketNow is the **trust layer for AI agents on MCP**: verify agent credentials (9 formats), scam-check domains, fingerprint MCP tools, and search a registry of **68,388 indexed MCP servers** with install-risk flags — from one hosted endpoint, free, no auth.

This repository packages MarketNow as a **universal agent plugin** — one repo, installable from every major agent:

| Agent | Install |
|---|---|
| **Claude Code** | `/plugin marketplace add alicelabs-llc/marketnow-agent` then `/plugin install marketnow@marketnow-agent` |
| **Grok Build** (xAI) | Listed in the [xAI plugin marketplace](https://github.com/xai-org/plugin-marketplace) — or add this repo as a marketplace source directly |
| **Cursor** | From the marketplace / Customize panel, or: `.cursor-plugin/` manifest in this repo |
| **Gemini CLI** | `gemini extensions install https://github.com/alicelabs-llc/marketnow-agent` |
| **Qwen Code** | `qwen extensions install alicelabs-llc/marketnow-agent:marketnow` (installs Claude Code marketplaces directly) |
| **Codex / any MCP client** | Add `https://marketnow.site/api/mcp` as a streamable-HTTP MCP server |

No API keys. No OAuth. No local install of anything (the MCP server is hosted and stateless for queries). The only write-side tool is `marketnow_submit_skill` (publishing to the public catalog), and it is honestly annotated as such.

## The 9 tools

| Tool | Purpose | Annotations |
|---|---|---|
| `marketnow_verify_trust` | Verify agent credentials (ATC v3, JWT/OAuth, W3C VC, MCP Card, A2A, EAT-AI, ZTA, SPIFFE SVID) | read-only, idempotent |
| `marketnow_translate_credential` | Translate credentials between the 9 adapter formats | read-only, idempotent |
| `marketnow_list_formats` | List supported credential formats | read-only, idempotent |
| `marketnow_get_pipeline` | 12-stage verification pipeline (PARSE→DECISION) | read-only, idempotent |
| `marketnow_check_domain` | Scam-check a domain (risk score + reasons) | read-only, idempotent |
| `marketnow_search_skills` | Search 68,388 MCP servers with security flags | read-only, idempotent |
| `marketnow_check_revocation` | Revocation status of Agent Trust Cards / CA keys | read-only, idempotent |
| `marketnow_fingerprint_tool` | Cryptographic fingerprint of MCP tool definitions (OWASP MCP Cheat Sheet) | read-only, idempotent |
| `marketnow_submit_skill` | Publish a validated skill to the public catalog | write-side (honest annotations) |

## Verify it yourself

```bash
curl -X POST https://marketnow.site/api/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

- Registry entry (official MCP Registry): `io.github.alicelabs-llc/marketnow` v1.15.0
- Website: https://marketnow.site · Privacy: https://marketnow.site/privacy
- Source: https://github.com/alicelabs-llc
- License: MIT OR Apache-2.0 (dual)
- Contact: eddyflores100@gmail.com

## Repository layout

```
.claude-plugin/    plugin.json + marketplace.json   (Claude Code)
.cursor-plugin/    plugin.json + marketplace.json + mcp.json   (Cursor)
.grok-plugin/      plugin.json + marketplace.json + mcp.json   (Grok Build / xAI)
.mcp.json          root MCP config (Grok remote / generic clients)
gemini-extension.json   (Gemini CLI)
skills/marketnow/SKILL.md   (Agent Skills format — all agents)
assets/logo.png
```
