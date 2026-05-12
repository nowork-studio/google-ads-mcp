# Google Ads MCP by NotFair

[![MCP](https://img.shields.io/badge/MCP-Remote%20Server-111827)](https://modelcontextprotocol.io)
[![Google Ads](https://img.shields.io/badge/Google%20Ads-Compatible-4285F4)](https://notfair.co/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Find what's wrong. Fix it from your AI agent.

NotFair connects Claude, OpenAI Codex, Cursor, Cline, OpenClaw, Hermes, and other MCP-compatible agents to live Google Ads data. Your agent can diagnose account issues, draft fixes, and execute campaign changes only after you approve.

> This repo is the public setup guide for NotFair's hosted Google Ads MCP. You do not need to clone this repo or run a local server.

## Copy these values

| Field | Value |
| --- | --- |
| Website | `https://notfair.co/` |
| Connect Google Ads | `https://notfair.co/connect` |
| MCP server URL | `https://notfair.co/api/mcp/google_ads` |
| Connector name | `NotFair-GoogleAds` |

## 60-second setup

1. Connect Google Ads at `https://notfair.co/connect`.
2. Add the MCP server URL to your AI client.
3. Ask a read-only question first, such as: `Audit my Google Ads account and rank fixes by impact.`
4. Review proposed changes before approving any write.

```mermaid
flowchart LR
  A[You] --> B[Claude / Codex / Cursor / OpenClaw / Hermes]
  B --> C[NotFair Google Ads MCP]
  C --> D[Google Ads]
  D --> C
  C --> B
  B --> E[Diagnosis, fix draft, approval request]
  E --> A
```

## Choose your client

| Client | Easiest setup | What to paste |
| --- | --- | --- |
| OpenAI Codex | One terminal command | `codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads` |
| Claude.ai / Desktop / Cowork | Add custom connector | Name `NotFair-GoogleAds`, URL `https://notfair.co/api/mcp/google_ads` |
| Cursor | Add MCP server in settings | JSON config below |
| Cline | Add MCP server in settings | JSON config below |
| OpenClaw | Add remote MCP server or ask the agent to connect | JSON config or setup prompt below |
| Hermes | Add remote MCP server or ask the agent to connect | JSON config or setup prompt below |
| Any MCP client | Remote MCP config | JSON config below |

## OpenAI Codex

Run:

```bash
codex mcp add NotFair-GoogleAds --url https://notfair.co/api/mcp/google_ads
```

Then follow the browser sign-in flow. Use the Google account that has access to the target Google Ads account.

First prompt:

```text
Audit my Google Ads account and rank the highest-impact fixes. Pull live data before making recommendations.
```

## Claude.ai, Claude Desktop, and Claude Cowork

1. Open Claude settings.
2. Go to Connectors.
3. Add a custom connector.
4. Name it `NotFair-GoogleAds`.
5. Set the remote MCP server URL to `https://notfair.co/api/mcp/google_ads`.
6. Click Add.
7. Complete the NotFair and Google OAuth flow.
8. Open a new chat and ask a read-only question first.

First prompt:

```text
Why did leads get more expensive this week? Diagnose the cause and show the evidence before suggesting fixes.
```

## Cursor, Cline, OpenClaw, Hermes, and other MCP clients

Use this MCP server config anywhere your client accepts MCP JSON:

```json
{
  "mcpServers": {
    "NotFair-GoogleAds": {
      "url": "https://notfair.co/api/mcp/google_ads"
    }
  }
}
```

If your agent can set up MCP servers from a prompt, use:

```text
Connect to the NotFair Google Ads MCP. Use connector name NotFair-GoogleAds and remote MCP server URL https://notfair.co/api/mcp/google_ads. After connecting, run a read-only Google Ads audit and wait for my approval before making any changes.
```

If your client does not support remote MCP OAuth, generate or reconnect through NotFair and configure a secure bearer-token header:

```text
Authorization: Bearer YOUR_NOTFAIR_TOKEN
```

Do not paste bearer tokens into prompts, chats, screenshots, README files, or committed config.

## What users can ask

Use business-language prompts. You do not need to know Google Ads internals before starting.

```text
Find what's wrong with my Google Ads account and rank fixes by wasted spend.
```

```text
Find irrelevant search terms from the last 30 days. Draft negative keyword changes and wait for approval.
```

```text
Compare this week to last week. Explain what changed in spend, conversions, CPA, and conversion rate.
```

```text
Find campaigns where budget changes are justified. Show the math before recommending an increase.
```

```text
Draft new responsive search ads for the weakest ad group. Do not publish anything until I approve.
```

More complete examples are in [USAGE_EXAMPLES.md](USAGE_EXAMPLES.md).

## How writes stay controlled

```mermaid
sequenceDiagram
  participant User
  participant Agent as AI agent
  participant NF as NotFair MCP
  participant GA as Google Ads

  User->>Agent: Find wasted spend
  Agent->>NF: Read campaigns, keywords, search terms
  NF->>GA: Fetch live Google Ads data
  GA-->>NF: Results
  NF-->>Agent: Structured account data
  Agent-->>User: Findings + proposed fix
  User->>Agent: Approve this change
  Agent->>NF: Execute approved write
  NF->>GA: Apply change
  GA-->>NF: Confirmation
  NF-->>Agent: Write result
  Agent-->>User: Change applied + summary
```

Rules to follow:

- Reads can inspect live Google Ads data after authorization.
- Writes should be reviewed before they land.
- Ask the agent to show the diff, expected impact, and rollback plan before approval.
- Reconnect at `https://notfair.co/connect` if auth expires.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| The client cannot find the server | Check the URL is exactly `https://notfair.co/api/mcp/google_ads`. |
| The agent says auth expired | Reconnect at `https://notfair.co/connect`, then retry. |
| No Google Ads accounts appear | Sign in with the Google account that has access to the Ads customer. |
| OAuth opens but setup does not finish | Remove the connector, add it again, then retry the OAuth flow. |
| The agent wants to make a change too quickly | Ask it to run read-only diagnosis first and show the proposed diff before writing. |

## Legacy endpoint

Existing NotFair installs may still use:

```text
https://notfair.co/api/mcp
```

New installs should use:

```text
https://notfair.co/api/mcp/google_ads
```

## Links

- NotFair: https://notfair.co/
- Connect Google Ads: https://notfair.co/connect
- Usage examples: [USAGE_EXAMPLES.md](USAGE_EXAMPLES.md)
- Agent instructions: [AGENTS.md](AGENTS.md)
- Model Context Protocol: https://modelcontextprotocol.io

## License

This repository is open source under the [MIT License](LICENSE).

## Support

For setup help, contact `tong@notfair.co`.

