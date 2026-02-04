---
title: API Anatomy: Single Payment Requests
description: A technical breakdown of the Payment Intent object and JSON data structures.
date: 2026-02-02
category: Reference
tags: [Payments, JSON, API Fundamentals]
author: [Your Name]
layout: doc
---
## API Anatomy: Payment Processing

Payment Intent API does three critical things:
* creates a record of the transaction to make sure that the customer is not charged twice for the same transaction.
* handles the complex math of currency conversion using Minor Units to make sure that nothing is lost in the process.
* tracks the transaction from it’s lifespan.
1. Required Payment Method
2. Processing
3. Succeeded, Denied or Canceled by Customer/Client

### Payment Intent Object

The Payment Intent is the core resource used to track a transaction from creation through the checkout flow. It ensures that you don't overcharge a customer or double-process a single order.

### Authentication

All API requests must be authenticated using Secret Keys. These keys must be included in the header of every request.  **Security Note:** Never share your Secret Keys or commit them to a public repository. Treat them like the physical keys to your vault.

| Header | Value | Description |
|:--- | :--- | :---|
| Authorization |Bearer <SECRET_KEY> | The standard method for passing your unique API Key |
| Content-Type | application/json | Informs the server that the request body is formatted as JSON |

### The Response Object

{
  "id": "pay_9f2a83bc11",
  "object": "payment_intent",
  "amount": 5000,
  "currency": "usd",
  "status": "succeeded",
  "livemode": false,
  "created": 1707052261
}

| Field | Type | Description |
| :--- | :--- | :--- |
| object | String | The type of resourse returned (E. G. payment_intent). |
| livemode | Boolean | Returns false if using test keys; true if this involves real currency. |

### Note on Time-Handling

**Why use Unix Timestamps?** You’ll notice dates appear as 10-digit numbers, such as 1707052261. This is a Unix Timestamp, which tracks time by counting the total seconds elapsed since the "Unix Epoch" (January 1, 1970). By using a single, universal counter, our API avoids the common errors caused by global time zones and leap years, ensuring that a payment made in London and a payment made in Tokyo are recorded with the same mathematical precision.

### The Error Object

"{
  "error": {
    "code": "card_declined",
    "decline_code": "insufficient_funds",
    "doc_url": "https://docs.api.com/error-codes#insufficient_funds",
    "message": "The card has insufficient funds to complete the purchase.",
    "type": "card_error"
  }
}"

| Code | Type | Recovery Step |
| :--- | :---: | :--- |
| card_declined | User Error | Ask the customer to use a different payment method. |
| rate_limit_reached | Integration Error | Wait a few seconds before retrying the request. |
| authentication_error | Security Error | Check that your Secret API Key is valid and active. |

### Best Practice: Contextual Error Documentation 

Notice the doc_url field in the error response. Providing a direct link to the relevant troubleshooting guide within the API response is a hallmark of "Developer-First" documentation. It reduces Mean Time to Resolution (MTTR) by placing the solution exactly where the problem is discovered—in the terminal.