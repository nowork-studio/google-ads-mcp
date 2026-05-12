# AGENTS.md

Instructions for AI agents and MCP clients working with the NotFair Google Ads MCP.

This repository is documentation for a hosted remote MCP server. Do not try to run a local Google Ads MCP server from this repo.

## Canonical connection values

- Product: NotFair Google Ads MCP
- Website: `https://notfair.co/`
- Connect URL: `https://notfair.co/connect`
- Remote MCP URL: `https://notfair.co/api/mcp/google_ads`
- Connector name: `NotFair-GoogleAds`
- Legacy endpoint: `https://notfair.co/api/mcp`

Use the platform-specific endpoint for all new installs:

```text
https://notfair.co/api/mcp/google_ads
```

## General agent behavior

- Treat NotFair as the hosted OAuth and Google Ads API bridge.
- Prefer OAuth when the MCP client supports remote MCP OAuth.
- If bearer-token auth is required, tell the user to generate or reconnect through NotFair and configure `Authorization: Bearer <token>`.
- Start with read-only diagnostics before suggesting account changes.
- Before any write action, show the proposed change, explain expected impact, and wait for explicit user approval.
- Never claim a Google Ads change was applied unless the MCP tool result confirms it.
- If auth fails, ask the user to reconnect at `https://notfair.co/connect`.

## OpenClaw

Add the NotFair Google Ads MCP as a remote MCP server using the canonical URL:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

After connecting, verify tool discovery before making Google Ads requests. If the server returns an auth challenge, complete the NotFair OAuth flow.

## Hermes

Configure Hermes as a remote MCP client with:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If Hermes requires explicit headers instead of OAuth, provide a NotFair bearer token through its secure secret/header configuration. Do not paste tokens into prompts or committed files.

## OpenAI Codex

Install with:

```bash
codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads
```

Then start with:

```text
Audit my Google Ads account and rank the highest-impact fixes.
```

## Claude.ai, Claude Desktop, and Claude Cowork

Use Claude's custom connector flow:

- Name: `NotFair-GoogleAds`
- Remote MCP server URL: `https://notfair.co/api/mcp/google_ads`

After OAuth completes, open a new chat and ask a read-only question first.

## Claude Code

If using remote MCP configuration directly, use:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If using a plugin marketplace flow, follow NotFair's current Claude Code instructions from `https://notfair.co/` and verify the plugin points to the same server URL.

## Cursor

Add the remote MCP server to Cursor's MCP configuration:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

Restart or reload Cursor's MCP servers after editing the config.

## Cline and other MCP clients

Use the same remote MCP JSON shape when supported:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If the client does not support remote MCP OAuth, use a bearer token stored in the client's secure secret/header mechanism.

## Recommended first prompts

```text
Audit my Google Ads account. Rank issues by wasted spend, likely impact, and confidence.
```

```text
Find irrelevant search terms that should become negative keywords. Show the proposed changes and wait for approval.
```

```text
Explain why conversions or CPA changed this week compared with last week.
```

## Troubleshooting invariant

When setup fails, verify these in order:

1. The client is using `https://notfair.co/api/mcp/google_ads`.
2. The user completed NotFair OAuth at `https://notfair.co/connect`.
3. The Google account has access to the target Google Ads customer.
4. The MCP client refreshed or reloaded after adding the server.
5. The agent is not using the legacy endpoint for a new install.

