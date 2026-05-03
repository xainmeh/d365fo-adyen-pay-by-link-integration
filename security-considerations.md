# Security Considerations

## Payment Data Handling

This project should not store raw credit card information in D365FO, Dataverse, source code, logs, or sample files.

Card entry and card processing should happen through Adyen hosted payment pages or Adyen controlled payment components.

## Allowed Data to Store

Depending on business, legal, and payment provider guidance, the following references may be stored:

1. Merchant reference.
2. PSP reference.
3. Payment status.
4. Payment amount and currency.
5. Payment link URL.
6. Link expiry date and time.
7. Masked card details where permitted.
8. Token or recurring reference where explicitly enabled and allowed.

## Secrets Management

Do not store API keys or webhook secrets in source code.

Recommended options include:

1. Azure Key Vault.
2. Environment variables.
3. Secure Power Platform connection references.
4. Managed identity where applicable.

## Webhook Security

Webhook endpoints should validate incoming events before processing payment updates.

Recommended controls:

1. Validate webhook signatures or HMAC where configured.
2. Restrict endpoint exposure where possible.
3. Log received events safely.
4. Prevent duplicate event processing.
5. Avoid logging sensitive payment details.

## Production Readiness

Before using this pattern in production, review it with security, compliance, payment, and architecture teams.
