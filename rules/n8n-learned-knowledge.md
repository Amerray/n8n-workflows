# n8n Learned Knowledge

This file summarizes what was learned from this repository before generating any new workflows.

## Study Scope

- Parsed all JSON files in the repository and all workflow/template files under `workflows/`, `templates/`, and other workflow-like folders.
- Read repository guidance in `rules/n8n-workflow-rules.md`.
- Read template documentation in `templates/README.md`.
- Checked supporting catalog/context files under `docs/api/` and `context/`.
- Found thousands of workflow-like JSON objects containing a top-level `nodes` array.

## Confirmed Workflow JSON Structure

Valid examples in this repo are n8n workflow export JSON objects. Common top-level fields include:

- `name`
- `nodes`
- `connections`
- `settings`
- `pinData`
- `staticData`
- `tags`
- `triggerCount`
- `updatedAt`
- `versionId`

Each node commonly contains:

- `parameters`: object shaped specifically for that node type/version
- `id`: unique node id, often UUID-like or readable template id
- `name`: display name used by `connections`
- `type`: internal n8n node type, for example `n8n-nodes-base.webhook`
- `typeVersion`: number, sometimes integer-like (`1`, `2`) and sometimes decimal (`1.1`, `2.2`, `4.5`)
- `position`: two-number array, for example `[460, 300]`
- `credentials`: optional object, always node-specific

Important finding: this repo's workflow nodes use `typeVersion`, not a `nodeVersion` field. `nodeVersion` did not appear on parsed nodes. When the user asks for nodeVersion values, use the confirmed `typeVersion` values from examples.

Connections are keyed by node display name, not node id:

```json
{
  "Source Node Name": {
    "main": [
      [
        {
          "node": "Next Node Name",
          "type": "main",
          "index": 0
        }
      ]
    ]
  }
}
```

IF nodes use two `main` output arrays: output index `0` for true and output index `1` for false.

Expressions are strings, commonly starting with `={{ ... }}` for full expressions, or sometimes `=` for expression fields. Confirmed expression patterns include:

- `={{ $json.field }}`
- `={{ $json.message.text }}`
- `={{ $('Node Name').item.json.field }}`
- `={{ new Date().toISOString() }}`
- `={{ $input.all() }}`
- `{{ $env.BASE_URL }}`
- `{{ $credentials.predefinedCredentialType }}`

## Confirmed Node Types Found in the Repo

The following internal node types were confirmed from parsed workflow/template JSON. This is not permission to use every node by default; future generation should still copy a close example for the requested behavior.

Core/safe workflow-building nodes:

- `n8n-nodes-base.webhook`
- `n8n-nodes-base.respondToWebhook`
- `n8n-nodes-base.if`
- `n8n-nodes-base.set`
- `n8n-nodes-base.code`
- `n8n-nodes-base.httpRequest`
- `n8n-nodes-base.manualTrigger`
- `n8n-nodes-base.scheduleTrigger`
- `n8n-nodes-base.noOp`
- `n8n-nodes-base.stickyNote`
- `n8n-nodes-base.stopAndError`
- `n8n-nodes-base.merge`
- `n8n-nodes-base.switch`
- `n8n-nodes-base.filter`
- `n8n-nodes-base.splitInBatches`
- `n8n-nodes-base.splitOut`
- `n8n-nodes-base.aggregate`
- `n8n-nodes-base.wait`
- `n8n-nodes-base.limit`
- `n8n-nodes-base.sort`
- `n8n-nodes-base.removeDuplicates`

Requested integration/action nodes confirmed:

- `n8n-nodes-base.gmail`
- `n8n-nodes-base.gmailTrigger`
- `n8n-nodes-base.gmailTool`
- `n8n-nodes-base.googleSheets`
- `n8n-nodes-base.googleSheetsTrigger`
- `n8n-nodes-base.googleSheetsTool`
- `n8n-nodes-base.telegram`
- `n8n-nodes-base.telegramTrigger`
- `n8n-nodes-base.telegramTool`
- `n8n-nodes-base.emailSend`
- `n8n-nodes-base.emailReadImap`
- `n8n-nodes-base.emailSendTool`

Other confirmed base nodes include:

- `n8n-nodes-base.airtable`
- `n8n-nodes-base.airtableTrigger`
- `n8n-nodes-base.asana`
- `n8n-nodes-base.asanaTrigger`
- `n8n-nodes-base.discord`
- `n8n-nodes-base.dropbox`
- `n8n-nodes-base.executeCommand`
- `n8n-nodes-base.executeWorkflow`
- `n8n-nodes-base.executeWorkflowTrigger`
- `n8n-nodes-base.extractFromFile`
- `n8n-nodes-base.form`
- `n8n-nodes-base.formTrigger`
- `n8n-nodes-base.function`
- `n8n-nodes-base.functionItem`
- `n8n-nodes-base.github`
- `n8n-nodes-base.githubTrigger`
- `n8n-nodes-base.googleCalendar`
- `n8n-nodes-base.googleCalendarTrigger`
- `n8n-nodes-base.googleDocs`
- `n8n-nodes-base.googleDrive`
- `n8n-nodes-base.googleDriveTrigger`
- `n8n-nodes-base.html`
- `n8n-nodes-base.markdown`
- `n8n-nodes-base.openAi`
- `n8n-nodes-base.postgres`
- `n8n-nodes-base.redis`
- `n8n-nodes-base.rssFeedRead`
- `n8n-nodes-base.slack`
- `n8n-nodes-base.whatsApp`
- `n8n-nodes-base.wordpress`
- `n8n-nodes-base.xml`

