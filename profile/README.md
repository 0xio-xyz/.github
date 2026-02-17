# 0xio

A privacy-focused cryptocurrency wallet ecosystem built on the Octra Network.

## Overview

0xio is a comprehensive wallet solution that enables secure management of both public and private cryptocurrency transactions on Octra Network. The ecosystem includes a browser extension wallet, mobile applications, and developer tools for seamless dApp integration.

## Products

### Browser Extension Wallet (0xio wallet)
**Status:** Live on Chrome Web Store (v2.1.15)

The new 0xio Wallet is a robust, high-performance browser extension rebuilt from the ground up using React and Vite. It provides a secure, user-friendly interface for managing your Octra Network assets directly in your browser.

**Features:**
- **Advanced Cryptography:** Implements industry-standard BIP39 mnemonics and HD wallet derivation.
- **Vault Architecture:** Utilizes a single encrypted vault for all account storage, protected by AES-GCM with 900,000 PBKDF2 iterations.
- **Modern Architecture:** Built with React and Vite for faster load times and a responsive UI.
- **Privacy First:** Native support for public and private (encrypted) transactions.
- **Multi-Wallet:** Create and manage up to 20 wallets per installation.
- **dApp Ready:** Seamless connectivity via the `@0xio/sdk`.
- **Supply Chain Security:** Protected against malicious npm packages using LavaMoat.

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc)

**Tech Stack:**
- **Framework:** React 18 + Vite
- **Styling:** TailwindCSS
- **Cryptography:** TweetNaCl (Ed25519), Web Crypto API (SHA-256, PBKDF2)
- **State Management:** React Context + Hooks
- **Standard:** Chrome Extension Manifest V3

