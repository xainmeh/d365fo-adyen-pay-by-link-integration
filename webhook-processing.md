# Webhook Processing

## Purpose

Webhook processing is used to receive payment status updates from Adyen after the customer interacts with the payment link.

## Recommended Flow

1. Adyen sends webhook event to the configured endpoint.
2. Integration layer validates the webhook event.
3. Raw payload is stored for audit and troubleshooting.
4. Merchant reference is used to identify the related payment request.
5. Payment status is mapped to the internal D365FO payment status.
6. Dataverse payment response record is created or updated.
7. D365FO payment request is updated.
8. Sales order prepayment coverage is updated if payment is successful.

## Status Mapping

| Adyen Result | Internal Status |
| --- | --- |
| Authorised | Paid |
| Refused | Failed |
| Cancelled | Cancelled |
| Error | Failed |
| Expired | Expired |

## Processing Rules

1. Do not update D365FO until the webhook is validated.
2. Use merchant reference to find the correct payment request.
3. Prevent duplicate processing of the same PSP reference and event code.
4. Store all processing errors in the event log.
5. Treat link creation as pending until payment is confirmed by webhook.

## Sample Completed Payment Event

```json
{
  "eventCode": "AUTHORISATION",
  "success": "true",
  "merchantReference": "USMF-SO000123-CUS001-5637144576",
  "pspReference": "8812345678901234",
  "eventDate": "2026-01-15T10:30:00Z",
  "amount": {
    "currency": "USD",
    "value": 30000
  }
}
```
