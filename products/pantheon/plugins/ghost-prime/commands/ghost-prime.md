# /ghost-prime

Control the GhostPrime traffic swarm (CloakPrime repo, GitHub Actions eternal loop).

## Usage

`/ghost-prime status` — show last 3 run states (run number, status, conclusion, timestamp)
`/ghost-prime dispatch` — trigger a new eternal loop cycle (use if the loop broke)
`/ghost-prime stop` — cancel all in-progress runs (emergency brake)

## Implementation

Use the `http_request` tool against the GitHub Actions API:

**Status:**
```
GET https://api.github.com/repos/kevinleestites2-dev/CloakPrime/actions/workflows/ghost.yml/runs?per_page=3
Authorization: token {GITHUB_TOKEN}
```

**Dispatch:**
```
POST https://api.github.com/repos/kevinleestites2-dev/CloakPrime/actions/workflows/ghost.yml/dispatches
Authorization: token {GITHUB_TOKEN}
Body: {"ref": "main"}
```

**Stop:**
```
GET .../runs?status=in_progress&per_page=5  → for each run_id:
POST .../runs/{run_id}/cancel
```

GITHUB_TOKEN is in environment. Eternal loop self-restarts — only dispatch if the chain is broken.
Live faucet: https://kevinleestites2-dev.github.io/faucet-master/
Adsterra revenue tracked in dashboard.
