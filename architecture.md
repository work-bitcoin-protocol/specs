---

Work Bitcoin Protocol - Technical Architecture

System Overview

Core Principles

· Non-custodial: Users control their keys and funds
· Bitcoin-native: Direct Bitcoin settlement, no intermediate stablecoins
· Privacy-preserving: Minimize data collection, maximize user privacy
· Censorship-resistant: No single point of failure or control

Technology Stack

Layer 1: Bitcoin

· Base settlement layer
· Taproot-enabled for efficiency
· Timechain for global state consensus

Layer 2: Lightning Network

· Instant payment layer
· LND/Core Lightning implementation
· AMP (Atomic Multi-Path Payments) for large work payments

Layer 3: Taproot Assets (Taro)

· Asset issuance layer
· Local work tokens as Taproot Assets
· 1:1 Bitcoin redemption

Auxiliary Protocols

· Nostr: Decentralized identity and reputation
· Fedimint: Community custody (future consideration)

System Components

1. Identity & Sybil Resistance Module

```
┌─────────────────────────────────────┐
│         Identity Module              │
├─────────────────────────────────────┤
│ • Nostr-based public keys            │
│ • Trust graph construction           │
│ • Attenuation scoring                │
│ • Physical verification oracle       │
│ • ZK-proofs of unique humanity       │
└─────────────────────────────────────┘
```

2. Work Verification Module

```
┌─────────────────────────────────────┐
│        Work Verification             │
├─────────────────────────────────────┤
│ • Task definition (standards)        │
│ • Proof-of-work-completion           │
│ • Multi-party attestation            │
│ • Dispute resolution mechanism       │
│ • Reputation scoring                 │
└─────────────────────────────────────┘
```

3. Asset Issuance & Management

```
┌─────────────────────────────────────┐
│          Asset Manager               │
├─────────────────────────────────────┤
│ • Taproot Assets minting             │
│ • Bitcoin collateralization          │
│ • Redemption smart contracts         │
│ • Liquidity pool management          │
│ • Cross-community exchange           │
└─────────────────────────────────────┘
```

4. Payment & Settlement Layer

```
┌─────────────────────────────────────┐
│          Payment Engine              │
├─────────────────────────────────────┤
│ • Lightning channel management       │
│ • Multi-path routing                 │
│ • Atomic swaps (Assets↔BTC)          │
│ • Fee optimization                   │
│ • Transaction monitoring             │
└─────────────────────────────────────┘
```

Transaction Flows

Flow 1: Local Work Payment

1. Worker completes verifiable task
2. Work proof submitted to network
3. Attestation by 3+ parties (including physical verifier)
4. Local tokens minted to worker's wallet
5. Worker swaps tokens for BTC via liquidity pool
6. BTC sent via Lightning to worker's wallet

Flow 2: Employer Funds Worker

1. Employer deposits BTC to community pool
2. BTC used as collateral for local token issuance
3. Employer pays worker in local tokens
4. Worker redeems tokens for BTC at any time

Security Considerations

Key Risks & Mitigations

· Collateral theft: Multi-sig custody, time locks
· Sybil attacks: Hybrid verification (physical + digital)
· Liquidity runs: Bonding curves, redemption limits
· Oracle failure: Decentralized oracle networks

Privacy Features

· CoinJoin integration for Bitcoin level
· Route blinding for Lightning
· Confidential transactions for Taproot Assets

Network Topology

Initial Deployment Model

```
Community A ── Bitcoin ── Community B
    │               │
┌───┴────┐      ┌───┴────┐
│ LN Node│      │ LN Node│
│ Assets │      │ Assets │
│ Pool   │──Swap────▶│ Pool   │
└────────┘      └────────┘
```

Future: Federated Model

```
┌─────────────────────────────────┐
│        Federation Layer          │
│ • Cross-community swaps          │
│ • Shared liquidity               │
│ • Dispute resolution             │
└─────────────────────────────────┘
              │
    ┌─────────┴─────────┐
    │                   │
┌───┴──────┐      ┌───┴──────┐
│Community │      │Community │
│    A     │      │    B     │
└──────────┘      └──────────┘
```

Scaling Considerations

Phase 1: Single Community

· One local token
· ~100-1000 users
· Manual verification

Phase 2: Multi-Community

· Cross-community swaps
· Automated verification
· ~10k users

Phase 3: Federation

· Shared liquidity pools
· Decentralized governance
· Global scale

Integration Points

Wallets Required

· Taproot Assets compatible (Joltz, etc.)
· Lightning enabled
· Nostr integration for identity

Services Needed

· Bitcoin/Lightning nodes
· Taproot Assets mint
· Oracle services for physical verification
· Indexing services for work proofs

---

This document is a living specification. Last updated: 2024
