# 0xio

Privacy-first wallet ecosystem for the Octra Network, built by **0xio Labs**.

## Overview

0xio is a comprehensive wallet solution for managing public and private cryptocurrency transactions on Octra Network. The ecosystem spans a browser extension, native mobile apps (iOS & Android), a desktop application, and developer tools — all unified by a custom privacy cryptography stack built on fully homomorphic encryption (FHE).

## Products

### Browser Extension (0xio wallet)
**Status:** Live on Chrome Web Store

The 0xio Wallet is a high-performance browser extension built with React and Vite. It serves as the primary interface for managing Octra Network assets, with native FHE privacy operations powered by pvac-rs compiled to WebAssembly.

**Features:**
- **Privacy Cryptography (PVAC):** FHE encrypt/decrypt, range proofs, stealth transfers — all in-browser via WASM
- **Vault Architecture:** Single encrypted vault protected by AES-GCM with 900,000 PBKDF2 iterations
- **Multi-Wallet:** Create and manage up to 20 wallets per installation
- **dApp Ready:** Seamless connectivity via the `@0xio/sdk` with origin-verified transaction approval
- **Asset Management:** Custom token import and NFT collection gallery with on-chain ownership enumeration
- **FHE Tools:** Standalone encrypt/decrypt UI + automatic FHE parameter expansion in contract calls
- **Supply Chain Security:** Protected against malicious npm packages using LavaMoat

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc)

**Tech Stack:**
- **Framework:** React 18 + Vite
- **Styling:** TailwindCSS
- **Cryptography:** pvac-rs (WASM + rayon multithreading), TweetNaCl (Ed25519), Web Crypto API
- **State Management:** React Context + Hooks
- **Standard:** Chrome Extension Manifest V3

### Desktop Application (0xio Desktop)
**Status:** In Development

Native desktop wallet powered by Tauri 2 and Rust. Offloads heavy cryptographic operations (range proofs, FHE encrypt/decrypt) to native Rust via a local WebSocket bridge, achieving the fastest privacy operation performance across all platforms.

**Features:**
- **Native Rust Crypto:** pvac-rs runs natively — no WASM overhead, full CPU utilization
- **WebSocket Bridge:** Local relay at `127.0.0.1:19345` connects the React UI to the Rust backend
- **FHE Tools:** Encrypt/decrypt UI + contract call FHE integration (same as extension)
- **Contract Interaction:** Deploy, call, and call-view smart contracts with FHE parameter support
- **Full Wallet Management:** Create, import, send, receive, claim — feature parity with extension

**Tech Stack:**
- **Framework:** Tauri 2 (Rust backend + React frontend)
- **Cryptography:** pvac-rs (native), curve25519-dalek, @noble/hashes
- **Frontend:** React + TypeScript + TailwindCSS
- **Bridge:** WebSocket (pvac-handler crate)

### Mobile Applications (0xio_app)
**Status:** In Development (Beta)

Native mobile wallet for iOS and Android with privacy operations powered by pvac-rs compiled to platform-native libraries (iOS static lib, Android shared lib via JNI/FFI).

**Features:**
- Multi-wallet management (create, import, watch-only)
- Public and private token transfers with FHE encryption
- Bulk transaction support (public & private, up to 5 recipients)
- Stealth transfer claiming with automatic scan
- Custom token import by contract address (swipe-to-delete)
- Biometric authentication (Face ID / Touch ID / Fingerprint)
- PIN lock with rate limiting and auto-lock timeout
- DApp browser with wallet provider injection
- Transaction history with pending tracking
- Address book for saved contacts
- QR code generation and sharing
- Internationalization (English, Bahasa Indonesia, Chinese, Japanese, Korean)
- Dark theme
- Hide balances toggle

**Tech Stack:**
- React Native 0.81 + Expo SDK 54 (New Architecture enabled)
- TypeScript 5.9 (strict mode)
- pvac-rs via native FFI (iOS: static lib, Android: shared lib)
- TanStack React Query for data fetching
- React Navigation (Stack)
- React Native Gesture Handler + Reanimated
- @noble/hashes (PBKDF2, SHA-256), TweetNaCl (Ed25519)
- expo-secure-store, expo-local-authentication, expo-haptics
- i18next for internationalization
- Sentry for error monitoring

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
- Contract interaction (call, call-view, storage reads)
- Event-driven architecture with typed events
- Rate limiting and retry with exponential backoff
- Full TypeScript support with strict readonly interfaces
- Framework agnostic (React, Vue, Svelte, Vanilla JS)

**Installation:**
```bash
npm install @0xio/sdk
```