Community/package nodes were also present, but should not be generated unless explicitly requested and backed by a close repo example:

- `@n8n/n8n-nodes-langchain.openAi`
- `n8n-nodes-mcp.mcpClient`
- `n8n-nodes-mcp.mcpClientTool`
- `n8n-nodes-exif-data.exifData`
- `n8n-nodes-brightdata.brightData`
- `n8n-nodes-dataforseo.dataForSeo`
- `n8n-nodes-document-generator.DocumentGenerator`

## Confirmed Node Versions Found

Requested/safe nodes:

- `n8n-nodes-base.webhook`: `1`, `1.1`, `2`
- `n8n-nodes-base.respondToWebhook`: `1`, `1.1`
- `n8n-nodes-base.if`: `1`, `2`, `2.1`, `2.2`
- `n8n-nodes-base.set`: `1`, `2`, `3`, `3.1`, `3.2`, `3.3`, `3.4`
- `n8n-nodes-base.code`: `1`, `2`
- `n8n-nodes-base.httpRequest`: `1`, `2`, `3`, `4`, `4.1`, `4.2`
- `n8n-nodes-base.gmail`: `1`, `2`, `2.1`
- `n8n-nodes-base.gmailTrigger`: `1`, `1.1`, `1.2`
- `n8n-nodes-base.googleSheets`: `1`, `2`, `3`, `4`, `4.1`, `4.2`, `4.3`, `4.4`, `4.5`
- `n8n-nodes-base.googleSheetsTrigger`: `1`
- `n8n-nodes-base.telegram`: `1`, `1.1`, `1.2`
- `n8n-nodes-base.telegramTrigger`: `1`, `1.1`, `1.2`
- `n8n-nodes-base.telegramTool`: `1.2`
- `n8n-nodes-base.emailSend`: `1`, `2`, `2.1`
- `n8n-nodes-base.emailReadImap`: `1`, `2`
- `n8n-nodes-base.emailSendTool`: `2.1`

Common modern versions seen frequently:

- Webhook: `typeVersion: 2`
- Respond to Webhook: `typeVersion: 1.1`
- IF: `typeVersion: 2.2`
- Set/Edit Fields: `typeVersion: 3.4`
- Code: `typeVersion: 2`
- HTTP Request: `typeVersion: 4.2`
- Gmail: `typeVersion: 2.1`
- Google Sheets: `typeVersion: 4.5`, with template examples at `4.4`
- Telegram: `typeVersion: 1.2`
- Telegram Trigger: `typeVersion: 1.1` appears frequently in examples
- Email Send: `typeVersion: 2.1`
- Email Read IMAP: `typeVersion: 2`

## Example Files Used as References

General rules and docs:

- `rules/n8n-learned-knowledge.md` (Self-referential, this file)
- `README.md`
- `workflows/` (Numerous examples)

Webhook / Respond to Webhook:

- `workflows/Webhook/1416_Webhook_Respondtowebhook_Create_Webhook.json`

IF / Set / Code / HTTP:

- `workflows/Code/0773_Code_Manual_Update_Triggered.json`
- `workflows/Filter/0801_Filter_Schedule_Import_Webhook.json`
- `workflows/Markdown/1571_Markdown_Stickynote_Send.json`

Gmail / Google Sheets / Telegram:

- `workflows/Openai/1256_Openai_Form_Automation_Triggered.json`
- `workflows/Limit/1645_Limit_Splitout_Automation_Webhook.json`
- `workflows/Noop/0108_Noop_GitHub_Create_Triggered.json`

## Confirmed Representations for Requested Nodes

Webhook:

- Internal type: `n8n-nodes-base.webhook`
- Confirmed versions: `1`, `1.1`, `2`
- Common parameters: `path`, `httpMethod`, `responseMode`, `responseData`, `options`, sometimes `authentication`

IF:

- Internal type: `n8n-nodes-base.if`
- Confirmed versions: `1`, `2`, `2.1`, `2.2`
- Modern structure can use `conditions.options`, `conditions.conditions`, and `combinator`.
- Connections normally have two output arrays under `main`.

Set / Edit Fields:

- Internal type: `n8n-nodes-base.set`
- Confirmed versions: `1`, `2`, `3`, `3.1`, `3.2`, `3.3`, `3.4`
- Modern examples use `parameters.assignments.assignments`.
- The node display name may say "Edit Fields", but the internal type remains `n8n-nodes-base.set`.

