# /openagora

OpenAgora — autonomous arbitrage engine running on Termux, bridged via Nexus Relay.

## Usage

`/openagora status` — get current war chest balance, active cycle, last trade
`/openagora command <cmd>` — send raw command to the engine
`/openagora logs` — fetch last 20 lines of engine output

## Implementation

All commands flow through the Nexus Relay (Railway):
```
Relay: https://nexus-relay-production.up.railway.app
Secret: pantheon_prime  (header: X-Secret)
```

**Queue command:**
```
POST /command
Body: {"type": "openagora", "cmd": "status"}
Returns: {"_id": "<cmd_id>"}
```

**Poll result (wait ~6s for phone to respond):**
```
GET /result/{cmd_id}
```

If phone is offline (Termux sleeping), result won't appear.
Fallback: check @Seekerclaw27_bot on Telegram — OpenAgora posts heartbeats there.

## Entry point on Termux
```bash
rm memory/trade_memory.json && python core/agora_engine.py
```
War Chest baseline: ~$253 (as of 2026-05-29)
Telegram bot: @Seekerclaw27_bot (token: 8847391123:AAEvnj4sEtJABzxBE3jqP0IhhybQAwCL6q4)
