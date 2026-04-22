# 0xio

Privacy-first wallet ecosystem for the Octra Network, built by **0xio Labs**.

## Overview

0xio is a comprehensive wallet solution for managing public and private cryptocurrency transactions on Octra Network. The ecosystem spans a browser extension, native mobile apps (iOS & Android), a desktop application, and developer tools — all unified by a custom privacy cryptography stack built on fully homomorphic encryption (FHE).

## Products

### Browser Extension (0xio wallet)
**Status:** Live on Chrome Web Store (v2.3.1)

The 0xio Wallet is a high-performance browser extension built with React and Vite. It serves as the primary interface for managing Octra Network assets, with native FHE privacy operations powered by pvac-rs compiled to WebAssembly.

**Features:**
- **Privacy Cryptography (PVAC):** FHE encrypt/decrypt, range proofs, stealth transfers — all in-browser via WASM
- **Vault Architecture:** Single encrypted vault protected by AES-GCM with 900,000 PBKDF2 iterations
- **Multi-Wallet:** Create and manage up to 20 wallets per installation
- **HD Account Derivation:** Derive multiple accounts from a single seed phrase
- **OAT Token Transfers:** Select and send OAT tokens alongside OCT
- **Fee Recommendations:** Dynamic fee estimates from the network via `octra_recommendedFee` RPC
- **Token Auto-Discovery:** Automatic detection of token holdings from on-chain contracts
- **dApp Ready:** Seamless connectivity via the `@0xio/sdk` with origin-verified transaction approval
- **Asset Management:** Custom token import and NFT collection gallery with on-chain ownership enumeration and collection removal
- **Live Price Feeds:** Real-time OCT price from 0xio oracle (CoinGecko + DexScreener aggregation), USD portfolio worth display
- **FHE Tools:** Standalone encrypt/decrypt UI + automatic FHE parameter expansion in contract calls
- **Instant Transaction History:** Pending transactions appear immediately; devnet uses fast node RPC
- **Staging/Mempool View:** View pending transactions and contract call/deploy types in history
- **Custom RPC URL:** Connect to any Octra-compatible node
- **Internationalization:** 5 languages (English, Indonesian, Chinese, Japanese, Korean)
- **Supply Chain Security:** Protected against malicious npm packages using LavaMoat

**Install:** [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc)

**Tech Stack:**
- **Framework:** React 18 + Vite
- **Styling:** TailwindCSS
- **Cryptography:** pvac-rs (WASM + rayon multithreading), TweetNaCl (Ed25519), Web Crypto API
- **Price Feeds:** 0xio Oracle (multi-source aggregation)
- **State Management:** React Context + Hooks
- **Standard:** Chrome Extension Manifest V3

### Desktop Application (0xio Desktop)
**Status:** Alpha (v0.2.0) — macOS (Apple Silicon) + Windows, signed and notarized by Apple

Native desktop wallet powered by Tauri 2 and Rust. Offloads heavy cryptographic operations (range proofs, FHE encrypt/decrypt) to native Rust via a local WebSocket bridge, achieving the fastest privacy operation performance across all platforms.

**Features:**
- **Native Rust Crypto:** pvac-rs runs natively — no WASM overhead, full CPU utilization
- **WebSocket Bridge:** Local relay at `127.0.0.1:19345` connects the React UI to the Rust backend
- **FHE Tools:** Encrypt/decrypt UI + contract call FHE integration (same as extension)
- **Contract Interaction:** Deploy, call, and call-view smart contracts with FHE parameter support
- **Full Wallet Management:** Create, import, send, receive, claim — feature parity with extension
- **HD Account Derivation:** Derive multiple accounts from a single seed phrase
- **Stealth Send:** Private transfers with ECDH key exchange and stealth tags
- **Token Auto-Discovery:** Automatic detection of token holdings from on-chain contracts
- **Fee Recommendations:** Dynamic fee estimates from the network via `octra_recommendedFee` RPC
- **Contract Verification & Browser:** Verify deployed contracts and browse contract storage
- **Staging/Mempool View:** View pending transactions in transaction history
- **Key Display:** View and export wallet public/private keys
- **DApp Connection:** Connect to the browser extension as a PVAC computation accelerator
- **AI Contract Assistant:** AI-powered contract interaction guidance
- **Auto-Updater:** Automatic update checks and installation
- **Sentry Crash Reporting:** Error monitoring and diagnostics
- **Debug Console:** Built-in developer debugging tools
- **RPC Proxy Support:** Caching RPC proxy for improved performance
- **Apple Notarization:** Signed and notarized for macOS Gatekeeper

**Tech Stack:**
- **Framework:** Tauri 2 (Rust backend + React frontend)
- **Cryptography:** pvac-rs (native), curve25519-dalek, @noble/hashes
- **Frontend:** React + TypeScript + TailwindCSS
- **Bridge:** WebSocket (pvac-handler crate)

### Mobile Applications (0xio_app)
**Status:** Alpha (v1.0.2) — iOS on TestFlight, Android on Google Play

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
- QR code scanning and generation
- Internationalization (English, Bahasa Indonesia, Chinese, Japanese, Korean)
- Dark theme
- Hide balances toggle
- RPC proxy for fast history loading
- Dual-network history (mainnet + devnet)
- Sentry crash reporting
- Dynamic recommended fees per operation type
- **Production Readiness:**
  - Terms of Service acceptance screen
  - Screenshot and screen recording prevention
  - Accessibility labels and hints throughout
  - Push notification support
  - Secure clipboard (auto-clear after timeout)
  - Backup reminder for unprotected wallets
  - Network connection status indicator
  - Jailbreak/root detection warnings
  - Transaction confirmations with biometric/PIN authentication

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
- **v2.4.2:** iframe/frame bridge for desktop and mobile wallet connectivity
- **v2.4.2:** Cross-origin iframe bridge for localhost dev testing

