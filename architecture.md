# Architecture

## High-Level Architecture

The solution uses D365FO as the sales order system of record, Dataverse as the payment tracking or integration state layer, and Adyen as the payment provider.

```text
D365FO Sales Order Confirmation
        |
        v
D365FO Payment Request Table
        |
        v
Dataverse Payment Request Table
        |
        v
Power Automate or Azure Function
        |
        v
Adyen Pay by Link API
        |
        v
Customer Payment Link
        |
        v
Adyen Webhook
        |
        v
Dataverse Payment Response Table
        |
        v
D365FO Payment Status Update
```

## Main Components

| Component | Responsibility |
| --- | --- |
| D365FO sales order confirmation extension | Detects confirmed sales orders requiring prepayment. |
| D365FO payment request table | Stores sales order payment request details. |
| Dataverse payment request table | Stores integration tracking information. |
| Power Automate or Azure Function | Calls Adyen APIs and processes webhook callbacks. |
| Adyen Pay by Link API | Generates the hosted payment link. |
| Adyen webhook | Sends payment result events. |
| D365FO update service | Updates payment request and sales order prepayment status. |

## Integration Pattern

The recommended pattern is to keep D365FO responsible for business rules and payment status updates, while the integration layer handles external API calls and webhook processing.

This avoids direct storage of sensitive payment credentials in X++ code and allows the integration logic to be maintained separately.

## Data Ownership

| Data | Owner |
| --- | --- |
| Sales order | D365FO |
| Prepayment rule | D365FO |
| Payment request | D365FO and Dataverse |
| Payment link | Adyen, tracked in D365FO and Dataverse |
| Card details | Adyen only |
| Payment result | Adyen, then Dataverse and D365FO |
| Audit log | D365FO and integration layer |
