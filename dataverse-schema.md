# Dataverse Schema

## Purpose

Dataverse can be used as an integration state layer between D365FO, Power Automate, Azure Functions, and Adyen.

## Table: isw_adyenpaymentrequest

| Column | Type | Description |
| --- | --- | --- |
| isw_name | Text | Display name or payment request number. |
| isw_legalentity | Text | D365FO legal entity. |
| isw_salesid | Text | Sales order number. |
| isw_custaccount | Text | Customer account. |
| isw_customeremail | Text | Customer email address. |
| isw_amount | Decimal | Payment amount. |
| isw_currencycode | Text | Currency code. |
| isw_merchantreference | Text | Merchant reference sent to Adyen. |
| isw_pspreference | Text | Adyen PSP reference. |
| isw_paymentlinkurl | Text | Hosted payment link. |
| isw_paymentstatus | Choice | Payment request status. |
| isw_expirydatetime | DateTime | Payment link expiry. |
| isw_lastwebhookdatetime | DateTime | Last webhook event date and time. |
| isw_errormessage | Multiline text | Last error message. |

## Table: isw_adyenpaymentresponse

| Column | Type | Description |
| --- | --- | --- |
| isw_name | Text | Response record name. |
| isw_merchantreference | Text | Merchant reference from webhook. |
| isw_pspreference | Text | Adyen PSP reference. |
| isw_eventcode | Text | Adyen event code. |
| isw_success | Yes or No | Indicates successful payment event. |
| isw_eventdatetime | DateTime | Event date and time. |
| isw_rawpayload | Multiline text | Raw webhook payload for troubleshooting. |
| isw_processed | Yes or No | Indicates whether D365FO was updated. |
| isw_processingmessage | Multiline text | Processing notes or errors. |

## Choice: isw_paymentstatus

| Value | Meaning |
| --- | --- |
| Draft | Request created but not submitted. |
| LinkCreated | Payment link created. |
| Sent | Payment link sent to customer. |
| Paid | Payment completed successfully. |
| Failed | Payment failed. |
| Expired | Payment link expired. |
| Cancelled | Payment request cancelled. |
