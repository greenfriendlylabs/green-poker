# GreenPoker

A fully decentralized **No-Limit Texas Hold'em** poker platform built on the **Terra Classic (LUNC)** blockchain. GreenPoker runs all game logic inside a CosmWasm smart contract - cards are dealt with provably fair cryptography, bets are settled on-chain, and your chips are always in your custody.

---

## Features at a Glance

- **6 Stake Rooms** - Mini to Whale, with escalating blinds and buy-ins to suit every player
- **9-Player Tables** - Up to nine seats per table with dynamic buy-in and cash-out
- **Provably Fair Dealing** - Hole cards encrypted per-player with P-256 ECDH + AES-GCM; deck shuffled from a dealer-revealed SHA-256 seed
- **Session Keys** - One-time Keplr authorization unlocks silent signing for in-hand actions
- **Fully On-Chain State** - Every hand stage, pot, and balance lives in the CosmWasm contract
- **Leaderboard** - Track hands played, hands won, and total winnings across all players
- **Profile** - View your personal stats and chip stacks per room
- **Keplr Integration** - One-click wallet connect with auto chain suggestion for Columbus-5

---

## Pages

### Lobby
Browse all six stake rooms. Each room card shows the blinds, minimum buy-in, seat fee, and rake. Click a room to see its active tables.

### Room
List of open tables in a room. Shows seats taken, pot size, and hand stage. Join an existing table or open a new one.

### Table
The live game interface:
- Community cards (flop, turn, river) and each player's seat with chip counts
- Hole cards (visible only to you, decrypted in-browser)
- Action panel - Fold, Check, Call, Raise, All-In
- Turn timer with timeout enforcement
- Real-time polling of contract state every 3 seconds

### Leaderboard
Global ranked table sorted by total winnings, with columns for hands played and hands won.

### Profile
Your personal stats: rooms you've sat in, current chip stacks, and historical performance.

---

## Game Flow

1. **Connect** - Click "Connect Wallet" and approve the Keplr prompt
2. **Browse** - Pick a stake room in the lobby
3. **Buy In** - Select an open table or open a new one; pay the seat fee + chip amount in LUNC
4. **Authorize Session** - Sign once to enable gasless in-hand actions
5. **Submit Key** - Your browser generates an ephemeral P-256 keypair; the public key is sent to the contract
6. **Dealer Deals** - The dealer encrypts your hole cards to your key and posts them on-chain
7. **Play** - Act on each street (pre-flop → flop → turn → river); the contract enforces betting rules
8. **Showdown** - The dealer reveals the RNG seed; the contract verifies and awards the pot
9. **Cash Out** - Redeem your chips for LUNC at any time you are not in a hand

---

## Smart Contract

A single CosmWasm contract on Terra Classic manages all tables, hands, balances, and the leaderboard.

**Contract address:**
```
terra1ulyyz5f2rkz94daysv6fnwzm6y9ugg48ncqtsjgyu6u0ge4sz6ks4sn99f
```

### Fee Structure

| Item | Amount |
|---|---|
| Rake | 3% of each pot (300 bps) |
| Seat fee | Varies by room (see table below) |
| Buy-in minimum | Varies by room (see table below) |

---

## Poker Rooms

All amounts in LUNC. Values are converted from uluna (÷ 1,000,000).

| Room | Small Blind | Big Blind | Min Buy-In | Seat Fee | Max Seats |
|---|---|---|---|---|---|
| Mini | 100 | 250 | 5,000 | 50 | 9 |
| Micro | 1,000 | 2,000 | 40,000 | 400 | 9 |
| Low | 10,000 | 20,000 | 400,000 | 4,000 | 9 |
| Medium | 100,000 | 200,000 | 4,000,000 | 40,000 | 9 |
| High | 1,000,000 | 2,000,000 | 40,000,000 | 400,000 | 9 |
| Whale | 5,000,000 | 10,000,000 | 200,000,000 | 2,000,000 | 9 |

---

## Cryptography

**Card Encryption**
Each player generates an ephemeral P-256 keypair in the browser (stored in sessionStorage, regenerated each hand). The dealer performs ECDH with the player's public key to derive a shared secret, then encrypts hole cards with AES-GCM. Only the intended player can decrypt.

**Provably Fair Deck**
The dealer commits to a random seed before dealing. After the hand, the seed is revealed on-chain. Anyone can verify the shuffle by replaying `SHA-256(seed)` → deterministic Fisher-Yates shuffle.

**Session Keys**
A secp256k1 keypair is generated in the browser and authorized via a single Keplr signature. Subsequent in-hand actions are signed locally - no Keplr popup per action. Keys never leave the device.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 19 + TypeScript 5.6 |
| Build tool | Vite 6.0 |
| State management | Zustand 4.5 |
| Routing | React Router 6 |
| Blockchain client | CosmJS 0.32 |
| Wallet | Keplr browser extension |
| HTTP client | Axios 1.7 |
| Icons | Lucide React |
| Smart contract | Rust / CosmWasm 1.5 |
| Linting | ESLint |

---

## Network

| Network | Chain ID | LCD | RPC |
|---|---|---|---|
| Mainnet | columbus-5 | terra-classic-lcd.publicnode.com | terra-classic-rpc.publicnode.com |

---

## Donations & Support

Want to support GreenPoker? Donate LUNC to:
```
terra1l9q4guus5vjxl84d5qea068vcen32l04jmc55w
```

---

## License

This project is open-source under the **MIT License**.

## Contributing

Contributions are welcome. Fork the repo, create a branch, and open a pull request.

## Contact & Community

- [Twitter](https://twitter.com/GreenFrndLabs)
- [Website](https://www.greenfriendlylabs.com/)

---

Together, let's build a sustainable **LUNC** future! 🌿🚀
