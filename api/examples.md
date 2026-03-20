# Examples & Support

PinkWallet Payment API

## Examples & Support

### Example Client Implementation

### Node.js Example

```js
const axios = require("axios");

const res = await axios.post(
  "https://api.pinkwallet.com/api/v1/payments",
  {
    merchant_order_id: "ORDER123",
    amount: "100.00",
    asset: "USDT",
    chain: "ERC20",
    callback_url: "https://merchant.com/callback"
  },
  {
    headers: {
      Authorization: "Bearer YOUR_API_KEY"
    }
  }
);

console.log(res.data);
```

## Questions & Support

For onboarding assistance, technical integration, or custom enterprise pricing:

https://t.me/PinkwaIIet_Suport

## Changelog

- Future updates will include card issuing, ACH rail integration, currency conversion APIs, automated settlements, webhook signature verification, and more.
- `v1.0`- Initial API release`2026-02-23`

