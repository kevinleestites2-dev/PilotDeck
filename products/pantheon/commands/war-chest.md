# /war-chest

War Chest balance + countdown to Pantheon financial targets.

## Targets (MidasPrime mandate)
- **Citadel** (Apartment): $5,000
- **Nexus** (1TB Laptop): $3,000
- **Steam Machine**: $600 (deadline: Holiday 2027)

## Implementation

1. Query OpenAgora via Nexus Relay for current war chest balance:
   ```
   POST https://nexus-relay-production.up.railway.app/command
   X-Secret: pantheon_prime
   Body: {"type": "openagora", "cmd": "war_chest"}
   ```
   Wait 6s, poll GET /result/{id}

2. If relay offline, use last known value: ~$253 (2026-05-29)

3. Compute progress:
   - Citadel: {balance} / $5,000 = {pct}%
   - Nexus: {balance} / $3,000 = {pct}%
   - Steam Machine: {balance} / $600 = {pct}%

4. Format as progress bars and ETA based on current burn rate.

## Context
Banking: Checking | Routing: 031101279 | Account: 333394759539
MidasPrime tracker: midas_tracker.py
