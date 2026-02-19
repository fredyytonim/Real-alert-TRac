# SKILL.md — TRAC Real-Time Alert System

This file describes how agents should interact with the TRAC Alert System app.

## App Purpose
Monitor a TRAC/TNK wallet in real-time and send alerts based on configurable rules.

## Agent Capabilities

### 1. Set Wallet
- Prompt user for their TRAC wallet address
- Validate format (bc1q... or tb1q...)
- Initialize monitoring session

### 2. Configure Alert Rules
Agents can set:
- `incoming_threshold` (TNK) — minimum amount to trigger incoming alert
- `outgoing_threshold` (TNK) — minimum amount to trigger outgoing alert
- `whale_threshold` (TNK) — amount that counts as a "whale" transaction
- `balance_drop_pct` (%) — percentage drop that triggers balance alert

### 3. Natural Language Commands
Agents should parse and respond to:
- "Alert me if I receive more than X TNK" → set incoming threshold
- "Set large threshold to X" → set whale threshold
- "What is my balance?" → return current balance
- "Stop monitoring" → pause all alerts
- "Status" → return monitoring status + balance

### 4. Alert Format
When an alert fires, respond with:
```
[ALERT TYPE] — [AMOUNT] TNK
Direction: incoming/outgoing
TX Hash: [hash]
New Balance: [balance] TNK
```

### 5. Error Handling
- If wallet address is invalid: "Please enter a valid TRAC wallet address."
- If no rules are active: "Enable at least one alert rule before monitoring."
- If monitoring fails: "Could not connect to Intercom network. Retrying..."

## Integration Notes
- This app runs client-side; integrate with Intercom P2P sidechannels for live TX data
- Alert state persists in memory during session
- Multiple wallets can be monitored by repeating the setup flow
