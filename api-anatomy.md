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