Code:

- Internal type: `n8n-nodes-base.code`
- Confirmed versions: `1`, `2`
- Version 2 examples use `parameters.jsCode`.

HTTP Request:

- Internal type: `n8n-nodes-base.httpRequest`
- Confirmed versions: `1`, `2`, `3`, `4`, `4.1`, `4.2`
- Common modern parameters: `url`, `method`, `sendBody`, `specifyBody`, `jsonBody`, `bodyParameters`, `authentication`, `nodeCredentialType`, `options`

Respond to Webhook:

- Internal type: `n8n-nodes-base.respondToWebhook`
- Confirmed versions: `1`, `1.1`
- Common parameters: `respondWith`, `responseBody`, `options`

Gmail:

- Internal type: `n8n-nodes-base.gmail`
- Confirmed versions: `1`, `2`, `2.1`
- Common credential key: `gmailOAuth2`

Google Sheets:

- Internal type: `n8n-nodes-base.googleSheets`
- Confirmed versions: `1`, `2`, `3`, `4`, `4.1`, `4.2`, `4.3`, `4.4`, `4.5`
- Common credential key: `googleSheetsOAuth2Api`
- Modern `documentId` and `sheetName` values often use resource locator objects:

```json
{
  "__rl": true,
  "value": "YOUR_GOOGLE_SHEET_ID",
  "mode": "id"
}
```

Telegram:

- Action node internal type: `n8n-nodes-base.telegram`
- Trigger node internal type: `n8n-nodes-base.telegramTrigger`
- Confirmed action versions: `1`, `1.1`, `1.2`
- Common credential key: `telegramApi`

Email Send:

- Internal type: `n8n-nodes-base.emailSend`
- Confirmed versions: `1`, `2`, `2.1`
- Common credential key: `smtp`

Email Read IMAP:

- Internal type: `n8n-nodes-base.emailReadImap`
- Confirmed versions: `1`, `2`
- Common credential key: `imap`

## Safe Nodes I Can Generate Confidently

These are safe to generate when the requested behavior matches existing examples and credentials are placeholders:

- `n8n-nodes-base.webhook`
- `n8n-nodes-base.respondToWebhook`
- `n8n-nodes-base.if`
- `n8n-nodes-base.set`
- `n8n-nodes-base.code`
- `n8n-nodes-base.httpRequest`
- `n8n-nodes-base.gmail`
- `n8n-nodes-base.googleSheets`
- `n8n-nodes-base.telegram`
- `n8n-nodes-base.emailSend`
- `n8n-nodes-base.emailReadImap`
- `n8n-nodes-base.manualTrigger`
- `n8n-nodes-base.scheduleTrigger`

## Nodes Missing or Uncertain

- AI Agent Nodes: Specific `n8n-nodes-base.aiAgent` or `n8n-nodes-base.basicLLM` were not explicitly found in my initial crawl, but `openAi` is confirmed.
- `n8n-nodes-base.editFields` is not a node type; use `n8n-nodes-base.set`.
- If a requested node behavior is not represented in the repo, I will ask the user to add an exported n8n example containing that node and operation.

## Rules for Future Workflow Generation

1. Never invent node types.
2. Use only internal node `type` values confirmed from repo examples.
3. Prefer modern versions found frequently in the corpus.
4. Use `typeVersion`, not `nodeVersion`.
5. Use `connections` keyed by exact node `name`; connection target `node` values must match existing node names exactly.
6. For IF nodes, map true to `main[0]` and false to `main[1]`.
7. Keep parameters shaped for the chosen node type and `typeVersion`.
8. Keep expressions as strings using confirmed n8n expression syntax such as `={{ ... }}`.
9. Credentials must always be placeholders. Never include real ids, tokens, passwords, API keys, cookies, or private account names.
10. Generated workflows must be valid JSON and saved inside `generated workflows by codex`.
11. Do not connect to local n8n.
12. Do not use MCP.
13. Do not run unsafe commands.
14. When unsure, stop and request the exact exported n8n example needed.

## Common Fake or Wrong Node Types to Avoid

- `n8n-nodes-base.googleGmail`
- `n8n-nodes-base.editFields` (Internal type is `n8n-nodes-base.set`)
- `n8n-nodes-base.chatGPT` (Use `openAi`)
- `n8n-nodes-base.http` (Use `httpRequest`)

## Common Causes of Broken "?" Nodes in n8n

- Using a display name instead of the internal node type.
- Wrong casing in node type.
- Missing `n8n-nodes-base.` prefix.
- Using `nodeVersion` instead of `typeVersion`.
- Using a node type not confirmed in this repo.

## Pre-Generation Checklist
- [ ] Node types are confirmed from the repo.
- [ ] Node versions match the confirmed `typeVersion` values.
- [ ] Expressions use `={{ ... }}`.
- [ ] No real credentials included.
- [ ] Connections correctly reference node names.
- [ ] Target folder is `generated workflows by codex`.
