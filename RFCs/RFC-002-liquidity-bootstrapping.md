# RFC-002: Liquidity Bootstrapping Mechanism

## 📋 Metadata
- **Status**: Draft
- **Created**: 2026-01-28
- **Authors**: Work Bitcoin Protocol Team
- **Related**: [RFC-001](./RFC-001-sybil-resistance.md)
- **Discussions**: *[GitHub Issue #2]*

## 🎯 Abstract

This RFC proposes a mechanism to bootstrap initial liquidity for local work tokens, solving the "chicken-and-egg" problem where both Bitcoin liquidity and token demand must exist simultaneously.

## 🔍 Problem Statement

### The Liquidity Bootstrap Challenge
For a local work token (LWT) to be useful:
1. **Workers** want assurance they can redeem tokens for Bitcoin
2. **Employers** want assurance tokens have value for paying workers
3. **Market makers** need incentives to provide initial liquidity
4. **Community** needs sustainable liquidity without external dependency

### Specific Constraints
1. **No premine/founders**: Avoid centralization and rent-seeking
2. **Progressive decentralization**: Start simple, become trust-minimized
3. **Capital efficiency**: Maximize Bitcoin utility
4. **Attack resistance**: Prevent manipulation during bootstrap

## 💡 Proposed Solution: Fractal Liquidity Pools

### Core Concept: Nested Bonding Curves

Global Bitcoin Reserve
↓
Community Liquidity Pool (CLP)
↓
Individual Work Token Pools (per worker/employer pair)


### Phase 1: Seed Liquidity (Months 1-3)

Mechanism: "Matching Pool"

    Early depositors get bonus tokens (1.1x multiplier)

    Matching funded by protocol fee (1% of transactions)

    Time-limited: 90-day bootstrap period

    Cap per depositor: 0.1 BTC max to prevent whale dominance


### Phase 2: Bonding Curve AMM (Months 4-12)

  Formula: x * y = k (Constant Product)
Where:

    x = Bitcoin reserves

    y = Local Work Token supply

    k = Constant (adjusts with deposits/withdrawals)

Implementation: Taproot Assets + Lightning Pool


### Phase 3: Cross-Community Liquidity (Year 2+)

Federated AMM:

    Multiple community pools connected

    Cross-community swaps enabled

    Shared liquidity for stability


## 🏗️ Implementation Details

### Smart Contract Structure (Taproot Assets)
```mermaid
graph TB
    A[Bitcoin Deposit] --> B[Collateral Manager]
    B --> C{Minting Logic}
    C --> D[Local Work Tokens]
    C --> E[Reserve Ratio Check]
    E --> F[90% Minimum Reserve]
    D --> G[Worker Wallet]
    G --> H[Lightning Payment]

Initial Parameters:
- Reserve ratio: 90% (0.9 BTC backing per 1.0 LWT)
- Minting fee: 0.5% (goes to liquidity incentives)
- Redemption fee: 0.5% (time-decaying over 2 years)
- Max daily redemption: 10% of pool (prevent bank runs)

Incentive Mechanisms

    Early Liquidity Provider (LP) Rewards:

        20% bonus tokens for first-month deposits

        10% bonus for second-month

        5% bonus for third-month

    Transaction Fee Distribution:

        50% to LP providers (proportional)

        30% to community fund (grants, verification)

        20% to protocol development

    Time-locked Benefits:

        LPs who lock for 6 months: +25% reward boost

        LPs who lock for 12 months: +50% reward boost

⚙️ Technical Implementation
Component 1: Collateral Manager

class CollateralManager:
    def mint_tokens(btc_deposit: sats) -> (lwt_amount, receipt):
        # Check reserve ratio
        # Mint Taproot Assets
        # Update liquidity pool
        # Return tokens and proof
        
    def redeem_tokens(lwt_amount: int) -> (btc_amount, proof):
        # Check daily limits
        # Calculate redemption value
        # Burn Taproot Assets
        # Send Bitcoin via Lightning

class CollateralManager:
    def mint_tokens(btc_deposit: sats) -> (lwt_amount, receipt):
        # Check reserve ratio
        # Mint Taproot Assets
        # Update liquidity pool
        # Return tokens and proof
        
    def redeem_tokens(lwt_amount: int) -> (btc_amount, proof):
        # Check daily limits
        # Calculate redemption value
        # Burn Taproot Assets
        # Send Bitcoin via Lightning

Component 2: Liquidity Pool Oracle

    Tracks real-time reserve ratios

    Adjusts minting/redemption parameters

    Provides transparency dashboard

    Triggers emergency pauses if <80% reserve

Component 3: Incentive Distributor

    Calculates LP rewards

    Distributes via Lightning

    Maintains reward history on Nostr

🔒 Security Considerations
Risk 1: Bank Run

Mitigation:

    Daily redemption limits (10% of pool)

    Time-delayed large withdrawals (72h for >1 BTC)

    Emergency pause functionality (multisig governed)

Risk 2: Oracle Manipulation

Mitigation:

    Multiple price feed oracles

    Time-weighted average prices

    Dispute period for anomalies

Risk 3: Contract Bugs

Mitigation:

    Formal verification of critical contracts

    Bug bounty program

    Gradual deployment (testnet → small mainnet → scale)

📊 Expected Outcomes
Phase 1 Goals (0-3 months):

    1-5 BTC total liquidity

    50-100 active users

    <24h liquidity for small payments

Phase 2 Goals (4-12 months):

    5-50 BTC liquidity

    500-1000 active users

    <1h liquidity for medium payments

Phase 3 Goals (Year 2+):

    50-500 BTC liquidity

    Cross-community liquidity

    <10min liquidity for all payments

❓ Open Questions

    Initial capital: Where do first BTC deposits come from?

    Governance: Who adjusts parameters over time?

    Legal status: Are these securities in any jurisdiction?

    Insurance: How to handle catastrophic hacks?

🔬 Research Directions

    Dynamic bonding curves that adjust based on usage

    ZK-proofs for private liquidity provision

    Cross-chain liquidity (if needed)

    Game theory models for optimal incentive design

This RFC is in draft status - feedback welcome via GitHub Issues

