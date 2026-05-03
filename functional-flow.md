# Functional Flow

## End-to-End Process

1. A user confirms a sales order in D365FO.
2. The system checks whether prepayment is required for the sales order.
3. The system calculates the prepayment amount.
4. D365FO creates a payment request record.
5. The payment request is sent to Dataverse or an integration layer.
6. The integration layer calls Adyen to generate a Pay by Link request.
7. Adyen returns the hosted payment link and payment reference.
8. The payment link is sent to the customer by email, SMS, or another notification method.
9. The customer opens the link and completes the card payment through Adyen.
10. Adyen sends a webhook event with the payment result.
11. The webhook response is stored in Dataverse or processed by the integration layer.
12. D365FO receives the payment status update.
13. The payment request status is updated in D365FO.
14. The Adyen PSP reference is stored for audit and reconciliation.
15. The sales order prepayment coverage is marked as completed.

## Trigger Point

The primary trigger point is sales order confirmation in D365FO.

The first version of this project assumes that the payment request is created after the sales order has been confirmed. This avoids creating payment links for orders that are still being edited or have not yet reached the confirmation stage.

## Payment Status Lifecycle

| Status | Description |
| --- | --- |
| Draft | Payment request created in D365FO but not yet sent to Adyen. |
| LinkCreated | Adyen payment link has been created. |
| Sent | Payment link has been sent to the customer. |
| Paid | Customer payment has been completed successfully. |
| Failed | Payment failed or was refused. |
| Expired | Payment link expired before payment was completed. |
| Cancelled | Payment request was cancelled manually or by system logic. |

## Example Business Scenario

A customer places a sales order worth 1,000 USD. The company requires 30 percent prepayment before fulfillment.

When the sales order is confirmed, D365FO creates a payment request for 300 USD. The integration layer generates an Adyen Pay by Link URL and sends it to the customer. Once the customer pays, Adyen sends a webhook response. D365FO updates the payment request as paid and marks the sales order prepayment requirement as covered.
