# d365fo-adyen-pay-by-link-integration
An open-source D365 Finance &amp; Operations integration that generates Adyen Pay by Link requests from confirmed sales orders and updates prepayment status through Dataverse and webhooks.

d365fo-adyen-paybylink-integration
│
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CHANGELOG.md
│
├── docs
│   ├── overview.md
│   ├── architecture.md
│   ├── functional-flow.md
│   ├── technical-design.md
│   ├── setup-guide.md
│   ├── dataverse-schema.md
│   ├── adyen-api-payloads.md
│   ├── webhook-processing.md
│   └── security-considerations.md
│
├── src
│   ├── xpp
│   │   ├── tables
│   │   ├── classes
│   │   ├── enums
│   │   ├── forms
│   │   ├── data-entities
│   │   ├── services
│   │   └── security
│   │
│   ├── dataverse
│   │   ├── tables
│   │   ├── choices
│   │   └── cloud-flows
│   │
│   └── integration
│       ├── power-automate
│       ├── azure-function
│       └── sample-config
│
├── samples
│   ├── create-payment-link-request.json
│   ├── create-payment-link-response.json
│   ├── webhook-authorisation-event.json
│   └── d365fo-payment-update-request.json
│
└── assets
    └── architecture-diagram-placeholder.png



    Use:

MIT License

This is usually the simplest choice for an open source technical accelerator.


# D365FO Adyen Pay by Link Integration

This open source project provides a reusable integration pattern for Microsoft Dynamics 365 Finance and Operations to generate Adyen Pay by Link payment requests from confirmed sales orders.

When a sales order is confirmed in D365FO, the solution can create a payment request, calculate the required prepayment amount, call Adyen to generate a hosted payment link, and send that link to the customer.

After the customer completes the payment, Adyen webhook responses can update Dataverse and synchronize the payment status back to D365FO. The sales order payment status and prepayment coverage can then be updated automatically.

## Purpose

The purpose of this project is to provide an implementation accelerator for D365FO projects where customer prepayment needs to be collected after sales order confirmation.

## Planned Capabilities

1. Trigger payment link creation from sales order confirmation.
2. Calculate prepayment amount from sales order rules.
3. Create a D365FO payment request record.
4. Store integration tracking data in Dataverse.
5. Generate Adyen Pay by Link through API orchestration.
6. Send payment link to the customer.
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

## Status

This project is currently in planning and initial development stage.

## Disclaimer

This is an open source accelerator and is not an official Microsoft or Adyen product. It should be reviewed, tested, and adapted before use in any production environment.


mkdir d365fo-adyen-paybylink-integration
cd d365fo-adyen-paybylink-integration

git init

mkdir docs src samples assets
mkdir src/xpp src/dataverse src/integration
mkdir src/xpp/tables src/xpp/classes src/xpp/enums src/xpp/forms src/xpp/data-entities src/xpp/services src/xpp/security
mkdir src/dataverse/tables src/dataverse/choices src/dataverse/cloud-flows
mkdir src/integration/power-automate src/integration/azure-function src/integration/sample-config

touch README.md LICENSE CONTRIBUTING.md CHANGELOG.md
touch docs/overview.md docs/architecture.md docs/functional-flow.md docs/technical-design.md docs/setup-guide.md docs/dataverse-schema.md docs/adyen-api-payloads.md docs/webhook-processing.md docs/security-considerations.md
touch samples/create-payment-link-request.json samples/create-payment-link-response.json samples/webhook-authorisation-event.json samples/d365fo-payment-update-request.json

git add .
git commit -m "Initial project skeleton for D365FO Adyen Pay by Link integration"
git branch -M main


