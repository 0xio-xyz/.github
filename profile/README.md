# 0xio

A privacy-focused cryptocurrency wallet ecosystem built on the Octra blockchain network.

## Overview

0xio is a comprehensive wallet solution that enables secure management of both public and private cryptocurrency transactions on the Octra blockchain. The ecosystem includes a browser extension wallet, mobile applications, and developer tools for seamless dApp integration.

## Products

### Browser Extension Wallet
**Status:** Live on Chrome Web Store

The 0xio Wallet browser extension provides a secure, user-friendly interface for managing your Octra blockchain assets directly in your browser.

**Features:**
- Secure wallet management with encrypted storage
- Public and private transaction support
- Multi-wallet support
- Token management
- Transaction history
- dApp connectivity via 0xio SDK
- Network switching (mainnet/testnet)

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc)

### Mobile Applications (0xio_app)
**Status:** In Development

Native mobile wallet for iOS and Android platforms.

**Features:**
- Multi-wallet management
- Public and private token transfers
- Bulk transaction support
- Private token claiming via encrypted transfers
- Transaction history
- Theme customization (Light/Dark modes)
- Secure encrypted storage
- QR code scanning

**Tech Stack:**
- React Native + Expo
- TypeScript
- React Navigation
- Secure Storage (expo-secure-store)
- Octra blockchain integration

### Developer SDK (0xio_SDK)
**Status:** Published on npm

Official TypeScript/JavaScript SDK for integrating 0xio Wallet with decentralized applications.

