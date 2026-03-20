# Product Overview

PinkWallet Payment API

## 1.1 Overview

PinkWallet provides a secure, real-time cryptocurrency payment infrastructure for merchants who accept USDT and USDC across major blockchain networks.

With our Payment API, you can:

- Convert crypto to USD/EUR/GBP or withdraw to your company wallet (coming soon)
- See all payment balances in your merchant dashboard
- Receive instant on-chain payment confirmation via webhook
- Display it directly on your website, mobile app, or checkout page
- Generate a hosted payment link or QR code

Our system ensures every payment is uniquely matched to one order and prevents mismatch, even if customers reuse outdated QR codes or screenshots.

## 1.2 Supported Assets & Networks

PinkWallet currently supports:

| Asset | Networks |
| --- | --- |
| USDT | Ethereum (ERC20), Tron (TRC20), Arbitrum One, BSC Smart Chain, SOL (Solana) |
| USDC | Ethereum (ERC20), Arbitrum One |

More networks will be added soon.

## 1.3 Core Concepts

### 1.3.1 Payment Link

A Payment Link represents a single order initiated by your system. It contains:

- Expiration time
- Unique deposit address
- Network selection
- Asset type
- Required payment amount

### 1.3.2 Deposit Address

Each Payment Link includes a dedicated deposit address, which is active only during the order validity window. After confirmation, PinkWallet attributes the received funds to the merchant's internal account balance.

### 1.3.3 Guaranteed Order Matching

PinkWallet ensures zero ambiguity using:

- Strict time-window validation
- Amount matching with ±0.2 USDT/USDC tolerance
- Address-level isolation

This ensures each blockchain deposit is associated with exactly one order.

## 1.4 Merchant Workflow

### Step 1 - Create a Payment Link via API

You call our API to create a payment request.

### Step 2 - Display QR Code to Your User

We return:

- QR code (optional)
- Amount, network, countdown timer
- A payment address
- A hosted payment URL

You embed or redirect your user to the link.

### Step 3 - User Pays on Chain

Your user sends USDT/USDC from their wallet or exchange.

### Step 4 - PinkWallet Confirms Payment in Seconds

Once the deposit hits the blockchain:

- Mark the order as paid
- Trigger a webhook to your server
- We validate it

### Step 5 - Funds Credited to Merchant Account

The deposit amount is credited to your merchant dashboard balance. You may:

- Withdraw to your business's external wallet (via PinkWallet APP)
- Convert to USD/EUR/GBP (via PinkWallet APP)
- Keep crypto

