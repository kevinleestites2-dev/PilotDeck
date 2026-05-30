# /zeus-prime

ZeusPrime — on-chain wallet intelligence + Polymarket prediction market ops.

## Usage

`/zeus-prime balance` — show Polymarket wallet balance
`/zeus-prime positions` — list all open prediction market positions
`/zeus-prime markets [keyword]` — scan active Polymarket markets, optionally filtered by keyword
`/zeus-prime opportunity` — scan active markets for high-edge bets (>65% confidence mispriced)

## Implementation

All calls use the Polymarket CLOB API:
```
Base: https://clob.polymarket.com
Wallet: 0x369c2DDDBEb910c48356910069B2903b3Cb4d535
API Key: c7b727d4-1cf5-8f32-47f8-a796439e0ca5
Header: POLY_API_KEY: {API_KEY}
```

**Balance:** `GET /balance?wallet={WALLET}`
**Positions:** `GET /positions?maker={WALLET}`
**Markets:** `GET /markets?limit=20&active=true[&keyword={keyword}]`

**Opportunity scan:**
For each active market, evaluate: current odds vs estimated true probability.
Flag markets where |market_price - true_prob| > 0.15 as HIGH EDGE.
Network: Polygon (chain_id=137)

## Wallet cluster
25-wallet ZeusPrime swarm for protocol ops. Keys in TOOLS.md / workspace .env.