**Package:** [`@0xgery/0xio-sdk`](https://www.npmjs.com/package/@0xgery/0xio-sdk)

**Features:**
- Seamless wallet connection
- Transaction management (public & private)
- Balance queries
- Event-driven architecture
- Full TypeScript support
- Framework agnostic (React, Vue, Svelte, Vanilla JS)
- Built-in extension detection with retry logic
- Production-ready with zero console noise

**Installation:**
```bash
npm install @0xgery/0xio-sdk
```

**Quick Example:**
```typescript
import { createZeroXIOWallet } from '@0xgery/0xio-sdk';

const wallet = await createZeroXIOWallet({
  appName: 'My DApp',
  autoConnect: true
});

const balance = await wallet.getBalance();
console.log('Balance:', balance.total, 'OCT');
```

### Core Wallet Library (0xio_wallet)
**Status:** Active

Python-based core wallet functionality for Octra blockchain operations.

**Features:**
- Wallet generation from mnemonic
- Public transaction creation and signing
- Private transaction encryption/decryption
- Octra blockchain API integration
- Balance and transaction queries

**Tech Stack:**
- Python 3.8+
- Octra SDK
- Cryptography libraries

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| **0xio_app** | React Native mobile application | Development |
| **0xio_SDK** | TypeScript SDK for dApp integration | Published |
| **0xio_wallet** | Python core wallet library | Active |
| **0xio_web** | Marketing website and onboarding | Live at [0xio.xyz](https://0xio.xyz) |
| **0xio_DEX** | Decentralized exchange | Planning |

## Architecture

```
┌─────────────────────────────────────────┐
│     Browser Extension / Mobile App      │
│  (React/React Native + TypeScript)      │
│  - UI/UX                                │
│  - State Management                     │
│  - Secure Storage                       │
└──────────────┬──────────────────────────┘
               │
               │ SDK Integration
               │
┌──────────────▼──────────────────────────┐
│          0xio_SDK (npm)                 │
│  - dApp Connection Layer                │
│  - Event Management                     │
│  - Type Safety                          │
└──────────────┬──────────────────────────┘
               │
               │ API Calls
               │
┌──────────────▼──────────────────────────┐
│       Network Service Layer             │
│  - Transaction Broadcasting             │
│  - Balance Queries                      │
│  - Private Transfer Management          │
└──────────────┬──────────────────────────┘
               │
               │
┌──────────────▼──────────────────────────┐
│          0xio_wallet Library            │
│  (Python Core)                          │
│  - Wallet Generation                    │
│  - Transaction Signing                  │
│  - Encryption/Decryption                │
└──────────────┬──────────────────────────┘
               │
               │
┌──────────────▼──────────────────────────┐
│          Octra Blockchain               │
│  - Smart Contracts                      │
│  - Transaction Processing               │
└─────────────────────────────────────────┘
```

## Key Features

### Privacy-First Design
- Private token transfers using end-to-end encryption
- Encrypted data stored on-chain with ephemeral keys
- No transaction history leakage for private transfers
- Balance encryption/decryption

### Multi-Wallet Support
- Create unlimited wallets
- Import existing wallets via private key or mnemonic
- Switch between wallets seamlessly
- Individual balance tracking per wallet

### Flexible Transaction Types
- **Public Transfers**: Standard blockchain transactions
- **Private Transfers**: Encrypted on-chain transfers
- **Bulk Transfers**: Send to multiple recipients at once
- **Claim System**: Decrypt and claim private transfers

### User Experience
- Intuitive UI/UX design
- Theme customization (Light/Dark modes)
- QR code support
- Transaction history
- Real-time balance updates

### Developer-Friendly
- Comprehensive SDK with TypeScript support
- Event-driven architecture
- Multi-framework compatibility
- Built-in error handling with retry logic
- Development mode debugging tools

## Getting Started

### For Users

**Browser Extension:**
1. Install from [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc)
2. Create or import your wallet
3. Start managing your Octra assets

**Mobile App (Coming Soon):**
- iOS: App Store (In Development)
- Android: Google Play Store (In Development)

### For Developers

**Integrate 0xio Wallet into your dApp:**

```bash
npm install @0xgery/0xio-sdk
```

```typescript
import { createZeroXIOWallet } from '@0xgery/0xio-sdk';

const wallet = await createZeroXIOWallet({
  appName: 'My Awesome DApp',
  appDescription: 'A revolutionary decentralized application',
  requiredPermissions: ['read_balance', 'send_transactions']
});

await wallet.connect();
```

**Documentation:**
- [SDK Documentation](https://github.com/0xio-xyz/docs/blob/main/sdk/README.md)
- [API Reference](https://github.com/0xio-xyz/docs/blob/main/sdk/api-reference.md)

### For Contributors

**Prerequisites:**
- Node.js 16+
- Python 3.8+
- Expo CLI (for mobile app)
- TypeScript knowledge

**Setup:**

```bash
# Clone repository
git clone https://github.com/0xio/[repository-name].git

# Mobile App
cd 0xio_app
npm install
npm start

# SDK Development
cd 0xio_SDK
npm install
npm run dev

# Core Wallet Library
cd 0xio_wallet
pip install -r requirements.txt
```

## Security

- Mnemonic phrases stored securely using platform-native secure storage
- Private keys never leave the device
- Tap-to-copy with security warnings for sensitive data
- Wallet data encrypted at rest
- Extension communication via secure message passing
- Rate limiting and request validation

## Technology Stack

| Component | Technologies |
|-----------|-------------|
| **Mobile App** | React Native, Expo, TypeScript, AsyncStorage |
| **Browser Extension** | React, TypeScript, Chrome Extension API |
| **SDK** | TypeScript, Rollup, Jest |
| **Core Library** | Python, Octra SDK, Cryptography |
| **Blockchain** | Octra Network |

## Roadmap

- [x] Browser extension wallet (Chrome)
- [x] Developer SDK with npm package
- [x] Core wallet library
- [x] Marketing website (0xio.xyz)
- [ ] Mobile applications (iOS & Android)
- [ ] Hardware wallet integration
- [ ] Multi-signature support
- [ ] NFT support
- [ ] Staking functionality
- [ ] Decentralized exchange (0xio_DEX)
- [ ] Browser extension for Firefox & Edge

## Contributing

We welcome contributions! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Community & Support

- **Website**: [0xio.xyz](https://0xio.xyz)
- **GitHub**: [@0xio](https://github.com/0xio)
- **Contact**: [Telegram](https://t.me/nullXgery)
- **Email**: team@0xio.xyz
- **Issues**: Report bugs via GitHub Issues

## License

MIT License - see individual repository LICENSE files for details.

## Acknowledgments

> **Disclaimer**: This is a community-built project for the Octra Network. It is not affiliated with, endorsed by, or maintained by the official Octra team.

---

**Important Notice**: This project is under active development. Always verify transactions and use appropriate security measures. Never share your private keys or mnemonic phrases.
