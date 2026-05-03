# Adyen API Payloads

## Create Payment Link Request

```json
{
  "merchantAccount": "YourMerchantAccount",
  "reference": "USMF-SO000123-CUS001-5637144576",
  "amount": {
    "currency": "USD",
    "value": 30000
  },
  "shopperReference": "CUS001",
  "shopperEmail": "customer@example.com",
  "countryCode": "US",
  "returnUrl": "https://yourcompany.example.com/payment-result",
  "metadata": {
    "legalEntity": "USMF",
    "salesOrder": "SO000123",
    "customerAccount": "CUS001",
    "sourceSystem": "D365FO"
  }
}
```

## Create Payment Link Response

```json
{
  "id": "PL123456789",
  "url": "https://test.adyen.link/PL123456789",
  "status": "active",
  "expiresAt": "2026-01-31T23:59:59Z",
  "reference": "USMF-SO000123-CUS001-5637144576"
}
```

## Notes

1. Amount values may need to be sent in minor units, such as cents for USD.
2. The merchant reference should be unique and traceable back to D365FO.
3. API keys should not be committed to the repository.
4. Samples in this project use fictional data only.
