# Project Overview

## Project Name

D365FO Adyen Pay by Link Integration

## Purpose

This project provides an open-source integration accelerator for Microsoft Dynamics 365 Finance and Operations. The goal is to automate the creation of Adyen Pay by Link payment requests when a sales order is confirmed and prepayment is required.

## Problem Statement

In many D365FO implementations, customer prepayment collection is handled outside the sales order process. Users may manually create payment links, email customers, check payment status in the payment provider portal, and then update the sales order manually.

This creates delays, manual effort, reconciliation issues, and gaps between payment status and sales order processing.

## Proposed Solution

The proposed solution creates a structured payment request from D365FO once the sales order is confirmed. The payment request is sent to an integration layer, which generates an Adyen Pay by Link request. The customer receives the hosted payment link and completes the payment externally through Adyen.

Adyen webhook responses are then processed and used to update Dataverse and D365FO. Once the payment is confirmed, the sales order prepayment status can be marked as covered.

## Business Value

1. Reduces manual payment follow-up.
2. Connects payment collection with the sales order lifecycle.
3. Improves visibility of prepayment status.
4. Provides audit tracking for payment requests and responses.
5. Supports automation through Dataverse, Power Automate, or Azure Functions.
6. Keeps card processing outside D365FO and Dataverse.

## Intended Audience

1. D365FO technical consultants.
2. D365FO functional consultants.
3. Solution architects.
4. Integration developers.
5. Payment implementation teams.
6. Customers using Adyen with Dynamics 365.
