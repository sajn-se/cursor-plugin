# sajn for Cursor

Work with sajn e-signature documents from Cursor, and build and debug integrations against the sajn API.

## What the plugin adds

| Component | What it does |
|---|---|
| `sajn` MCP server | Connects to your sajn workspace at `https://app.sajn.se/api/mcp`. Find, draft, fill in, send, and follow up on documents. Read API logs and webhook deliveries. |
| `sajn-docs` MCP server | Searches the sajn documentation at `https://docs.sajn.se/mcp`. Needs no login. |
| `sajn-documents` skill | Tells the agent how to send a document safely: check readiness, confirm with you, then send. |
| `sajn-api` skill | Tells the agent how to call the REST API, verify webhooks, and debug a live integration. |

## Connect your workspace

1. Install the plugin from the Cursor Marketplace.
2. Open **Cursor Settings > MCP** and connect the `sajn` server.
3. Sign in to sajn, pick the workspace, and choose an access level: read, write, or admin.

The connection acts as you, in that one workspace. Your workspace role and the workspace's AI agent policy still apply, so the agent can never do more than you can. Read access is enough to find and summarize documents. To draft and send, grant write access.

## Example prompts

- "Which agreements are still waiting for a signature, and who are we waiting for?"
- "Draft an NDA from our standard template for Anna at Example AB, and show it to me before you send it."
- "Write a Next.js route that receives sajn webhooks and verifies the signature."
- "Why is my integration getting 422 from sajn? Check the API logs."

## Develop locally

1. Clone this repository into `~/.cursor/plugins/local/sajn`.
2. In Cursor, run **Developer: Reload Window**.
3. Check that the plugin and its components appear under **Customize**.

Run the validator before you open a pull request:

```bash
node scripts/validate.mjs
```

## Learn more

- [sajn MCP server](https://docs.sajn.se/ai/workspace-mcp)
- [sajn API quickstart](https://docs.sajn.se/get-started/quickstart)
- [Verify webhook signatures](https://docs.sajn.se/webhooks/verify-signatures)

## License

MIT
