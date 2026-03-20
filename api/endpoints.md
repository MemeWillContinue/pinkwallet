# API Endpoints

PinkWallet Payment API

## Base URL

`https://api.pinkwallet.xyz/blockchain/pinkwallet`

## 1. Get Supported Assets and Networks

### GET `/api/payment/supported-assets`

Returns the currently supported payment assets and their available blockchain networks.

#### Request Parameters

None.

#### Response Example

```json
{
  "USDT": ["BNB Smart Chain(BEP20)", "Ethereum (ERC 20)", "Tron (TRC20)"],
  "USDC": ["Solana", "Ethereum (ERC 20)"]
}
```

#### Response Fields

| Field | Type | Description |
| --- | --- | --- |
| `{symbol}` | `string[]` | List of supported blockchain networks for the given asset symbol |

## 2. Create Payment Order

### POST `/api/payment/create`

Creates a payment order for your merchant account. The system allocates an on-chain payment address from the deposit address pool.

#### Request Body (JSON)

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `merchantId` | `number` | Yes | Merchant ID |
| `externalOrderId` | `string` | No | Custom merchant order ID. If omitted, the system generates a 32-character order ID |
| `asset` | `string` | Yes | Payment asset: `USDT` or `USDC` |
| `chain` | `string` | Yes | Blockchain network. You can fetch valid values from `/api/payment/supported-assets` |
| `amount` | `number` | Yes | Payment amount |
| `callbackUrl` | `string` | No | Webhook callback URL for payment result notifications |

#### Request Example

```json
{
  "merchantId": 3,
  "externalOrderId": "ORD_20260313_001",
  "asset": "USDT",
  "chain": "Solana",
  "amount": 5,
  "callbackUrl": "https://your-server.com/webhook/payment"
}
```

#### Response Example

```json
{
  "link_token": "81663115hE4b11PVzY",
  "external_order_id": "ORD_20260313_001",
  "amount": "5",
  "asset": "USDT",
  "chain": "Solana",
  "expires_at": "2026-03-13T06:31:15.000Z",
  "pay_address": "B27iWjQYNhE1ZN4PX3T2gAsPc5HSgeNoYBacZ78UVLS3",
  "memo": ""
}
```

#### Response Fields

| Field | Type | Description |
| --- | --- | --- |
| `link_token` | `string` | Order access token used for payment page URL and order status lookup |
| `external_order_id` | `string` | Merchant order ID |
| `amount` | `string` | Payment amount |
| `asset` | `string` | Payment asset |
| `chain` | `string` | Blockchain network |
| `expires_at` | `string` | Order expiration time in ISO 8601 format. Default validity is 30 minutes |
| `pay_address` | `string` | On-chain deposit address that the user should transfer funds to |
| `memo` | `string` | Memo/tag value required by some chains (for example, EOS). Empty string if not needed |

Payment Page URL: `https://pay.pinkwallet.xyz/{link_token}`

## 3. Query Order Status

### GET `/api/payment/{linkToken}`

Retrieves the current order status by `link_token`. The payment frontend should poll this endpoint every 2-5 seconds.

#### Path Parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `linkToken` | `string` | The `link_token` returned when the order was created |

#### Response Example

```json
{
  "link_token": "81663115hE4b11PVzY",
  "status": "pending",
  "amount": "5",
  "asset": "USDT",
  "chain": "Solana",
  "pay_address": "B27iWjQYNhE1ZN4PX3T2gAsPc5HSgeNoYBacZ78UVLS3",
  "expires_at": "2026-03-13T06:31:15.000Z",
  "paid_at": null,
  "tx_hash": null
}
```

#### Response Fields

| Field | Type | Description |
| --- | --- | --- |
| `link_token` | `string` | Order access token |
| `status` | `string` | Order status. See status table below |
| `amount` | `string` | Payment amount |
| `asset` | `string` | Payment asset |
| `chain` | `string` | Blockchain network |
| `pay_address` | `string \| null` | Deposit address. Returns `null` if the order fails |
| `expires_at` | `string` | Expiration time in ISO 8601 format |
| `paid_at` | `string \| null` | Payment completion time in ISO 8601 format. `null` if unpaid |
| `tx_hash` | `string \| null` | On-chain transaction hash. `null` if unpaid |

#### Order Status Values

| Status | Description |
| --- | --- |
| `pending` | Waiting for payment |
| `paid` | Payment completed |
| `expired` | Payment expired |
| `failed` | Payment failed |

