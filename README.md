# Attenomics: Revolutionizing the Attention Economy

## Quick Access
**App Access Codes:**
- WWPASH
- MJC2P5
- 9K8R2W
- ULUS8F

## Project Overview
Attenomics is a groundbreaking blockchain platform that transforms how attention is valued, measured, and transacted in the digital economy. By tokenizing engagement and creating transparent metrics, the platform establishes a fair marketplace where creators, audiences, and brands can interact with increased trust and efficiency.

## Platform Models

### Attenomics Core Model
![image](https://github.com/user-attachments/assets/1eae8dfe-470c-49ea-81de-eceb3ab6bf7a)

Attenomics operates at the intersection of three key pillars:
- **Creator Tokens**: Enabling creators to monetize their influence directly through custom tokenomics
- **Incentivizing Honest Engagement**: Rewarding genuine user interactions across multiple platforms
- **Visual Layer for Attention Distribution**: Providing transparent analytics on engagement metrics

### Architecture Overview
![image](https://github.com/user-attachments/assets/60eacd37-e2f9-4cd7-8fcc-b8cff07d3c4d)

The platform bridges social media platforms with blockchain technology:
- **Social Layer**: Connects to multiple platforms to gather engagement data
- **Attenomics Layer**: Processes and validates attention data through verifiable mechanisms
- **Public Blockchain**: Records tokenized attention and distributes rewards transparently

## Technical Components
![image](https://github.com/user-attachments/assets/fcd43e2f-cd65-4417-a6e1-0c0a40b3db57)

Our solution consists of three integrated components:
- **Off-Chain Verifiable Component**: Processes social data and verifies genuine engagement
- **Intermediary Component**: Bridges verified attention data to the blockchain with fraud protection
- **On-Chain Tokenization Component**: Manages token creation, distribution, and marketplace functions

## Core Workflows

### 1. Attention Data Collection
- The system periodically fetches tweets and replies from creators
- It analyzes the content using LLM to determine attention metrics
- The metrics are stored in the database for later use in token distribution

### Sequence Diagram (Simplified)
```
┌────────┐          ┌─────────┐          ┌─────┐          ┌─────────┐
│ Cron   │          │ Twitter │          │ LLM │          │ Destore │
│ Job    │          │ API     │          │     │          │         │
└────┬───┘          └────┬────┘          └──┬──┘          └────┬────┘
     │     Trigger       │                  │                  │
     │─────────────────> │                  │                  │
     │                   │                  │                  │
     │    Fetch Tweets   │                  │                  │
     │────────────────>  │                  │                  │
     │                   │                  │                  │
     │   Return Tweets   │                  │                  │
     │<────────────────  │                  │                  │
     │                   │                  │                  │
     │                   │  Analyze Content │                  │
     │─────────────────────────────────────>│                  │
     │                   │                  │                  │
     │                   │  Return Analysis │                  │
     │<─────────────────────────────────────│                  │
     │                   │                  │                  │
     │                   │                  │   Store Metrics  │
     │───────────────────────────────────────────────────────> │
     │                   │                  │                  │
     │                   │                  │   Confirm Save   │
     │<─────────────────────────────────────────────────────── │
┌────┴───┐          ┌────┴────┐          ┌──┴──┐          ┌────┴────┐
│ Cron   │          │ Twitter │          │ VerLLM│        │ DESTORE │
│ Job    │          │ API     │          │     │          │         │
└────────┘          └─────────┘          └─────┘          └─────────┘
```

## Implementation Status
The project is currently deployed on the Sonic testnet, with transaction evidence available at:
- **Creator Token contract on Sonics Blaze Testnet**: [https://testnet.sonicscan.org/token/0xea04f8c64d0cd553b1791f9c1a6132641a0645e2?a=0xe217998ac130485ce5f993682eedace79daf08ed](https://testnet.sonicscan.org/token/0xea04f8c64d0cd553b1791f9c1a6132641a0645e2?a=0xe217998ac130485ce5f993682eedace79daf08ed)
- **Example Token**: [https://testnet.sonicscan.org/tx/0xb3f3cdf80d98955d444fb3d0846049be2af26aa34151e1f13b90512ad30aa1e5](https://testnet.sonicscan.org/tx/0xb3f3cdf80d98955d444fb3d0846049be2af26aa34151e1f13b90512ad30aa1e5)

## Technical Architecture

### Core Smart Contract System
The Attenomics platform is built on a sophisticated system of interconnected smart contracts:

#### AttenomicsCreatorEntryPoint.sol
- Acts as the primary gateway for creators to join the ecosystem
- Mints non-transferable NFTs that represent creator profiles and their associated tokens
- Maintains registry mappings between creator handles, token contracts, and NFT IDs
- Controls AI agent authorization through an allowlist mechanism

#### CreatorToken.sol
- Implements customized ERC20 tokens unique to each creator
- Orchestrates the deployment of three sub-contracts:
  - SelfTokenVault (creator's vested tokens)
  - BondingCurve (market trading mechanism)
  - CreatorTokenSupporter (community token distribution)
- Configurable token allocation with percentage-based distribution

#### BondingCurve.sol
- Implements a sophisticated linear bonding curve pricing model
- Manages buy/sell operations with protocol fees
- Formula: `costUnits = normAmount * BASE_PRICE + SLOPE * (normSupply * normAmount + (normAmount*(normAmount-1))/2)`
- Decouples pricing mechanism from actual token balances using purchaseMarketSupply
- Includes detailed transaction logging with ETH/USD equivalents

#### SelfTokenVault.sol
- Manages creator tokens with configurable vesting schedules
- Implements time-based token release with immediate and locked portions
- Parameters include dripPercentage, dripInterval, lockTime, and lockedPercentage
- Provides withdrawal mechanisms that respect the vesting schedule

#### CreatorTokenSupporter.sol
- Distributes tokens to community members over time
- Controlled by authorized AI agents that determine distribution patterns
- Implements signature verification for secure off-chain distribution commands
- Prevents double-spending with hash tracking

#### GasliteDrop.sol
- Highly optimized contract for efficient token distribution
- Uses assembly code to minimize gas costs for batch transfers
- Supports ERC20, ERC721, and ETH distributions
- Critical for scalable operations with many recipients

### AI Agent Integration
A distinctive feature of Attenomics is its integration of AI agents:
- Each creator must associate with an approved AI agent
- AI agents authorize and manage token distribution
- Off-chain signature verification ensures secure operations
- AI agents can analyze engagement metrics to inform distribution

## Technical Innovations

### Gas Optimization Techniques
- Named imports to reduce bytecode size
- Custom errors instead of string errors (saves ~50 bytes per error)
- Assembly-level optimizations in GasliteDrop
- Careful state management to minimize storage operations

### Security Mechanisms
- Non-transferable NFTs for robust creator identity
- ECDSA signature verification for distribution authorization
- Hash-based prevention of double-spending
- Strict validation of configuration parameters

### Transparent Tokenomics
- Clear pricing formulas with published constants
- Configurable fee structures
- Detailed logging of all financial transactions
- Separate tracking of market supply and protocol fees

## Technical Challenges Addressed

### Token Distribution Efficiency
- Traditional airdrops are gas-intensive
- GasliteDrop contract reduces costs by ~60% through assembly optimizations
- Batch processing minimizes transaction overhead

### Creator Vesting Complexity
- Vesting schedules must balance creator liquidity with long-term alignment
- Configurable parameters allow for customized vesting strategies
- Time-based dripping ensures gradual token distribution

### Bonding Curve Mathematics
- Determining optimal curve parameters for sustainable tokenomics
- Normalizing values to prevent precision errors
- Managing effective supply separate from actual token balances

### Secure AI Agent Authorization
- Preventing unauthorized AI agents from participating
- Secure signature verification for distribution commands
- Protection against replay attacks with hash tracking

## Market Problem Solved
Attenomics addresses critical inefficiencies in the current attention economy:
- **Lack of Transparency**: Most platforms obscure engagement metrics
- **Value Capture Asymmetry**: Platforms capture most value, leaving creators undercompensated
- **Engagement Verification**: Difficulty distinguishing genuine from artificial engagement
- **Monetization Barriers**: High thresholds for creator monetization

By using blockchain to tokenize attention with verifiable metrics, Attenomics creates a more equitable system where:
- Creators receive fair compensation for generating engagement
- Audiences can support creators directly and participate in their success
- Brands can access transparent metrics for partnership decisions
- AI agents provide verification and optimization services

## Future Development Roadmap
The contracts include provisions for:
- Protocol fee adjustments for sustainability
- Additional AI agent capabilities
- Enhanced distribution mechanisms
- Cross-platform engagement verification

## Technical Differentiators
- **AI-Verified Engagement**: Unlike other social tokens, Attenomics uses AI to verify genuine engagement
- **Gas-Optimized Distribution**: Advanced assembly techniques for efficient token transfers
- **Configurable Tokenomics**: Flexible parameters for different creator needs
- **Non-Transferable Identity**: Robust creator verification through non-transferable NFTs
- **Transparent Pricing Mechanism**: Fully visible bonding curve calculations

## App Screenshots

### Dashboard View
![image](https://github.com/user-attachments/assets/8f9010ab-43ac-4127-a14f-2302b4db1bc0)

### Creator Profile
![image](https://github.com/user-attachments/assets/14c3af54-affc-42c8-9a4c-6d86a0fb6e09)

### Token Market
![image](https://github.com/user-attachments/assets/a40b2e23-3897-4bbe-8424-462104d80104)

### Competition  Panel
![image](https://github.com/user-attachments/assets/3d8a3762-3551-4511-aedb-c8ea0af2733c)



This comprehensive system represents a significant advancement in blockchain-based social platforms, creating a more transparent and equitable attention economy.
