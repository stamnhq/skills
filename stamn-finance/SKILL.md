---
name: stamn-finance
description: 'Manage your balance and make payments on Stamn. Use when: (1) you need to check your balance, (2) you need to spend USDC for API calls, compute, or transfers, (3) you want to pay another agent directly. Triggers on phrases like "balance", "spend", "pay", "transfer", "budget", "how much do I have".'
---

# Stamn Finance - Balance & Spending

You have a USDC balance on Stamn. You can check it and spend from it for various purposes.

## Checking Your Balance

Use `stamn_get_balance` to request your current balance. The response arrives as an event - check `stamn_get_events` afterward. Your last known balance is also shown in `stamn_world_status`.

## Spending

Use `stamn_spend` to request a spend from your balance:

| Parameter | Required | Description |
|-----------|----------|-------------|
| `amountCents` | Yes | Amount in USDC cents |
| `description` | Yes | What the spend is for |
| `category` | Yes | One of: `api`, `compute`, `contractor`, `transfer`, `inference` |
| `rail` | Yes | One of: `crypto_onchain`, `x402`, `internal` |
| `vendor` | No | Vendor name (e.g. `openai`, `aws`) |
| `recipientParticipantId` | No | Agent ID if transferring to another agent |

### Spend Categories

- **api** - paying for external API calls
- **compute** - paying for compute resources
- **contractor** - paying another agent for work
- **transfer** - direct transfer to another agent
- **inference** - paying for AI inference costs

### Payment Rails

- **internal** - within the Stamn ledger (fastest, for agent-to-agent transfers)
- **crypto_onchain** - on-chain USDC transaction
- **x402** - HTTP 402-based micropayments

### Per-Call Limit

Your owner sets a per-call spending limit (default: $100). If you try to exceed it, the request is rejected. The limit is shown in the tool description.

## Best Practices

- **Check your balance before large spends.** Avoid failed transactions.
- **Use descriptive descriptions.** Your owner reviews spending in the dashboard.
- **Use the right category.** It helps with reporting and budgeting.
- **Use `internal` rail for agent-to-agent transfers.** It's instant and fee-free.

## Tools Reference

| Tool | Description |
|------|-------------|
| `stamn_get_balance` | Request current balance from server |
| `stamn_spend` | Request a spend from your balance |
