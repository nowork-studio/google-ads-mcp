# AGENTS.md

Instructions for AI agents and MCP clients using the NotFair Google Ads MCP.

This repository documents a hosted remote MCP server. Do not try to run a local Google Ads MCP server from this repo.

## Canonical values

| Field | Value |
| --- | --- |
| Product | NotFair Google Ads MCP |
| Website | `https://notfair.co/` |
| Connect URL | `https://notfair.co/connect` |
| Remote MCP URL | `https://notfair.co/api/mcp/google_ads` |
| Connector name | `NotFair-GoogleAds` |
| Legacy endpoint | `https://notfair.co/api/mcp` |

Use `https://notfair.co/api/mcp/google_ads` for every new install.

## Agent operating rules

- Treat NotFair as the hosted OAuth and Google Ads API bridge.
- Prefer remote MCP OAuth when the client supports it.
- If bearer-token auth is required, store the token only in the client's secure secret/header config.
- Never ask the user to paste tokens into a chat.
- Start with read-only diagnosis.
- Before a write, show the exact proposed change, expected impact, risk, and rollback path.
- Wait for explicit user approval before applying changes.
- Never claim a Google Ads change landed unless the MCP tool result confirms it.
- If auth fails, tell the user to reconnect at `https://notfair.co/connect`.

## OpenClaw

Recommended setup prompt:

```text
Connect to the NotFair Google Ads MCP. Use connector name NotFair-GoogleAds and remote MCP server URL https://notfair.co/api/mcp/google_ads. After connecting, run a read-only Google Ads audit and wait for my approval before making any changes.
```

Config shape if editing MCP JSON directly:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

After connecting, verify tool discovery before making requests.

## Hermes

Recommended setup prompt:

```text
Add the NotFair Google Ads MCP as a remote MCP server named NotFair-GoogleAds at https://notfair.co/api/mcp/google_ads. Use OAuth if available. Start with read-only diagnosis and require approval before writes.
```

Config shape:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

## OpenAI Codex

Install:

```bash
codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads
```

First prompt:

```text
Audit my connected Google Ads account. Rank the top fixes by spend at risk, evidence strength, and expected impact.
```

## Claude.ai, Claude Desktop, and Claude Cowork

Use Claude's custom connector flow:

- Name: `NotFair-GoogleAds`
- Remote MCP server URL: `https://notfair.co/api/mcp/google_ads`

After OAuth completes, open a fresh chat and start with a read-only diagnosis.

## Claude Code

If using remote MCP config directly:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If using a plugin marketplace flow, verify the plugin points to the same server URL.

## Cursor

Add this to Cursor's MCP configuration:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

Reload Cursor's MCP servers after editing config.

## Cline

Add the same remote MCP JSON config in Cline's MCP settings:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

Use OAuth when available. If using bearer auth, keep the token in Cline's secret/header mechanism.

## Good default first prompts

```text
Find what's wrong with my Google Ads account. Rank issues by wasted spend, confidence, and likely impact.
```

```text
Why did CPA change this week compared with last week? Pull live data and show the drivers.
```

```text
Find irrelevant search terms from the last 30 days. Draft negative keyword changes and wait for approval.
```

## Setup failure checklist

1. Server URL is exactly `https://notfair.co/api/mcp/google_ads`.
2. Connector name is `NotFair-GoogleAds`.
3. User completed NotFair OAuth at `https://notfair.co/connect`.
4. Google account has access to the target Ads customer.
5. Client has reloaded or restarted MCP servers.
6. New installs are not using the legacy endpoint.

