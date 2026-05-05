# D365FO Adyen Pay by Link Integration

An open-source integration accelerator for Microsoft Dynamics 365 Finance and Operations that generates Adyen Pay by Link requests from confirmed sales orders and updates payment or prepayment status through Dataverse and webhook processing.

## Overview

This project provides a reusable integration pattern for D365FO implementations where customer prepayment needs to be collected after sales order confirmation.

When a sales order is confirmed, the solution can create a payment request, calculate the required prepayment amount, call Adyen to generate a hosted payment link, and send that link to the customer.

After the customer completes the payment, Adyen webhook responses can update Dataverse and synchronize the payment status back to D365FO. The sales order payment status and prepayment coverage can then be updated automatically.

## Business Scenario

Many businesses need to collect customer prepayments before releasing, reserving, fulfilling, or delivering sales orders. In many D365FO implementations, this process is handled manually through emails, external payment portals, or disconnected payment references.

This project provides a technical pattern where payment link generation and payment confirmation can be connected back to the sales order lifecycle.

## Planned Capabilities

1. Trigger payment link creation from sales order confirmation.
2. Calculate prepayment amount from sales order rules.
3. Create a D365FO payment request record.
4. Store integration tracking data in Dataverse.
5. Generate Adyen Pay by Link through API orchestration.
6. Send the payment link to the customer.
7. Receive Adyen webhook payment responses.
8. Update D365FO payment status.
9. Mark sales order prepayment requirement as covered.
10. Maintain request and response logs for audit and troubleshooting.

## Technology Stack

1. Microsoft Dynamics 365 Finance and Operations.
2. X++.
3. Dataverse.
4. Power Automate or Azure Functions.
5. Adyen Pay by Link API.
6. Adyen webhooks.

## Proposed Repository Structure

```text
docs
src
samples
assets
```

## Documentation

| File | Purpose |
| --- | --- |
| docs/overview.md | Explains the project purpose and business value. |
| docs/functional-flow.md | Describes the end-to-end functional process. |
| docs/architecture.md | Explains the proposed integration architecture. |
| docs/technical-design.md | Describes the D365FO, Dataverse, and integration components. |
| docs/dataverse-schema.md | Defines the proposed Dataverse tables and fields. |
| docs/adyen-api-payloads.md | Provides sample Adyen request and response structures. |
| docs/webhook-processing.md | Explains webhook processing and status update logic. |
| docs/security-considerations.md | Documents security, PCI, and data protection considerations. |

## Scope

The first version of this project should focus on a simple and realistic flow:

1. Create a payment request when a sales order is confirmed.
2. Generate an Adyen Pay by Link request.
3. Send the payment link to the customer.
4. Receive the Adyen payment webhook.
5. Update payment status in Dataverse.
6. Update the D365FO sales order payment status.
7. Mark prepayment as covered.

## Out of Scope for Initial Version

1. Refund processing.
2. Chargebacks and disputes.
3. Full settlement reconciliation.
4. Multiple partial payment schedules.
5. Advanced tokenization flows.
6. Complex customer payment journal automation.
7. Multi-merchant routing.

## Security Notes

This project should not store raw credit card information in D365FO or Dataverse. Payment card details should remain within Adyen. D365FO and Dataverse should only store allowed references such as payment status, merchant reference, PSP reference, masked card details where permitted, and token references where applicable.

API keys and secrets should be stored securely through Azure Key Vault or another secure secrets management option. They should not be stored directly in source code.

## Status

This project is currently in planning and initial development stage.

## Disclaimer

This is an open-source accelerator and is not an official Microsoft or Adyen product. It should be reviewed, tested, and adapted before use in any production environment.
