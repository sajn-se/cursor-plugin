---
name: sajn-api
description: Build and debug code that calls the sajn REST API or receives sajn webhooks. Use when the user writes an integration with sajn, sends documents for signing from code, handles sajn webhook events, or debugs failing sajn API requests or webhook deliveries.
---

# Build and debug a sajn integration

Use the `sajn-docs` MCP server for endpoint shapes, field names, and event payloads. It needs no login. Don't guess a field name; search the docs.

## Call the API

- Base URL: `https://app.sajn.se/api/v1`. There is no separate sandbox host.
- Send `Authorization: Bearer <key>` and `Sajn-Version: 2026-10` on every request. Pin the version; don't omit it.
- Read the key from an environment variable such as `SAJN_API_KEY`. Never hard-code it or commit it.
- A production key starts with `sajn_sk_`. A sandbox key starts with `sajn_dev_`. Build and test against a sandbox: BankID is mocked, signed PDFs are watermarked, and nothing is billed.
- An error body carries `code`, `message`, and `requestId`. Log `requestId`; sajn support needs it.
- A document needs `expiresAt` before you can send it.
- To act for other sajn users instead of your own workspace, use OAuth. To choose, search `sajn-docs` for "choosing authentication".

## Receive webhooks

- sajn signs deliveries with Standard Webhooks. Verify every delivery with the `standardwebhooks` library and the endpoint secret (`whsec_...`) before you act on it.
- Verify against the raw request body. A body parser that runs first breaks the signature.
- Deliveries retry, so handle each `webhook-id` once.

## Debug a live integration

If the `sajn` MCP server is connected, read the real traffic instead of guessing:

- Run `findApiLogs` through `runReadOnlyTool` to find a failing request. Run `getApiLog` to read its request and response bodies.
- Run `findWebhookDeliveries` to find failed deliveries. Run `getWebhookDelivery` to see the status code and body your endpoint returned.

The API log tools need the workspace permission to manage API keys. The webhook tools need the permission to manage webhooks. If `findTools` doesn't return them, tell the user which permission is missing.
