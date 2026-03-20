# Error Codes

PinkWallet Payment API

## Error Codes

### Example Format

```json
{
  "error": {
    "code": "INVALID_AMOUNT",
    "message": "Amount must be greater than 0"
  }
}
```

### Common Errors

| Code | Description |
| --- | --- |
| `UNAUTHORIZED` | Invalid API key |
| `INVALID_PARAMETER` | Missing or invalid field |
| `UNSUPPORTED_ASSET` | This asset/network is not supported |
| `ADDRESS_UNAVAILABLE` | No available payment address at the moment |
| `PAYMENT_EXPIRED` | Payment link has expired |
| `INTERNAL_ERROR` | Temporary service error |

