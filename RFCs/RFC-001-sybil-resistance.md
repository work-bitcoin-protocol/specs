# RFC-001: Sybil Resistance Mechanisms

## Metadata
- **Status**: Draft
- **Created**: 2024-01-28
- **Authors**: Work Bitcoin Protocol Team
- **Discussions**: *[GitHub Issue #1]*

## Abstract

This RFC explores mechanisms to prevent Sybil attacks in the Work Bitcoin Protocol, where a single entity creates multiple fake identities to exploit the work-to-Bitcoin system.

## Problem Statement

### The Sybil Attack Vector
In a system that converts verifiable human work to Bitcoin:
1. **Cost of attack**: Creating fake identities must be more expensive than rewards
2. **Detection difficulty**: Fake work must be indistinguishable from real work
3. **Scalability**: Solution must work for communities of 100 to 100,000+ people

### Specific Challenges for WBP
1. **Privacy requirement**: Minimal personal data collection
2. **Global accessibility**: Must work without government ID in all regions
3. **Cost constraints**: Verification must be cheap enough for small work payments
4. **Decentralization**: No single point of trust or failure

## Existing Approaches

### 1. Proof-of-Personhood Protocols
- **BrightID**: Social graph verification, but requires existing connections
- **Idena**: Proof-of-personhood via CAPTCHAs, but AI vulnerability
- **Worldcoin**: Orb biometrics, but hardware dependency and privacy concerns

### 2. Reputation & Trust Graphs
- **Web of Trust**: PGP-style, slow to bootstrap
- **Nostr Relays**: Decentralized, but Sybil vulnerable in early stages
- **Trust-at-distance**: Attenuation through multiple hops

### 3. Physical Verification
- **In-person meetups**: High trust, low scalability
- **Video verification**: Moderate scalability, privacy concerns
- **Hardware tokens**: Costly, distribution challenges

### 4. Financial Bonds
- **Staking**: Capital requirement excludes the poor
- **Bonding curves**: Works for tokens but not initial identity

## Proposed Solutions

### Hybrid Model: "Local Trust, Global Verification"

#### Component 1: Local Web of Trust (LWT)

Each community bootstraps with:

    3-5 trusted "seed verifiers" (community leaders)

    Each seed can verify 10 new members in-person

    Each verified member can verify 3 others

    Maximum verification chain: 3 hops from seed

    
**Advantages**: 
- Rapid local bootstrap
- Physical trust foundation
- Privacy preserved within community

**Disadvantages**:
- Requires initial trusted seeds
- Limited to local communities

#### Component 2: Cross-Community Verification (CCV)

Using Nostr as decentralized identity layer:

  Each user has a Nostr public key

    Verification events are published to relays

    Trust scores calculated across communities

    Sybil detection via graph analysis


**Implementation**:
```json
{
  "kind": 30078,  // WBP Verification
  "pubkey": "user_pubkey",
  "content": "",
  "tags": [
    ["verifier", "verifier_pubkey"],
    ["community", "community_id"],
    ["method", "in-person"],
    ["expires", "2024-06-28"],
    ["score", "0.95"]
  ]
}

Component 3: Periodic Re-verification

    Tier 1 (low trust): Verify every 3 months

    Tier 2 (medium trust): Verify every 6 months

    Tier 3 (high trust): Verify yearly

    Verification can be: in-person, video, or multi-party

Component 4: Work Pattern Analysis

    Detect Sybil patterns in work behavior

    Timing analysis (multiple accounts working simultaneously)

    Payment graph analysis (circular payments)

    Machine learning detection (privacy-preserving)

Verification Layer Design
┌─────────────────────────────────────┐
│      Verification Manager           │
├─────────────────────────────────────┤
│ • Identity registry (Nostr-based)   │
│ • Trust score calculator            │
│ • Expiration scheduler              │
│ • Anomaly detection                 │
│ • Dispute resolver                  │
└─────────────────────────────────────┘
         │              │              │
┌────────┴────┐ ┌──────┴──────┐ ┌─────┴─────┐
│ Local Trust │ │ Cross-Comm  │ │ Work      │
│ (In-person) │ │ (Nostr)     │ │ Patterns  │
└─────────────┘ └─────────────┘ └───────────┘

Trust Scoring Algorithm
Base Score = 0.5

+ Local Verification:
  • Seed verifier: +0.3
  • 1-hop from seed: +0.2  
  • 2-hop from seed: +0.1
  • 3-hop from seed: +0.05

+ Cross-Community:
  • Verified in 2+ communities: +0.15
  • Verified in 3+ communities: +0.25
  • No negative reports: +0.1

+ Time Based:
  • 6 months active: +0.1
  • 1 year active: +0.2
  • Recent verification: +0.05

- Penalties:
  • Work pattern anomaly: -0.2 to -0.5
  • Dispute lost: -0.3
  • Expired verification: score decays 0.1/month

MAX_SCORE = 1.0
MIN_WORK_SCORE = 0.3  # Below this, cannot receive payments

⚖️ Trade-offs & Considerations
Privacy vs. Verification

    Option A: More verification = less privacy

    Option B: Less verification = more Sybil risk

    Our choice: Hybrid - physical for bootstrap, anonymous thereafter

Decentralization vs. Efficiency

    Fully decentralized: Slow, expensive verification

    Centralized: Fast, but single point of failure

    Our choice: Federated - community-based with cross-checking

Cost vs. Security

    High security: Expensive verification processes

    Low cost: Vulnerable to Sybil attacks

    Our choice: Tiered - small payments low security, large payments high security

Implementation Roadmap
Phase 1: MVP (Months 1-3)

    Local web of trust only

    Manual verification by community admins

    Simple trust scoring

    Single community focus

Phase 2: Cross-Community (Months 4-6)

    Nostr integration for identity

    Cross-community verification events

    Automated trust scoring

    Basic anomaly detection

Phase 3: Advanced (Months 7-12)

    ZK-proofs for private verification

    Machine learning pattern detection

    Federated learning for Sybil detection

    Decentralized dispute resolution

Open Questions

    Initial seed selection: How to choose initial verifiers without central authority?

    Verification cost: Who pays for physical verification?

    False positives: How to handle legitimate users flagged as Sybil?

    Recovery: How to recover from compromised verification seeds?

    Legal considerations: KYC/AML implications in different jurisdictions?

🔬 Research Needed

    Graph analysis: Optimal parameters for trust attenuation

    Game theory: Economic incentives for honest verification

    Privacy tech: Using zk-SNARKs for private attestation

    Attack simulations: Cost analysis of various Sybil attacks

Success Metrics
Primary Metrics

    Sybil detection rate: >95% detection of fake identities

    False positive rate: <5% legitimate users flagged

    Verification cost: <$0.50 per user annualized

    Time to verify: <48 hours for new users

Secondary Metrics

    User retention after verification

    Community growth rate

    Dispute resolution time

Alternatives Considered
Alternative A: Pure Financial Bond

    Each user stakes $10 in Bitcoin

    Sybils lose stake if detected

    Rejected: Excludes unbanked/poor users

Alternative B: Government ID

    Use national ID systems

    Rejected: Privacy concerns, excludes refugees/undocumented

Alternative C: Pure Social Graph

    Like BrightID, rely on existing connections

    Rejected: Slow bootstrap, excludes isolated individuals

Recommendation

Implement the Hybrid Model with:

    Local web of trust for bootstrap

    Nostr-based cross-community verification

    Tiered security based on payment size

    Gradual decentralization over time

This balances privacy, accessibility, and security while allowing iterative improvement based on real-world usage.

## Community Feedback from Bitcoin Stack Exchange

References

    Douceur, J. R. (2002). "The Sybil Attack"

    Bitcoin Whitepaper (2008)

    Nostr Protocol Specification

    BrightID Whitepaper

    Idena Documentation

    Human work protocol(2026) el problema sybil explicación visual (RFC-001) https://youtu.be/Om-gXoy7s-A

Voting

[To be filled during RFC review process]

    Accept as proposed

    Accept with modifications

    Reject

    Defer for more research



---

### **5. LICENSE**
```text
MIT License

Copyright (c) 2024 Work Bitcoin Protocol

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
