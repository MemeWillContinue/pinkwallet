# Webhook Callback

PinkWallet Payment API

## Webhook Callback

When an order is paid or marked as failed, the system sends an HTTP `POST` request to the `callbackUrl` provided during order creation.

### Delivery and Retry Policy

- Any HTTP `2xx` response is treated as successful delivery
- The order is marked as `failed` if all retries fail
- Maximum 4 retries
- Automatic retry schedule on failure: 1 minute -> 5 minutes -> 30 minutes -> 2 hours
- First attempt is sent immediately

### Webhook Payload (JSON)

```json
{
  "event": "payment.paid",
  "status": "paid",
  "link_token": "81663115hE4b11PVzY",
  "external_order_id": "ORD_20260313_001",
  "asset": "USDT",
  "chain": "Solana",
  "amount_expected": "5",
  "amount_received": "5.000000",
  "tx_hash": "5KtP...abc123",
  "paid_at": "2026-03-13T06:35:20.000Z"
}
```

### Payload Fields

| Field | Type | Description |
| --- | --- | --- |
| `event` | `string` | Event type: `payment.paid` (success) or `payment.failed` (failure) |
| `status` | `string` | Processing status: `paid` or `failed` |
| `link_token` | `string` | Order access token |
| `external_order_id` | `string` | Merchant order ID |
| `asset` | `string` | Payment asset |
| `chain` | `string` | Blockchain network |
| `amount_expected` | `string` | Expected payment amount |
| `amount_received` | `string` | Actual received amount |
| `tx_hash` | `string` | On-chain transaction hash |
| `paid_at` | `string` | Payment/processing time in ISO 8601 format |
| `message` | `string` | Failure reason. Present only for `payment.failed` |

