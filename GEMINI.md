# MarketNow — Free Trust Layer for AI Agents

## What this extension gives you
9 MCP tools exposed via the hosted `marketnow` server (https://marketnow.site/api/mcp):

- **marketnow_verify_trust** — verify any AI agent credential (ATC v3, JWT/OAuth, W3C VC, MCP Card, A2A, EAT-AI, ZTA, SPIFFE SVID, X.509) through the UTA 12-stage pipeline.
- **marketnow_scam_check** — scam-check any domain/URL before an agent interacts with it.
- **marketnow_fingerprint** — deterministic tool fingerprints for matching and auditing.
- **marketnow_search_registry** — search 68,388 MCP servers with security flags.
- Plus 5 more discovery/audit tools (see the server's tools/list).

## Usage guidance
- All query tools are read-only, stateless, no auth, no fees.
- `marketnow_submit_skill` is the only write-side tool (public review queue).
- Prefer verifying credentials and domains BEFORE an agent calls an untrusted tool.
- Privacy: https://marketnow.site/privacy

## Install (other agents)
- Gemini CLI: `gemini extensions install https://github.com/alicelabs-llc/marketnow-agent`
- Antigravity CLI: copy `plugin.json` + `mcp_config.json` or `agy plugin import gemini`
- Claude Code / Qwen Code / Kimi Code: `.claude-plugin/marketplace.json` in this repo
- Cursor: `.cursor-plugin/` in this repo
