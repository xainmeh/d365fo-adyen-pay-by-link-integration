# Technical Design

## D365FO Components

| Object | Type | Purpose |
| --- | --- | --- |
| ISWAdyenPayByLinkParameters | Table | Stores integration parameters and business rules. |
| ISWAdyenPaymentRequest | Table | Stores payment request details linked to a sales order. |
| ISWAdyenPaymentLog | Table | Stores request, response, and error logs. |
| ISWAdyenPaymentStatus | Enum | Defines payment request statuses. |
| ISWAdyenSalesConfirm_Extension | Class extension | Creates a payment request after sales order confirmation. |
| ISWAdyenPayByLinkService | Class | Creates and prepares payment request payloads. |
| ISWAdyenPaymentUpdateService | Class | Updates payment status from Dataverse or integration layer. |
| ISWAdyenPaymentRequestEntity | Data entity | Exposes payment request records for integration. |
| ISWAdyenPaymentResponseEntity | Data entity | Receives payment result updates. |
| ISWAdyenPayByLinkWorkspace | Form | Provides payment tracking visibility. |
| ISWAdyenPayByLinkSecurityPrivilege | Security privilege | Controls user access. |

## Suggested D365FO Payment Request Fields

| Field | Description |
| --- | --- |
| LegalEntity | Company creating the payment request. |
| SalesId | Related sales order number. |
| CustAccount | Customer account. |
| CustomerEmail | Email address used for sending the payment link. |
| Amount | Payment or prepayment amount. |
| CurrencyCode | Sales order currency. |
| MerchantReference | Unique reference sent to Adyen. |
| AdyenPspReference | PSP reference returned by Adyen. |
| PaymentLinkUrl | Hosted payment link returned by Adyen. |
| PaymentStatus | Current payment request status. |
| PrepaymentRequired | Indicates whether prepayment is required. |
| PrepaymentCovered | Indicates whether prepayment is covered. |
| ExpiryDateTime | Payment link expiry date and time. |
| LastWebhookDateTime | Last webhook event received. |
| ErrorMessage | Last integration or payment error. |

## Merchant Reference Pattern

Use a predictable and unique merchant reference.

```text
<LegalEntity>-<SalesOrderNumber>-<CustomerAccount>-<PaymentRequestRecId>
```

Example:

```text
USMF-SO000123-CUS001-5637144576
```

## Processing Notes

1. Do not create duplicate payment links for the same confirmed sales order unless the previous link is expired or cancelled.
2. Use idempotency where possible when calling Adyen APIs.
3. Store request and response logs for troubleshooting.
4. Validate webhook events before updating D365FO.
5. Do not store raw card information in D365FO or Dataverse.
