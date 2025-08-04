# BitCreator Protocol

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Stacks](https://img.shields.io/badge/Stacks-2.1+-orange.svg)
![Clarity](https://img.shields.io/badge/Clarity-2.0-purple.svg)

## Bitcoin-Native Creator Economy Platform

BitCreator transforms digital content creation through Bitcoin's security and Stacks' programmability, establishing a trustless ecosystem where creators earn through genuine engagement while building verifiable on-chain reputation.

## 🌟 Overview

Leveraging Bitcoin's immutable security via Stacks Layer 2, BitCreator creates the first truly decentralized creator monetization protocol. The platform combines algorithmic reputation scoring, engagement-based rewards, and NFT-backed membership systems to establish sustainable creator economies without intermediaries.

### Core Innovation

- **Time-decay reputation mechanics** ensuring active participation
- **Microtransaction-powered engagement** rewards with anti-spam protection  
- **Tiered NFT membership system** with governance and revenue rights
- **Creator-controlled monetization** parameters and earning thresholds
- **Bitcoin-finalized transparency** with Stacks programmability
- **Treasury management** with emergency controls and governance features

## 🏗️ Architecture

### Smart Contract Components

#### State Management

- **User Profiles**: Reputation scores, activity tracking, NFT ownership
- **Creator Settings**: Monetization parameters, reward distributions
- **Engagement History**: Anti-spam protection and interaction tracking
- **Membership Tiers**: Hierarchical access and benefit systems

#### NFT Systems

- **Reputation NFTs**: On-chain certificates of creator credibility
- **Membership NFTs**: Tiered access tokens with governance rights

#### Economic Model

- **Reputation Scoring**: Time-decay algorithm with activity incentives
- **Engagement Rewards**: Microtransaction-based creator compensation
- **Tip Economy**: Direct creator support with reputation bonuses

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) >= 1.7.0
- [Node.js](https://nodejs.org/) >= 16.0.0
- [Stacks CLI](https://docs.stacks.co/build-with-stacks/cli)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/sambo-tldr/bit-creator.git
   cd bit-creator
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Check contract syntax**

   ```bash
   clarinet check
   ```

4. **Run tests**

   ```bash
   npm test
   ```

### Project Structure

```text
bit-creator/
├── contracts/
│   └── bit-creator.clar         # Main protocol contract
├── tests/
│   └── bit-creator.test.ts      # Comprehensive test suite
├── settings/
│   ├── Devnet.toml             # Development network config
│   ├── Testnet.toml            # Testnet configuration
│   └── Mainnet.toml            # Production settings
├── Clarinet.toml               # Project configuration
└── README.md                   # Documentation
```

## 🔧 Development

### Running Tests

Execute the full test suite:

```bash
npm test
```

Run contract checks:

```bash
clarinet check
```

### Local Development

Start a local development environment:

```bash
clarinet console
```

Deploy to devnet:

```bash
clarinet deploy --devnet
```

## 📖 API Reference

### Core Functions

#### User Management

- **`initialize-user-profile()`**
  - Creates a new user profile with starting reputation
  - Returns: `(response bool uint)`

- **`setup-creator-profile(threshold: uint, reward-per-engagement: uint)`**
  - Configures creator monetization settings
  - Parameters: earnings threshold, engagement reward amount

#### Engagement System

- **`tip-creator(creator: principal, amount: uint)`**
  - Direct STX transfer to creator with reputation rewards
  - Minimum: 1 STX (1,000,000 microSTX)

- **`engage-with-creator(creator: principal, engagement-type: string-ascii 20)`**
  - Records engagement ("like", "share", "comment", "follow")
  - Includes anti-spam cooldown protection

#### NFT Minting

- **`mint-reputation-certificate()`**
  - Mints reputation NFT (requires 500+ reputation)
  - Returns unique NFT ID

- **`mint-membership-certificate()`**
  - Mints tier-based membership NFT (requires 1000+ reputation)
  - Automatically calculates appropriate tier

### Read-Only Functions

- **`get-user-profile(user: principal)`** - Retrieve user data
- **`get-current-reputation(user: principal)`** - Calculate time-decayed reputation
- **`get-membership-tier(tier-id: uint)`** - Get tier information
- **`calculate-tier-for-reputation(reputation: uint)`** - Determine membership tier

### Administrative Functions

- **`set-membership-tier(...)`** - Configure tier parameters (owner only)
- **`pause-contract()`** / **`unpause-contract()`** - Emergency controls
- **`emergency-withdraw(amount: uint)`** - Treasury management

## 🎯 Usage Examples

### Initialize User Profile

```clarity
;; Create new user profile
(contract-call? .bit-creator initialize-user-profile)
```

### Setup Creator Profile

```clarity
;; Configure creator settings
(contract-call? .bit-creator setup-creator-profile u5000000 u100000)
;; Threshold: 5 STX, Reward: 0.1 STX per engagement
```

### Tip a Creator

```clarity
;; Send 2 STX tip to creator
(contract-call? .bit-creator tip-creator 'SP1234...CREATOR u2000000)
```

### Engage with Content

```clarity
;; Like creator's content
(contract-call? .bit-creator engage-with-creator 'SP1234...CREATOR "like")
```

## 🏆 Membership Tiers

| Tier | Name | Min Reputation | Benefits |
|------|------|----------------|----------|
| 1 | Bronze Creator | 1,000 | Basic creator tools and community access |
| 2 | Silver Creator | 2,000 | Enhanced monetization tools + priority support |
| 3 | Gold Creator | 5,000 | Premium features + governance participation |
| 4 | Platinum Creator | 8,000 | Full protocol access + revenue sharing rights |

## 💰 Economic Parameters

### Reputation System

- **Starting Reputation**: 100 points
- **Maximum Reputation**: 10,000 points
- **Decay Period**: 144 blocks (~24 hours)
- **Engagement Rewards**: 25-100 points
- **Tip Bonus**: 50-100 points

### Engagement Mechanics

- **Minimum Tip**: 1 STX
- **Cooldown Period**: 6 blocks (~1 hour)
- **Valid Engagement Types**: like, share, comment, follow

## 🔒 Security Features

### Anti-Spam Protection

- Time-based engagement cooldowns
- Reputation-gated NFT minting
- Transaction amount validation

### Administrative Controls

- Contract pause functionality
- Emergency fund withdrawal
- Owner-only configuration updates

### Economic Safeguards

- Maximum reputation caps
- Threshold-based rewards
- Balance verification checks

## 🧪 Testing

The project includes comprehensive tests covering:

- **User Profile Management**: Creation, updates, reputation tracking
- **Creator Economics**: Tip processing, engagement rewards
- **NFT Systems**: Minting, metadata, ownership
- **Administrative Functions**: Security, configuration
- **Edge Cases**: Error handling, boundary conditions

Run specific test categories:

```bash
# Unit tests
npm run test:unit

# Integration tests  
npm run test:integration

# Coverage report
npm run test:coverage
```

## 🚦 Deployment

### Testnet Deployment

1. Configure testnet settings in `settings/Testnet.toml`
2. Deploy contract:

   ```bash
   clarinet deploy --testnet
   ```

### Mainnet Deployment

1. Review mainnet configuration in `settings/Mainnet.toml`
2. Perform final security audit
3. Deploy to mainnet:

   ```bash
   clarinet deploy --mainnet
   ```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Write tests for new functionality
4. Ensure all tests pass: `npm test`
5. Submit a pull request

### Code Standards

- Follow Clarity best practices
- Include comprehensive test coverage
- Document public functions
- Use descriptive variable names

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built for the future of decentralized content creation on Bitcoin infrastructure.**

*Powered by Stacks and secured by Bitcoin.*