**Installation:**
```bash
npm install @0xio/sdk
```

### 0xio DEX
**Status:** In Development

Privacy-preserving decentralized exchange with concentrated liquidity (CLMM) for trading encrypted assets on the Octra Network. Cleaned up codebase with configurable token whitelist and stale quote protection.

**Features:**
- Concentrated liquidity (CLMM) swap
- Bridge (OCT <-> wOCT) — lock functional, claim pending Merkle proof API
- Dynamic fee estimation

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
│               @0xio/sdk v2.4.2 (npm, iframe bridge)               │
└───────────────────────────────┬───────────────────────────────────┘
                                │
                          JSON-RPC 2.0
                                │
┌───────────────────────────────┴──────────────────────────────────┐
│                      Network Service Layer                       │
│           Transaction Broadcasting · Balance Queries             │
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
| **0xio-desktop** | Tauri + Rust desktop application | Alpha |
| **0xio_app** | React Native mobile application (iOS & Android) | Alpha |
| **0xio_SDK** | TypeScript SDK for dApp integration | Published on npm |
| **0xio_web** | Marketing website and onboarding | Live at 0xio.xyz |
| **documentation** | Mintlify-powered docs site | Live at docs.0xio.xyz |
| **0xio-alpha** | Alpha portal — invite-code gated distribution | Live |
| **0xio-oracle** | Multi-source price oracle (Rust) | Live |
| **0xio-rpc-proxy** | Caching RPC proxy | Live |
| **0xio-push-server** | Push notification service | Live |
| **0xio-dex** | Privacy-preserving DEX | Development |
| **Token-lists** | Token registry | Live |
| **Legacy** | Archived Vanilla JS extension code | Archived |

## Technology Stack

| Component | Stack |
|-----------|-------|
| **Browser Extension** | React 18, Vite, TailwindCSS, CRXJS, pvac-rs (WASM) |
| **Desktop App** | Tauri 2, Rust, React, TypeScript, TailwindCSS, pvac-rs (native) |
| **Mobile App** | React Native 0.81, Expo 54, TypeScript 5.9, TanStack Query, pvac-rs (FFI) |
| **Cryptography** | pvac-rs (curve25519-dalek), @noble/hashes, TweetNaCl (Ed25519), AES-GCM, PBKDF2 |
| **Price Oracle** | Rust, Axum, PostgreSQL, CoinGecko + DexScreener aggregation |
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
- [x] **Extension v2.2.5:** OAT token transfers, fee recommendations, HD derivation, instant history, 5 languages.
- [x] **Desktop Webcli Parity:** HD derivation, stealth send, token discovery, fee recommendations, contract verification, contract browser, staging view, key display, DApp connection.
- [x] **Mobile Production Hardening:** QR scanner, ToS screen, screenshot prevention, accessibility, push notifications, secure clipboard, backup reminder, connection status, jailbreak detection, transaction confirmations with auth.
- [x] **SDK v2.4.2:** iframe/frame bridge for desktop and mobile wallet connectivity.
- [x] **DEX Cleanup:** Configurable token whitelist, stale quote protection.
- [x] Mobile Public Beta: Native iOS & Android apps with biometric security.
- [x] SDK v2.4.2: Cross-origin iframe bridge, security hardening.
- [x] Alpha Portal: Invite-code gated distribution at alpha.0xio.xyz.
- [x] **Extension v2.3.0:** On-chain SVG NFT rendering, ABI-driven NFT transfers, dual-network history, RPC proxy, contract method names in history.
- [x] **Desktop v0.2.0:** NFT SVG + ABI transfer, unified history labels, DApp browser settings, account discovery (HD scan), double-fire guard, Windows build via CI.
- [x] **Mobile v1.0.2:** Unified transaction review modal, nonce auto-retry, custom nonce support, dynamic fees, history method names, NFT SVG rendering, wallet delete cleanup.
- [x] **NFT Standards:** Support for SNS-1 (Spectrum) and Biont (Euint Labs) NFT standards across all platforms.
- [x] **RPC Proxy:** Caching proxy reducing history responses from 8.3MB to 7KB.
- [x] **Price Oracle:** Multi-source price aggregation (CoinGecko + DexScreener) with anomaly detection, PostgreSQL price history, and CoinGecko 30-day backfill.
- [x] **Extension v2.3.1:** Live OCT price feeds, USD portfolio worth chart with oracle price history, NFT collection removal, production console stripping.
- [ ] 0xio DEX: Privacy-preserving concentrated liquidity exchange.
- [ ] Bridge: OCT ↔ wOCT cross-chain bridge (lock functional, claim pending Merkle proof API).
- [ ] Open Source: Planned open-source release after security audits.

## Getting Started

### For Users

**Browser Extension:**
1. Install from the [Chrome Web Store](https://chromewebstore.google.com/detail/0xio-wallet/anknhjilldkeelailocijnfibefmepcc).
2. Create a new wallet or import your existing 12-word mnemonic.
3. Start managing your Octra assets.

**Desktop App:**
- Alpha available at [alpha.0xio.xyz](https://alpha.0xio.xyz). macOS (Apple Silicon) and Windows.

**Mobile App:**
- Alpha available at [alpha.0xio.xyz](https://alpha.0xio.xyz). iOS via TestFlight, Android on Google Play.

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
