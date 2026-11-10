---
name: sajn-documents
description: Work with documents in a sajn workspace through the sajn MCP server. Use when the user asks to find, draft, fill in, send, remind, or follow up on agreements, contracts, or anything sent for e-signature in sajn.
---

# Work with sajn documents

The `sajn` MCP server acts in one sajn workspace, as the user who approved the connection. It sends its own instructions about statuses, costs, and what stays in the app. Follow them.

## Find the right tool

- Start with the listed tools: `findDocuments`, `getDocument`, `getParties`, `getFields`, `getSettings`, `getDocumentReadiness`, `summarizeContent`, `findTemplates`, `getTemplate`, `findContacts`, `createDocument`, `addParty`, `setFieldValues`, `addDocumentFile`, `createContact`, and `sendDocument`.
- For anything else, call `findTools` with a short description of the task. Run what it returns with `runReadOnlyTool` or `runTool`.
- If `findTools` lists the tool under `blockedByPolicy`, the workspace has switched it off for AI agents. Tell the user; don't search again.
- If no tool covers the task, call `reportMissingCapability` and tell the user to do it in the sajn app.

## Send a document

1. Find a template with `findTemplates`, or create a blank document with `createDocument`.
2. Add each party with `addParty`. Ask how each party signs and verifies. Don't pick BankID for them.
3. Fill the values with `setFieldValues`.
4. Call `getDocumentReadiness` and fix every blocker it reports.
5. Show the user the document, the parties, and the signing methods. Wait for a clear yes.
6. Call `sendDocument`.

`sendDocument` emails or texts real people, and a BankID signature costs money. Never send, remind, withdraw, or delete without the user's go for that document.

## Follow up

- To see what waits for a signature, call `findDocuments` filtered by status. Call `getParties` to see who hasn't signed.
- To remind a party, run `sendPartyReminder` through `runTool`. Confirm who gets the reminder first.
- A sent document is locked. To change it, run `withdrawDocument` through `runTool`. Tell the user first that the parties are notified.

## When a tool is missing

The tools the connection can reach depend on three things: the access level the user granted at consent (read, write, or admin), their role in the workspace, and the workspace's policy for AI agents. If a write tool is missing, tell the user to reconnect the `sajn` server in **Cursor Settings > MCP** and grant write access. Don't try to work around a permission.
