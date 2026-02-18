---

Work Bitcoin Protocol

A non-custodial protocol on Lightning Network that enables verifiable human work to be directly exchanged for Bitcoin, creating a P2P bridge between local economies and global sound money.

Problem Statement

Traditional local economies face:

· Currency depreciation: Local fiat loses value rapidly
· Limited access: No direct path to global sound money
· High fees: Remittance costs up to 10-15%
· Centralized control: Banking intermediaries required

Technical Architecture

```
graph TB
    A -->[Local Worker] --> B[Work Verification]
    B --> C[Taproot Assets Issuance]
    C --> D[Lightning Network]
    D --> E[Bitcoin Settlement]
    F[Local Employer] --> D
    G[Market Maker] --> D

    B --> H[Nostr Identity Graph]
    C --> I[Sybil Resistance Layer]
```

Core Components

1. Work Verification Layer

· Zero-knowledge proofs of work completion
· Decentralized attestation network
· Physical verification fallback

2. Asset Issuance (Taproot Assets)

· Local work tokens as Taproot Assets
· 1:1 redeemable for Bitcoin
· Non-custodial by design

3. Lightning Network Settlement

· Instant Bitcoin payments
· Sub-cent transaction fees
· Global liquidity access

4. Sybil Resistance

· Hybrid proof-of-personhood
· Trust graphs with attenuation
· Periodic physical verification

Current Status

Phase: Research & Specification

We are actively researching solutions to core challenges:

· RFC-001: Sybil Resistance Mechanisms
· RFC-002: Liquidity Bootstrapping

Documentation

· ARCHITECTURE.md - Detailed technical architecture
· CONTRIBUTING.md - How to contribute
· RFCs - Technical proposals and discussions

Getting Started

For Researchers

1. Read ARCHITECTURE.md
2. Review open RFCs
3. Join the discussion in GitHub Issues

For Developers

Coming soon: Prototype repository

Contributing

We welcome technical discussions and research contributions. Please read CONTRIBUTING.md first.

---
