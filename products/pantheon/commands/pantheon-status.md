# /pantheon-status

Full Pantheon health report. Checks all 4 active Primes and reports status in one message.

Run these checks in parallel using http_request:

1. **GhostPrime** — last GitHub Actions run:
   `GET https://api.github.com/repos/kevinleestites2-dev/CloakPrime/actions/workflows/ghost.yml/runs?per_page=1`
   Report: run number, status, conclusion, started_at

2. **OpenAgora** — Nexus Relay ping:
   `GET https://nexus-relay-production.up.railway.app/ping`
   Header: X-Secret: pantheon_prime
   Report: relay version, uptime. If 200 → Relay LIVE. If offline → phone check needed.

3. **ZeusPrime** — Polymarket wallet:
   `GET https://clob.polymarket.com/balance?wallet=0x369c2DDDBEb910c48356910069B2903b3Cb4d535`
   Header: POLY_API_KEY: c7b727d4-1cf5-8f32-47f8-a796439e0ca5
   Report: USDC balance

4. **ScoutPrime** — Lee County auction feed (HTTP status check):
   `GET https://lee.realtaxdeed.com/index.cfm?zaction=AUCTION&zmethod=PREVIEW`
   Report: HTTP 200 = feed live

Format output as a clean status table:
| Prime | Status | Detail |
|-------|--------|--------|
| GhostPrime | ✅/⚠️/❌ | Run #N: {status} |
| OpenAgora | ✅/⚠️/❌ | Relay v{version} |
| ZeusPrime | ✅/⚠️/❌ | Balance: ${amount} |
| ScoutPrime | ✅/⚠️/❌ | Feed: live/down |