> **Legacy Version:** The previous Vanilla JavaScript version of the extension has been deprecated and open-sourced for educational purposes. You can find it here: [Legacy 0xio Extension](https://github.com/0xio-xyz/Legacy/tree/main/legacy-0xio-extension).

### Mobile Applications (0xio_app)
**Status:** In Development

Native mobile wallet for iOS and Android platforms.

**Features:**
- Multi-wallet management (create, import, watch-only)
- Public and private token transfers
- Bulk transaction support (Public & Private)
- Private token claiming for encrypted transfers
- Transaction history with pending tracking
- Secure encrypted storage (TweetNaCl + AsyncStorage)
- QR code generation and sharing
- Biometric authentication (Face ID / Touch ID)
- PIN lock with auto-lock timeout
- Internationalization (English, Bahasa Indonesia, Chinese, Japanese, Korean)
- DApp browser with wallet provider injection
- Address book for saved contacts
- Dark and light theme support
- Gesture-based navigation (edge swipe for wallet switching)
- In-app token swap (coming soon)
- Hide balances toggle for privacy
- Sentry error tracking and monitoring

**Tech Stack:**
- React Native 0.81 + Expo SDK 54 (New Architecture enabled)
- TypeScript (strict mode)
- React Navigation (Stack)
- TanStack React Query for data fetching
- React Native Gesture Handler + Reanimated
- expo-secure-store, expo-local-authentication, expo-haptics
- i18next for internationalization
- Sentry for error monitoring
- Lucide icons

### Developer SDK (0xio_SDK)
**Status:** Published on npm

Official TypeScript/JavaScript SDK for integrating 0xio Wallet with decentralized applications.

**Package:** `@0xio/sdk`

**Features:**
- Seamless wallet connection and auto-reconnection
- Transaction management (public & private)
- Balance queries (public + encrypted private)
- Message signing (Ed25519)
- Transaction finality tracking (`pending`, `confirmed`, `rejected`)
- Balance encryption/decryption and private transfer claiming
- Event-driven architecture (connect, disconnect, balanceChanged, accountChanged, etc.)
- Rate limiting (50 concurrent / 20 per second) and retry with exponential backoff
- 20 RPC error codes with human-readable messages
- Full TypeScript support with strict readonly interfaces
- Framework agnostic (React, Vue, Svelte, Vanilla JS)
- Cryptographically secure request IDs (Web Crypto API)

**Installation:**
```bash
npm install @0xio/sdk
```

### 0xio DEX
**Status:** In Development

Privacy-preserving decentralized exchange for trading encrypted assets on the Octra Network.

**URL:** [dex.0xio.xyz](https://dex.0xio.xyz)

### Atlas
**Status:** Live (Beta)

High-performance blockchain visualization and analytics platform for the Octra Network.

**URL:** [atlas.0xio.xyz](https://atlas.0xio.xyz)

### Telegram Bot
**Status:** Live

Real-time wallet monitoring and notifications via Telegram.

**Bot:** [@NullXio_bot](https://t.me/NullXio_bot)

## Security & Cryptography

The 0xio wallet implements a rigorous security model based on standard cryptographic primitives and hierarchical deterministic (HD) wallet specifications.

### Key Generation and Derivation

The wallet strictly adheres to the following standards to ensure compatibility and security:

  * **Mnemonic Generation (BIP39):**
      * Generates 128-bit entropy using the Web Crypto API.
      * Produces a standard 12-word mnemonic phrase.
  * **Seed Derivation:**
      * Uses PBKDF2 with HMAC-SHA512 (2048 iterations) to derive the binary seed from the mnemonic.
  * **Hierarchical Deterministic (HD) Path:**
      * Follows a specific derivation path for the Octra network: `m/345'/0'/0'/0'/0'/0'/0'/0`.
      * Indices represent: Purpose (345) / Coin / Network / Contract / Account / Token / Subnet / Index.
  * **Signing Keys:**
      * Uses **Ed25519** (Twisted Edwards curve) for high-speed, high-security digital signatures.
      * Implemented via the `tweetnacl` library.
  * **Address Generation:**
      * Public keys are hashed using **SHA-256**.
      * The resulting hash is encoded using **Base58** and prefixed with `oct`.

### Storage Security (Vault Architecture)

Sensitive data is never stored in plain text. The wallet utilizes a "Vault" architecture:

  * **AES-GCM Encryption:** All private keys and mnemonics are bundled into a single JSON object and encrypted using AES-GCM (Advanced Encryption Standard in Galois/Counter Mode).
  * **Key Wrapping:** The encryption key for the vault is derived from the user's password using PBKDF2 (900,000 iterations) and a unique, randomly generated salt.
  * **Non-Custodial:** Private keys never leave the user's device. They are encrypted at rest within the browser's local storage and only decrypted in memory when signing a transaction.

### Security Hardening (v2.1+)

The wallet includes multiple layers of protection against common attack vectors:

  * **Password Rate Limiting:** Progressive lockout after failed password attempts (30s, 60s, 120s, etc.) to prevent brute force attacks.
  * **Wallet Reset Confirmation:** Users must type "DELETE MY WALLET" to confirm wallet deletion, preventing accidental data loss.
  * **Session Key Protection:** Session keys are kept in memory only and never stored as exportable material.
  * **DApp Connection Expiry:** Connected dApps automatically disconnect after 24 hours or when the wallet is locked.
  * **Message Origin Verification:** All postMessage communications use strict origin checking instead of wildcards.
  * **Request Replay Prevention:** Nonce-based verification prevents replay attacks on wallet requests.
  * **Automatic Migration:** Seamless vault upgrades when updating from older versions, with backwards-compatible decryption.

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| **0xio\_wallet** | React-based browser extension wallet | Live (v2.1.15) |
| **0xio\_app** | React Native mobile application | Development |
| **0xio\_SDK** | TypeScript SDK for dApp integration | Published on npm |
| **0xio\_web** | Marketing website and onboarding | Live at 0xio.xyz |
| **documentation** | Mintlify-powered docs site | Live at docs.0xio.xyz |
| **Legacy** | Archived Vanilla JS extension code | Archived |

## Architecture

```
┌──────────────────────────┐        ┌──────────────────────────┐
│   0xio_wallet (Chrome)   │        │    0xio_app (Mobile)     │
│  React + Vite + Tailwind │        │ React Native + Expo      │
│  - HD Wallet (BIP39)     │        │  - Biometric Auth        │
│  - Ed25519 Signatures    │        │  - DApp Browser          │
│  - AES-GCM Vault         │        │  - i18n (5 Languages)    │
└───────────┬──────────────┘        └──────────┬───────────────┘
            │                                  │
            │ Extension API                    │ Direct Integration
            │                                  │
            └──────────┬───────────────────────┘
                       │
           ┌───────────▼──────────────────────┐
           │   dApps (Web Applications)       │
           │  - React, Vue, Svelte, etc       │
           └───────────┬──────────────────────┘
                       │
                       │ SDK Integration
                       │
           ┌───────────▼──────────────────────┐
           │        0xio_SDK (npm)            │
           │  - TypeScript/JavaScript         │
           │  - Wallet Connection             │
           │  - Event Management              │
           └───────────┬──────────────────────┘
                       │
                       │ JSON-RPC 2.0
                       │
           ┌───────────▼──────────────────────┐
           │     Network Service Layer        │
           │  - Transaction Broadcasting      │
           │  - Balance Queries               │
           │  - Private Transfer Management   │
           └───────────┬──────────────────────┘
                       │
           ┌───────────▼──────────────────────┐
           │         Octra Network            │
           │  - Consensus Layer               │
           │  - Smart Contracts               │
           │  - Encrypted Private Transfers   │
           └──────────────────────────────────┘
```

## Key Features

### Privacy-First Design

  - Private token transfers using end-to-end encryption
  - Encrypted data stored on-chain with ephemeral keys
  - No transaction history leakage for private transfers
  - Balance encryption/decryption

### Multi-Wallet Support

  - Create up to 20 wallets per installation
  - Import existing wallets via private key or mnemonic
  - Watch-only wallet mode (view balance without private key)
  - Switch between wallets seamlessly
  - Individual balance tracking per wallet

### Flexible Transaction Types

  - **Public Transfers:** Standard blockchain transactions
  - **Private Transfers:** Encrypted on-chain transfers
  - **Bulk Transfers:** Send to up to 5 recipients at once
  - **Claim System:** Claim private transfers

### Developer-Friendly

  - Comprehensive SDK (`@0xio/sdk`) with full TypeScript support
  - Event-driven architecture with typed events
  - Multi-framework compatibility (React, Vue, Svelte, Vanilla JS)
  - Built-in error handling with retry logic and rate limiting
  - Message signing for dApp authentication

## Getting Started

### For Users

**Browser Extension:**

1.  Install the latest version from [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc).
2.  Create a new wallet (generates a new BIP39 seed) or import your existing phrase.
3.  Start managing your Octra assets with the new React-powered interface.

**Mobile App:**

  - *Coming Soon to iOS and Android.*

### For Developers

**Integrate 0xio Wallet into your dApp:**

```bash
npm install @0xio/sdk
```

```typescript
import { createZeroXIOWallet } from '@0xio/sdk';

const wallet = await createZeroXIOWallet({
  appName: 'My Awesome DApp',
  autoConnect: true
});

await wallet.connect();
```

## Technology Stack

| Component | Stack |
|-----------|-------|
| **Browser Extension** | **React, Vite, TailwindCSS, CRXJS** |
| **Cryptography** | **TweetNaCl (Ed25519), BIP39, PBKDF2, AES-GCM** |
| **Mobile App** | React Native 0.81, Expo SDK 54, TypeScript, TanStack Query, Reanimated |
| **SDK** | TypeScript, Rollup |
| **Blockchain** | Octra Network |

## Roadmap

  - [x] **Browser Extension V2:** Complete rewrite in React for better performance and maintainability.
  - [x] **SDK Core (v2.0):** Enhanced connection handling and strict typing.
  - [x] **SDK v2.1:** Transaction finality, RPC error types, message signing, public key exposure.
  - [x] **Atlas (Beta):** Blockchain visualization and analytics platform.
  - [x] **Telegram Bot:** Real-time wallet monitoring via [@NullXio_bot](https://t.me/NullXio_bot).
  - [x] **JSON-RPC Migration:** Network layer migrated from REST to JSON-RPC 2.0.
  - [ ] Stealth Addresses (RFC-001): Client-side disposable address layer.
  - [ ] Mobile Beta: Native iOS & Android apps with biometric security.
  - [ ] 0xio DEX: Privacy-preserving decentralized exchange.

## Community & Support

  - **Website**: [0xio.xyz](https://0xio.xyz)
  - **X/Twitter**: [@0xio\_xyz](https://x.com/0xio_xyz)
  - **GitHub**: [@0xio-xyz](https://github.com/0xio-xyz/)
  - **Telegram**: [@Nullxgery](https://t.me/nullXgery)
  - **Documentation**: [docs.0xio.xyz](https://docs.0xio.xyz)
  - **Email**: team@0xio.xyz
  - **Issues**: Report bugs via GitHub Issues

## License & Terms

### Current Version (v2.0+)

**0xio Wallet (React/Vite)** is **Proprietary Software**.
Copyright © 2026 0xio Labs. All Rights Reserved.
Unauthorized copying, modification, distribution, or use of this software is strictly prohibited.

### Legacy Version (v1.0)

The **Legacy 0xio Extension** (located in the `legacy/` directory) remains open-source under the **MIT License**. It is provided for educational and archival purposes only.

-----

## Legal & Disclaimer

**0xio Wallet** is a proprietary software product developed and maintained by **0xio Labs**.

While designed exclusively for the **Octra Network**, 0xio Labs is an independent entity and is not affiliated with Octra Labs. This software is provided "as is", without warranty of any kind. Users are responsible for the security of their recovery phrases and private keys.

> **Future Open Source Commitment:**
> While the current codebase is proprietary to ensure integrity during our initial launch phase, we believe in the open-source ethos of Web3. We plan to open-source the v2.0 codebase once our security audits and feature stability phases are complete.
