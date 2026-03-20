# Operations & Security

PinkWallet Payment API

## Operations & Security

### Payment Expiration

Each payment link has a default expiration time of 30 minutes.

If blockchain payment arrives after expiration:

- You may manually handle or refund
- It will be shown as an unassigned deposit in our dashboard
- It will not be matched to the original order

This prevents screenshot reuse and wrong-order attribution.

### Merchant Dashboard Settlement

After a payment is marked as paid, the funds are credited to your merchant balance.

You can access:

- Withdraw to a local bank account
- Withdraw to an external wallet
- Convert balance to USD/EUR/GBP
- Transaction History
- Crypto Balance (USDT/USDC)

Coming soon:

- Automatic settlement schedules

These features will be available via PinkWallet APP.

### Security & Compliance

PinkWallet provides:

- Strict transaction matching rules
- Anti-replay protection
- Double-spend protection
- Real-time blockchain monitoring
- Time-boxed deposit address usage
- Address-level isolation

We never expose internal wallet infrastructure and do not require merchants to manage private keys.

All settlements occur through the PinkWallet merchant account system.