### 0xio DEX
**Status:** In Development

Privacy-preserving decentralized exchange with concentrated liquidity (CLMM) for trading encrypted assets on the Octra Network.

**URL:** [dex.0xio.xyz](https://dex.0xio.xyz)

### Atlas
**Status:** Live (Beta)

Blockchain visualization and analytics platform for the Octra Network.

**URL:** [atlas.0xio.xyz](https://atlas.0xio.xyz)

### Telegram Bot
**Status:** Live

Real-time wallet monitoring and notifications via Telegram.

**Bot:** [@NullXio_bot](https://t.me/NullXio_bot)

## Security & Cryptography

0xio implements a multi-layered cryptographic architecture combining standard key management with a custom privacy system built on fully homomorphic encryption.

### Key Generation and Derivation

- **Mnemonic Generation (BIP39):** 128-bit entropy via Web Crypto API produces a standard 12-word mnemonic phrase.
- **Seed Derivation:** PBKDF2 with HMAC-SHA512 (2048 iterations) derives the binary seed from the mnemonic.
- **Master Root Key:** `HMAC-SHA512("Octra seed", seed)[0:32]` — deterministic master key derivation used across all platforms.
- **Signing Keys:** Ed25519 (Twisted Edwards curve) via TweetNaCl for high-speed digital signatures.
- **Address Generation:** Public key → SHA-256 hash → Base58 encoding → `oct` prefix.

### Privacy Cryptography (PVAC)

PVAC (Privacy Via Additive Ciphers) is 0xio's custom privacy system built on fully homomorphic encryption, enabling encrypted on-chain balances and private transfers.

**Core Primitives:**
- **FHE Encrypt/Decrypt:** Additively homomorphic encryption of token amounts — encrypted values can be added on-chain without decryption
- **Range Proofs:** Zero-knowledge proofs (64-bit) proving an encrypted amount is non-negative and within bounds, without revealing the value
- **Pedersen Commitments:** Binding commitments to amounts using elliptic curve points, used for transaction integrity
- **Stealth Transfers:** ECDH key agreement generates one-time stealth addresses — recipient scans for incoming transfers using stealth tag matching
- **Zero Proofs:** Proof that a ciphertext encrypts zero, used during decrypt (withdrawal) operations

**Cryptographic Libraries:**
- **pvac-rs** — Custom Rust library implementing all PVAC operations
  - `curve25519-dalek` for elliptic curve arithmetic
  - Multithreaded range proof generation (work-stealing across CPU cores)
  - Compiles to: WASM (extension), iOS static lib, Android shared lib, native binary (desktop)
- **@noble/hashes** — PBKDF2, SHA-256, HMAC for key derivation
- **TweetNaCl** — Ed25519 signing and key pair generation

### Storage Security

- **Extension:** AES-GCM encrypted vault, key derived from password via PBKDF2 (900,000 iterations) with unique random salt. Keys never leave the device.
- **Mobile:** expo-secure-store for sensitive data, PBKDF2-hardened PIN verification, biometric gating, progressive rate limiting on failed attempts.
- **Desktop:** Same vault architecture as extension, with native Rust crypto backend.

## Architecture

```
┌──────────────────────────────┐     ┌──────────────────────────────┐
│    0xio_wallet (Chrome)      │     │     0xio Desktop (Tauri)     │
│  React + Vite + TailwindCSS  │     │  React + Rust + TailwindCSS  │
│  pvac-rs (WASM + rayon)      │     │  pvac-rs (native binary)     │
│  Ed25519 + AES-GCM Vault     │     │  WebSocket bridge :19345     │
└──────────────┬───────────────┘     └──────────────┬───────────────┘
               │                                    │
               │ Extension API              Tauri IPC + WS
               │                                    │
┌──────────────┴────────────────────────────────────┴───────────────┐
│                     dApps (Web Applications)                      │
│                   React, Vue, Svelte, Vanilla JS                  │
│                        @0xio/sdk (npm)                            │
└───────────────────────────────┬──────────────────────────────────┘
                                │
                          JSON-RPC 2.0
                                │
┌───────────────────────────────┴──────────────────────────────────┐
│                      Network Service Layer                       │
│           Transaction Broadcasting · Balance Queries              │
│     Private Transfer Management · Contract Call (REST + RPC)     │
└───────────────────────────────┬──────────────────────────────────┘
                                │
┌───────────────────────────────┴──────────────────────────────────┐
│                         Octra Network                            │
│   Consensus · Smart Contracts (AML) · FHE Encrypted Balances     │
└──────────────────────────────────────────────────────────────────┘

┌──────────────────────────────┐
│     0xio_app (Mobile)        │
│  React Native + Expo 54      │
│  pvac-rs (native FFI)        │         Connects directly to
│  Biometric · DApp Browser    │ ──────► Network Service Layer
│  i18n (5 languages)          │
└──────────────────────────────┘
```

## Repositories

| Repository | Description | Status |
|------------|-------------|--------|
| **0xio_wallet** | React-based browser extension wallet | Live |
| **0xio-desktop** | Tauri + Rust desktop application | Development |
| **0xio_app** | React Native mobile application (iOS & Android) | Development (Beta) |
| **0xio_SDK** | TypeScript SDK for dApp integration | Published on npm |
| **0xio_web** | Marketing website and onboarding | Live at 0xio.xyz |
| **documentation** | Mintlify-powered docs site | Live at docs.0xio.xyz |
| **Legacy** | Archived Vanilla JS extension code | Archived |

## Technology Stack

| Component | Stack |
|-----------|-------|
| **Browser Extension** | React 18, Vite, TailwindCSS, CRXJS, pvac-rs (WASM) |
| **Desktop App** | Tauri 2, Rust, React, TypeScript, TailwindCSS, pvac-rs (native) |
| **Mobile App** | React Native 0.81, Expo 54, TypeScript 5.9, TanStack Query, pvac-rs (FFI) |
| **Cryptography** | pvac-rs (curve25519-dalek), @noble/hashes, TweetNaCl (Ed25519), AES-GCM, PBKDF2 |
| **SDK** | TypeScript, Rollup |
| **Smart Contracts** | AML (AppliedML) — Octra's contract language |
| **Blockchain** | Octra Network |

## Roadmap

- [x] **Browser Extension V2:** Complete rewrite in React with PVAC integration.
- [x] **SDK v2.1:** Transaction finality, RPC error types, message signing.
- [x] **Atlas (Beta):** Blockchain visualization and analytics.
- [x] **Telegram Bot:** Real-time wallet monitoring via [@NullXio_bot](https://t.me/NullXio_bot).
- [x] **JSON-RPC Migration:** Network layer migrated from REST to JSON-RPC 2.0.
- [x] **FHE Tools:** Standalone encrypt/decrypt + contract call FHE integration across all platforms.
- [x] **Desktop App:** Tauri + Rust desktop wallet with native crypto backend.
- [x] **NFT Gallery:** Collection import and on-chain ownership display in the browser extension.
- [x] **dApp Approval UX:** Origin verification, wallet context, and auto-reject on popup close.
- [ ] Mobile Public Beta: Native iOS & Android apps with biometric security.
- [ ] 0xio DEX: Privacy-preserving concentrated liquidity exchange.
- [ ] Open Source: Planned open-source release after security audits.

## Getting Started

### For Users

**Browser Extension:**
1. Install from the [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc).
2. Create a new wallet or import your existing 12-word mnemonic.
3. Start managing your Octra assets.

**Desktop App:**
- *Coming soon.*

**Mobile App:**
- *Coming soon to iOS and Android.*

### For Developers

**Integrate 0xio Wallet into your dApp:**

```bash
npm install @0xio/sdk
```

```typescript
import { createZeroXIOWallet } from '@0xio/sdk';

const wallet = await createZeroXIOWallet({
  appName: 'My DApp',
  autoConnect: true
});

await wallet.connect();
```

## Community & Support

- **Website**: [0xio.xyz](https://0xio.xyz)
- **X/Twitter**: [@0xio_xyz](https://x.com/0xio_xyz)
- **GitHub**: [@0xio-xyz](https://github.com/0xio-xyz/)
- **Telegram**: [@Nullxgery](https://t.me/nullXgery)
- **Documentation**: [docs.0xio.xyz](https://docs.0xio.xyz)
- **Email**: team@0xio.xyz

## License & Terms

### Current Version

**0xio Wallet, Desktop, and Mobile** are **Proprietary Software**.
Copyright &copy; 2026 0xio Labs. All Rights Reserved.
Unauthorized copying, modification, distribution, or use of this software is strictly prohibited.

### Legacy Version

The **Legacy 0xio Extension** (located in the `legacy/` directory) remains open-source under the **MIT License** for educational purposes.

---

**0xio** is developed and maintained by **0xio Labs**. While designed exclusively for the **Octra Network**, 0xio Labs is an independent entity and is not affiliated with Octra Labs. This software is provided "as is", without warranty of any kind. Users are responsible for the security of their recovery phrases and private keys.
