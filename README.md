# Google Ads MCP by NotFair

[![MCP](https://img.shields.io/badge/MCP-Remote%20Server-111827)](https://modelcontextprotocol.io)
[![Google Ads](https://img.shields.io/badge/Google%20Ads-Compatible-4285F4)](https://notfair.co/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Hosted Google Ads MCP for AI agents.

NotFair gives Claude, OpenAI Codex, Cursor, Cline, OpenClaw, Hermes, and other MCP-compatible clients live access to Google Ads data through a hosted remote MCP server. Users connect with Google OAuth through NotFair, then ask their AI agent to audit campaigns, inspect search terms, diagnose performance changes, and draft approved account changes.

This repository is the public setup guide for the NotFair Google Ads MCP endpoint. The server is hosted by NotFair; you do not need to clone or run this repository to use it.

## Quick start

Use this remote MCP server URL:

```text
https://notfair.co/api/mcp/google_ads
```

Recommended connector name:

```text
NotFair-GoogleAds
```

Start the Google Ads connection flow here:

```text
https://notfair.co/connect
```

Website:

```text
https://notfair.co/
```

## What it does

- Connects AI agents to live Google Ads account data
- Supports campaign, ad group, keyword, search term, budget, ad, asset, and performance analysis
- Lets agents draft changes such as negatives, bids, budgets, ads, and campaign updates
- Keeps Google Ads OAuth and developer-token plumbing inside NotFair
- Uses approval-oriented write flows so users stay in control of changes

## Installation

### OpenAI Codex

Add the remote MCP server:

```bash
codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads
```

Codex will open or guide you through the OAuth flow. Sign in with the Google account that has access to the target Google Ads account.

Try:

```text
Audit my Google Ads account and rank the highest-impact fixes.
```

### Claude.ai, Claude Desktop, and Claude Cowork

1. Open Claude connector settings.
2. Add a custom connector.
3. Set the connector name to `NotFair-GoogleAds`.
4. Set the remote MCP server URL to `https://notfair.co/api/mcp/google_ads`.
5. Click Add.
6. Complete the NotFair and Google OAuth flow.
7. Start a new Claude chat and ask about your Google Ads account.

Try:

```text
Find search terms I should add as negative keywords. Show me the proposed changes before applying anything.
```

### Cursor, Cline, OpenClaw, Hermes, and other MCP clients

Use this remote MCP config where your client accepts MCP server definitions:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If your client supports remote MCP OAuth, use OAuth. If it requires a bearer token, generate or reconnect through NotFair and configure your client to send:

```text
Authorization: Bearer YOUR_NOTFAIR_TOKEN
```

Client-specific details vary. See [AGENTS.md](AGENTS.md) for agent-oriented setup notes.

## Example prompts

Start with read-only analysis:

```text
Audit my Google Ads account. Rank issues by likely wasted spend and expected impact.
```

```text
Compare this week to last week and explain what changed in CPA, conversion volume, and spend.
```

```text
Find search terms with spend and no conversions that are good candidates for negatives.
```

Move into controlled changes:

```text
Draft negative keyword changes for irrelevant search terms. Show the diff and wait for approval before writing.
```

```text
Draft two new responsive search ads for the weakest ad group. Do not publish until I approve.
```

```text
Find campaigns limited by budget where increasing budget is justified by conversion performance. Show the math first.
```

## Safety model

- NotFair handles Google OAuth and Google Ads API access.
- The MCP endpoint is remote and protected; unauthenticated requests should receive an auth challenge.
- Read actions can inspect live Google Ads data after authorization.
- Write actions should be treated as approval-gated: ask the agent to show proposed changes before applying them.
- Users can revoke Google access from their Google account or disconnect from NotFair.

## Troubleshooting

### The connector is installed but cannot see my account

Reconnect through NotFair:

```text
https://notfair.co/connect
```

Use the Google account that has access to the Google Ads customer you want to manage.

### OAuth opens but the client does not finish connecting

Remove the connector from the client and add it again with the exact endpoint:

```text
https://notfair.co/api/mcp/google_ads
```

### The agent says authentication expired or was revoked

Reconnect Google Ads in NotFair, then retry the same prompt:

```text
https://notfair.co/connect
```

### I have an older NotFair MCP URL

The legacy endpoint may still work for existing connections:

```text
https://notfair.co/api/mcp
```

New setups should use the platform-specific Google Ads endpoint:

```text
https://notfair.co/api/mcp/google_ads
```

## Links

- NotFair: https://notfair.co/
- Connect Google Ads: https://notfair.co/connect
- Model Context Protocol: https://modelcontextprotocol.io

## License

This repository is open source under the [MIT License](LICENSE).

## Support

For setup help, contact:

```text
tong@notfair.co
```

