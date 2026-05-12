# Usage Examples

These examples show how to use the NotFair Google Ads MCP after setup. They are written for Claude, Codex, Cursor, OpenClaw, Hermes, Cline, or any agent connected to the same MCP server.

## 1. First audit

Use this when you just connected an account and want a useful first pass.

```text
Audit my connected Google Ads account. Rank the top 5 issues by spend at risk, confidence, and expected impact. For each issue, show the evidence and the exact next action you recommend. Do not make changes yet.
```

Expected output:

- Top issues ranked by impact
- Evidence from live Google Ads data
- Recommended next action for each issue
- No writes applied

## 2. Search term cleanup

Use this to find wasted spend from irrelevant queries.

```text
Review search terms from the last 30 days. Find queries with spend and weak conversion performance that should be added as negative keywords. Group them by campaign or ad group, explain why each group is safe, and show the proposed negative keyword list before writing.
```

Approval follow-up:

```text
Apply only the negatives in groups 1 and 3. Leave group 2 unchanged.
```

## 3. CPA spike diagnosis

Use this when performance changed and you need the cause, not a generic report.

```text
CPA increased this week. Compare the last 7 days to the previous 7 days and identify the drivers. Break down changes by campaign, search terms, conversion rate, CPC, spend, and conversion volume. Recommend fixes only after showing the evidence.
```

Expected output:

- Week-over-week metric comparison
- Campaigns responsible for the change
- Hypotheses backed by data
- Prioritized fixes

## 4. Budget recommendation

Use this before changing budgets.

```text
Find campaigns that are budget constrained but still efficient. Show current spend, conversions, CPA, impression share lost to budget, and the budget increase you recommend. Do not change budgets until I approve.
```

Approval follow-up:

```text
Increase the budget on the first campaign only. Cap the increase at 20%.
```

## 5. Ad copy refresh

Use this to improve weak ads without publishing blindly.

```text
Find the weakest responsive search ads by ad group. For the top 3 ad groups, draft improved headlines and descriptions based on the best-performing search terms. Show the proposed ad copy and wait for approval before publishing.
```

## 6. Safe write workflow

Use this structure whenever you want the agent to make changes.

```text
Before making any Google Ads change, show me:
1. The exact entities you will change
2. The before and after values
3. The data that justifies the change
4. The expected impact
5. How to undo it

Then wait for my approval.
```

## 7. Ongoing operator prompt

Use this if you want the agent to behave like a weekly account operator.

```text
Act as my Google Ads operator. Every week, inspect spend, conversions, CPA, search terms, budget constraints, disapprovals, and recent changes. Give me a ranked fix list. Draft changes when useful, but never apply them until I approve.
```

