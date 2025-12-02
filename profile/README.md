# 0xio

A privacy-focused cryptocurrency wallet ecosystem built on the Octra blockchain network.

## Overview

0xio is a comprehensive wallet solution that enables secure management of both public and private cryptocurrency transactions on the Octra blockchain. The ecosystem includes a browser extension wallet, mobile applications, and developer tools for seamless dApp integration.

## Products

### Browser Extension Wallet (0xio_wallet)
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

**Tech Stack:**
- Vanilla JavaScript
- Chrome Extension Manifest V3
- NaCl cryptography library
- Chrome Storage API

### Mobile Applications (0xio_app)
**Status:** In Development

Native mobile wallet for iOS and Android platforms.

**Features:**
- Multi-wallet management
- Public and private token transfers
- Bulk transaction support both Public and private token transfer
- Private token claiming for encrypted transfers
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

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| **0xio_wallet** | Browser extension wallet for Chrome | Live on [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc) |
| **0xio_app** | React Native mobile application | Development |
| **0xio_SDK** | TypeScript SDK for dApp integration | Published on [npm](https://www.npmjs.com/package/@0xgery/0xio-sdk) |
| **0xio_web** | Marketing website and onboarding | Live at [0xio.xyz](https://0xio.xyz) |
| **0xio_DEX** | Decentralized exchange | Planning |

## Architecture

```
┌──────────────────────────┐       ┌──────────────────────────┐
│   0xio_wallet (Chrome)   │       │    0xio_app (Mobile)     │
│  Vanilla JS + Manifest V3│       │  React Native + TypeScript│
│  - Wallet Management     │       │  - Multi-wallet Support  │
│  - NaCl Cryptography     │       │  - Private Transfers     │
│  - Secure Storage        │       │  - QR Code Scanner       │
└───────────┬──────────────┘       └──────────┬───────────────┘
            │                                 │
            │ Extension API                   │ Direct Integration
            │                                 │
            └──────────┬──────────────────────┘
                       │
            ┌──────────▼──────────────────────┐
            │  dApps (Web Applications)       │
            │  - React, Vue, Svelte, etc      │
            └──────────┬──────────────────────┘
                       │
                       │ SDK Integration
                       │
            ┌──────────▼──────────────────────┐
            │       0xio_SDK (npm)            │
            │  - TypeScript/JavaScript        │
            │  - Wallet Connection            │
            │  - Event Management             │
            │  - Type Safety                  │
            └──────────┬──────────────────────┘
                       │
                       │ RPC/API Calls
                       │
            ┌──────────▼──────────────────────┐
            │    Network Service Layer        │
            │  - Transaction Broadcasting     │
            │  - Balance Queries              │
            │  - Private Transfer Management  │
            │  - Block Explorer               │
            └──────────┬──────────────────────┘
                       │
                       │
            ┌──────────▼──────────────────────┐
            │      Octra Blockchain           │
            │  - Consensus Layer              │
            │  - Smart Contracts              │
            │  - Transaction Processing       │
            │  - Encrypted Private Transfers  │
            └─────────────────────────────────┘
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
- [SDK Documentation](https://github.com/0xio-xyz/docs/tree/main/sdk)
- [Getting Started Guide](https://github.com/0xio-xyz/docs/blob/main/sdk/getting-started.md)
- [API Reference](https://github.com/0xio-xyz/docs/blob/main/sdk/api-reference.md)

### For Contributors

**Prerequisites:**
- Node.js 16+
- Expo CLI (for mobile app)
- TypeScript knowledge

**Setup:**

```bash
# Clone repository
git clone https://github.com/0xio/[repository-name].git

# Browser Extension
cd 0xio_wallet
# Load unpacked extension in Chrome from this directory

# Mobile App
cd 0xio_app
npm install
npm start

# SDK Development
cd 0xio_SDK
npm install
npm run dev
```

## Security

- Mnemonic phrases stored securely using platform-native secure storage
- Private keys never leave the device
- Tap-to-copy with security warnings for sensitive data
- Wallet data encrypted at rest
- Extension communication via secure message passing
- Rate limiting and request validation

## Technology Stack

| Component | Stack |
|-----------|-------|
| **Browser Extension** | Vanilla JavaScript, Manifest V3, NaCl, Chrome Storage API |
| **Mobile App** | React Native, Expo, TypeScript, AsyncStorage |
| **SDK** | TypeScript, Rollup, Jest |
| **Website** | HTML, CSS, JavaScript |
| **Blockchain** | Octra Network |

## Roadmap

- [x] Browser Extension V1: Live on Chrome Web Store (Key Management, Encrypted Storage)
- [x] SDK Core (v1.0): Connection, Balance Reading, & Client-side Encryption/Decryption
- [x] Developer Portal: Documentation & Onboarding at 0xio.xyz
- [ ]Stealth Addresses (RFC-001): Client-side disposable address layer [See RFC](https://github.com/0xio-xyz/0xio-wallet-react/issues/1)
- [ ] SDK v2 (Write Operations): Adding `signTransaction` and `broadcast` methods to enable dApps to trigger transfers (Public & Private) directly.
- [ ] Mobile Beta: Native iOS & Android apps with biometric security.
- [ ] Cross-Browser Support: Porting extension to Firefox & Edge.
- [ ] 0xio DEX: The first encrypted AMM for the Octra network.
- [ ] Mobile-dApp Deep Linking: Seamless mobile browser-to-wallet connections

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
