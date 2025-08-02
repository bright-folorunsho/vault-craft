# VaultCraft Protocol

## Overview

VaultCraft is a revolutionary yield-farming protocol built on the Stacks blockchain that transforms traditional staking into a sophisticated yield optimization platform. The protocol enables users to deposit STX tokens into intelligent vaults that automatically compound rewards based on lock duration and stake size.

## Key Features

### 🏆 Three-Tier Membership System

- **Bronze Tier (Level 1)**: 1M+ STX stake, 1x reward multiplier
- **Silver Tier (Level 2)**: 5M+ STX stake, 1.5x reward multiplier  
- **Gold Tier (Level 3)**: 10M+ STX stake, 2x reward multiplier

### ⏰ Time-Lock Rewards

- **No Lock**: Base rewards
- **1 Month Lock**: 1.25x multiplier
- **2 Month Lock**: 1.5x multiplier

### 🗳️ Decentralized Governance

- Community-driven protocol evolution
- Proposal creation and voting system
- Voting power based on stake amount

### 🛡️ Security Features

- Emergency pause functionality
- Mandatory cooldown periods for unstaking
- Robust validation and error handling

## Smart Contract Architecture

### Core Components

#### Data Structures

- **UserPositions**: Comprehensive tracking of user stakes and rewards
- **StakingPositions**: Individual staking position details
- **TierLevels**: Configurable tier system parameters
- **Proposals**: Governance proposal management

#### Key Functions

- `stake-stx`: Deposit STX with optional time-lock
- `initiate-unstake`: Begin unstaking process
- `complete-unstake`: Finalize unstaking after cooldown
- `create-proposal`: Submit governance proposals
- `vote-on-proposal`: Cast votes on proposals

## Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) for local development
- Node.js for running tests
- Stacks wallet for mainnet deployment

### Installation

1. Clone the repository:

```bash
git clone https://github.com/bright-folorunsho/vault-craft.git
cd vault-craft
```

2. Install dependencies:

```bash
npm install
```

3. Run contract checks:

```bash
clarinet check
```

4. Run tests:

```bash
npm test
```

## Usage Examples

### Staking STX

```clarity
;; Stake 5M STX with 1-month lock period
(contract-call? .vault-craft stake-stx u5000000 u4320)
```

### Creating a Governance Proposal

```clarity
;; Create a proposal for protocol improvement
(contract-call? .vault-craft create-proposal 
  u"Increase base reward rate to 6%" 
  u1440)
```

### Voting on Proposals

```clarity
;; Vote in favor of proposal #1
(contract-call? .vault-craft vote-on-proposal u1 true)
```

## Contract Configuration

### Initial Setup

The contract must be initialized by the owner to configure tier levels:

```clarity
(contract-call? .vault-craft initialize-contract)
```

### Key Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Minimum Stake | 1,000,000 µSTX | Minimum amount to stake |
| Base Reward Rate | 5% | Annual base reward rate |
| Cooldown Period | 1,440 blocks | ~24 hours unstaking delay |
| Bronze Tier | 1M+ STX | Entry-level membership |
| Silver Tier | 5M+ STX | Mid-tier membership |
| Gold Tier | 10M+ STX | Premium membership |

## Reward Calculation

Rewards are calculated using the formula:

```
Rewards = (Stake × Base Rate × Tier Multiplier × Lock Multiplier × Blocks) / Normalizer
```

Where:

- **Stake**: Amount of STX staked
- **Base Rate**: 5% annual rate (500 basis points)
- **Tier Multiplier**: 1x, 1.5x, or 2x based on tier
- **Lock Multiplier**: 1x, 1.25x, or 1.5x based on lock period
- **Blocks**: Number of blocks since last claim
- **Normalizer**: 14,400,000 (for annualized calculation)

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 1000 | ERR-NOT-AUTHORIZED | Unauthorized access attempt |
| 1001 | ERR-INVALID-PROTOCOL | Invalid protocol parameters |
| 1002 | ERR-INVALID-AMOUNT | Invalid amount specified |
| 1003 | ERR-INSUFFICIENT-STX | Insufficient STX balance |
| 1004 | ERR-COOLDOWN-ACTIVE | Cooldown period still active |
| 1005 | ERR-NO-STAKE | No active stake found |
| 1006 | ERR-BELOW-MINIMUM | Amount below minimum threshold |
| 1007 | ERR-PAUSED | Contract is paused |

## Security Considerations

### Access Controls

- Owner-only functions for pausing/resuming
- Voting power requirements for proposal creation
- Validation of all user inputs

### Emergency Mechanisms

- Contract pause functionality
- Emergency mode for critical situations
- Time-locked unstaking process

### Best Practices

- Always validate function parameters
- Use proper error handling
- Implement comprehensive testing

## Testing

The protocol includes comprehensive test coverage:

```bash
# Run all tests
npm test

# Run specific test files
npm test -- vault-craft.test.ts
```

Test coverage includes:

- Staking and unstaking flows
- Tier system calculations
- Governance proposal lifecycle
- Emergency pause mechanisms
- Error condition handling

## Deployment

### Testnet Deployment

1. Configure testnet settings in `settings/Testnet.toml`
2. Deploy using Clarinet:

```bash
clarinet deploy --testnet
```

### Mainnet Deployment

1. Configure mainnet settings in `settings/Mainnet.toml`
2. Deploy using Clarinet:

```bash
clarinet deploy --mainnet
```

## Contributing

We welcome contributions to VaultCraft! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch
3. Write comprehensive tests
4. Ensure all tests pass
5. Submit a pull request

### Development Workflow

1. Make changes to contracts in `contracts/`
2. Update tests in `tests/`
3. Run `clarinet check` to validate syntax
4. Run `npm test` to execute test suite
5. Update documentation as needed

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Roadmap

### Phase 1 (Current)

- ✅ Core staking functionality
- ✅ Three-tier reward system
- ✅ Time-lock mechanisms
- ✅ Basic governance

### Phase 2 (Planned)

- 🔄 Advanced governance features
- 🔄 Liquid staking tokens
- 🔄 Cross-protocol integrations
- 🔄 Enhanced analytics

### Phase 3 (Future)

- 📋 Advanced yield strategies
- 📋 Multi-asset support
- 📋 Layer 2 scaling solutions
- 📋 Mobile application

## Acknowledgments

- Built on [Stacks](https://stacks.co) blockchain
- Powered by [Clarity](https://clarity-lang.org) smart contracts
- Developed with [Clarinet](https://github.com/hirosystems/clarinet)
