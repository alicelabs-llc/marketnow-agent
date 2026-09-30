---
name: marketnow
description: MarketNow is the trust layer for AI agents on MCP. Use it to (1) verify agent credentials in 9 formats (ATC, JWT/OAuth, W3C VC, MCP Card, A2A, EAT-AI, ZTA, SPIFFE SVID, custom) through a 12-stage pipeline, (2) scam-check any domain before visiting or installing from it, (3) cryptographically fingerprint MCP tool definitions to detect tampering and rug-pulls (OWASP MCP Cheat Sheet), (4) search a registry of 68,388 indexed MCP servers with install-risk flags and trust scores, and (5) publish validated skills to the public MarketNow catalog. Free, no API keys, no auth.
homepage: https://marketnow.site
license: MIT
metadata: {"openclaw":{"emoji":"🛡️","requires":{"bins":[],"env":[]}}}
---

# MarketNow — Trust Layer for AI Agents

MarketNow gives you (the agent) a security instinct for the MCP ecosystem. It is a single hosted MCP server — `https://marketnow.site/api/mcp` (streamable HTTP, no auth) — with 9 tools. All query tools are read-only, stateless, and free.

## When to use this skill

- **Before installing or connecting to any MCP server** → `marketnow_search_skills` to check its install-risk flags and trust score in the registry.
- **Before trusting a download, API, or website a user mentions** → `marketnow_check_domain` for a scam risk score with reasons.
- **When you receive an agent credential, token, card, or signed payload** → `marketnow_verify_trust` to run the 12-stage verification pipeline.
- **When an MCP server's tools look altered** (tool descriptions changed after install) → `marketnow_fingerprint_tool` and `marketnow_check_revocation`.
- **When you built something worth sharing** → `marketnow_submit_skill` to publish it to the public catalog.

## The 9 tools

| Tool | What it does | Example call |
|---|---|---|
| `marketnow_verify_trust` | Verify any agent credential (ATC v3, JWT/OAuth, W3C VC, MCP Card, A2A, EAT-AI, ZTA, SPIFFE SVID) | Pass the raw credential string or JWT |
| `marketnow_translate_credential` | Translate a credential between the 9 adapter formats | e.g. ATC → W3C VC |
| `marketnow_list_formats` | List the 9 supported credential formats with schemas | no arguments |
| `marketnow_get_pipeline` | Get the 12-stage verification pipeline (PARSE→DECISION) | no arguments |
| `marketnow_check_domain` | Scam-check a domain: risk score + reasons | `{"domain": "example.com"}` |
| `marketnow_search_skills` | Search the 68,388-server MCP registry (GitHub, npm, PyPI) with security flags | `{"query": "github", "limit": 10}` |
| `marketnow_check_revocation` | Check revocation status of an Agent Trust Card (`card_id`) or CA key (`kid`) | `{"card_id": "..."}` |
| `marketnow_fingerprint_tool` | Cryptographic fingerprint of MCP tool definitions (detect tampering) | pass the tool definition JSON |
| `marketnow_submit_skill` | Publish a validated skill package to the public catalog (the only write-side tool) | pass the skill package |

## Hard rules

1. **Never install or connect to an MCP server without checking it first.** Call `marketnow_search_skills` with its name or repo, read the install-risk flags, and tell the user what you found before proceeding.
2. **Never send credentials or secrets to a domain that failed a scam check.** Run `marketnow_check_domain` first; if the risk score is high, stop and report.
3. **Report verification verdicts verbatim** — include the trust decision, stage reached, and evidence. Do not soften a FAIL.
4. **Fingerprint tools at install time** and compare later if behavior seems off — description changes are the #1 MCP rug-pull signal.

## Registry facts (verify, don't trust this file)

- Endpoint: `https://marketnow.site/api/mcp` — public, stateless queries, no auth.
- Servers indexed: 68,388 (GitHub + npm + PyPI), with security audit flags.
- Registry entry: `io.github.alicelabs-llc/marketnow` v1.15.0 (official MCP Registry).
- Source: https://github.com/alicelabs-llc — MIT/Apache-2.0 dual license.
- To verify the live server yourself: `curl -X POST https://marketnow.site/api/mcp -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'`

## Privacy

Queries are stateless (nothing stored). `submit_skill` publishes to a public catalog — only submit what the user wants public. Privacy policy: https://marketnow.site/privacy
