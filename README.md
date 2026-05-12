# Google Ads MCP by NotFair

Connect AI clients such as Claude, OpenAI Codex, Cursor, Cline, and any MCP-compatible client to Google Ads through NotFair.

NotFair hosts the MCP server, handles Google Ads OAuth, and exposes tools your AI client can use to inspect campaigns, search terms, keywords, budgets, ads, and performance. Read operations are available after connection. Write operations are designed to be approval-gated so the agent can draft changes and you can approve them before they touch Google Ads.

## Hosted MCP server

Use this remote MCP server URL:

```text
https://notfair.co/api/mcp/google_ads
```

Recommended connector name:

```text
NotFair-GoogleAds
```

## Requirements

- A NotFair account
- A Google account with access to the Google Ads account you want to manage
- An MCP-compatible client
- For OAuth setup, a client that supports remote MCP OAuth such as Claude.ai or OpenAI Codex

Start here:

```text
https://notfair.co/connect
```

## OpenAI Codex setup

Install the MCP server in Codex:

```bash
codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads
```

Codex will walk through the OAuth flow. Sign in with the Google account that has Google Ads access, select the account, then return to Codex.

Try:

```text
Audit my Google Ads account and rank the highest-impact fixes.
```

## Claude setup

For Claude.ai Web, Claude Desktop, or Claude Cowork:

1. Open Claude connector settings.
2. Add a custom connector.
3. Use this name:

```text
NotFair-GoogleAds
```

4. Use this remote MCP server URL:

```text
https://notfair.co/api/mcp/google_ads
```

5. Click Add and complete the NotFair/Google OAuth flow.
6. Start a new Claude chat and ask about your Google Ads account.

Try:

```text
Find search terms I should add as negative keywords, but show me the proposed changes before writing.
```

## Cursor, Cline, and other MCP clients

Use a remote MCP config like this:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If your client does not support OAuth for remote MCP servers, generate a NotFair connection/token from:

```text
https://notfair.co/connect
```

Then configure your client to send it as:

```text
Authorization: Bearer YOUR_NOTFAIR_TOKEN
```

Exact config syntax varies by MCP client.

## What you can ask

Good first prompts:

```text
Audit my Google Ads account and rank fixes by likely impact.
```

```text
Which campaigns wasted the most spend in the last 30 days?
```

```text
Find zero-conversion keywords with meaningful spend.
```

```text
Draft negative keywords from irrelevant search terms and wait for my approval before applying.
```

```text
Explain why CPA changed this week compared with last week.
```

## Safety model

- OAuth is handled by NotFair.
- The MCP server URL is remote; you do not need to run a local Google Ads server.
- Read tools can inspect live Google Ads data after you connect.
- Write tools should present proposed changes for approval before execution.
- You can revoke Google access from your Google account permissions or disconnect from NotFair.

## Troubleshooting

### The connector is added but cannot see my account

Reconnect Google Ads at:

```text
https://notfair.co/connect
```

Make sure you sign in with the Google account that has access to the target Google Ads customer.

### OAuth opens but returns to the wrong client

Remove the connector from your MCP client, add it again with the exact server URL, then retry:

```text
https://notfair.co/api/mcp/google_ads
```

### The AI says authentication expired

Reconnect NotFair to Google Ads:

```text
https://notfair.co/connect
```

Then retry the same request.

### I use an older NotFair MCP URL

The older endpoint may still work for existing connections:

```text
https://notfair.co/api/mcp
```

New setups should use the platform-specific Google Ads endpoint:

```text
https://notfair.co/api/mcp/google_ads
```

## Links

- NotFair: https://notfair.co
- Google Ads MCP page: https://notfair.co/google-ads-mcp
- Codex setup guide: https://notfair.co/google-ads-codex-mcp-setup-guide
- Claude connector setup guide: https://notfair.co/google-ads-claude-connector-setup-guide
- Model Context Protocol: https://modelcontextprotocol.io

## Support

For setup help, contact:

```text
tong@notfair.co
```
