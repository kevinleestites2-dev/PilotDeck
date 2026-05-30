# Pantheon — PilotDeck Product

The Pantheon WorkSpace product for PilotDeck.

Four Primes, one WorkSpace. Smart-routed. Always-on. White-box memory.

## Structure

```
products/pantheon/
  config/
    pilotdeck.yaml        ← Pantheon model routing + memory config
  plugins/
    ghost-prime/          ← GhostPrime swarm control
    scout-prime/          ← Lee County property intel
    zeus-prime/           ← On-chain + Polymarket ops
    openagora/            ← Arb engine via Nexus Relay
  commands/
    pantheon-status.md    ← /pantheon-status slash command
    war-chest.md          ← /war-chest slash command
  README.md               ← This file
```

## Deploy

```bash
# Link Pantheon plugins to PilotDeck global plugins dir
ln -s $(pwd)/products/pantheon/plugins/ghost-prime ~/.pilotdeck/plugins/ghost-prime
ln -s $(pwd)/products/pantheon/plugins/scout-prime ~/.pilotdeck/plugins/scout-prime
ln -s $(pwd)/products/pantheon/plugins/zeus-prime  ~/.pilotdeck/plugins/zeus-prime
ln -s $(pwd)/products/pantheon/plugins/openagora   ~/.pilotdeck/plugins/openagora

# Merge config
cat products/pantheon/config/pilotdeck.yaml >> ~/.pilotdeck/pilotdeck.yaml

# Start
npm run server
```

## Slash Commands

- `/pantheon-status` — full Pantheon health report (all 4 Primes)
- `/war-chest` — current War Chest balance + countdown to Citadel/Nexus/Steam Machine
