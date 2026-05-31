# n8n Learned Knowledge

## 1. Confirmed Node Types
These node types have been verified from existing workflows in the repository:

- **Core/Trigger Nodes**:
  - `n8n-nodes-base.webhook`
  - `n8n-nodes-base.manualTrigger`
  - `n8n-nodes-base.scheduleTrigger`
  - `n8n-nodes-base.formTrigger`
  - `n8n-nodes-base.githubTrigger`
  - `n8n-nodes-base.emailReadImap`

- **Flow Control Nodes**:
  - `n8n-nodes-base.if`
  - `n8n-nodes-base.filter`
  - `n8n-nodes-base.switch`
  - `n8n-nodes-base.merge`
  - `n8n-nodes-base.splitInBatches`
  - `n8n-nodes-base.splitOut`
  - `n8n-nodes-base.limit`
  - `n8n-nodes-base.stopAndError`
  - `n8n-nodes-base.noOp`
  - `n8n-nodes-base.wait`

- **Action/Transformation Nodes**:
  - `n8n-nodes-base.respondToWebhook`
  - `n8n-nodes-base.httpRequest`
  - `n8n-nodes-base.set`
  - `n8n-nodes-base.code`
  - `n8n-nodes-base.function` (Legacy)
  - `n8n-nodes-base.html`
  - `n8n-nodes-base.markdown`
  - `n8n-nodes-base.stickyNote`

- **Integration Nodes**:
  - `n8n-nodes-base.openAi`
  - `n8n-nodes-base.googleSheets`
  - `n8n-nodes-base.gmail`
  - `n8n-nodes-base.telegram`
  - `n8n-nodes-base.slack`
  - `n8n-nodes-base.github`
  - `n8n-nodes-base.postgres`
  - `n8n-nodes-base.shopify`
  - `n8n-nodes-base.youTube`
  - `n8n-nodes-base.emailSend`

## 2. Confirmed Node Versions
Use these versions when generating nodes:

- `n8n-nodes-base.webhook`: `2`
- `n8n-nodes-base.respondToWebhook`: `1.1`
- `n8n-nodes-base.httpRequest`: `4.2`
- `n8n-nodes-base.set`: `3.4`
- `n8n-nodes-base.code`: `2`
- `n8n-nodes-base.if`: `2.2`
- `n8n-nodes-base.filter`: `2.2`
- `n8n-nodes-base.merge`: `2.1`
- `n8n-nodes-base.openAi`: `1` to `1.3`
- `n8n-nodes-base.googleSheets`: `4.5`
- `n8n-nodes-base.gmail`: `2.1`
- `n8n-nodes-base.emailSend`: `2.1`

## 3. Reference Files
Best examples for structure:
- `workflows/Webhook/1416_Webhook_Respondtowebhook_Create_Webhook.json` (Webhooks & HTTP)
- `workflows/Code/0773_Code_Manual_Update_Triggered.json` (Code & Loops)
- `workflows/Markdown/1571_Markdown_Stickynote_Send.json` (Conditional Logic)
- `workflows/Openai/1256_Openai_Form_Automation_Triggered.json` (AI & Forms)

## 4. Safe Nodes for Generation
You can confidently generate:
`Webhook`, `Respond to Webhook`, `HTTP Request`, `Manual Trigger`, `Schedule Trigger`, `Set`, `Code`, `IF`, `Filter`, `Switch`, `Merge`, `Split In Batches`, `Split Out`, `Limit`, `Stop and Error`, `NoOp`, `Sticky Note`, `Wait`, `OpenAI`, `Google Sheets`, `Gmail`, `Telegram`, `Slack`, `GitHub`, `Postgres`.

## 5. Uncertain/Missing Nodes
- **AI Agent Nodes**: Specific `n8n-nodes-base.aiAgent` or `n8n-nodes-base.basicLLM` were not explicitly found. Use `openAi` node or `httpRequest` for AI tasks.
- **Edit Fields**: Mostly handled by `n8n-nodes-base.set` or as `editFields` parameter in specific integration nodes (e.g., GitHub).

## 6. Fake/Wrong Node Types to Avoid
- `n8n-nodes-base.chatGPT` (Wrong, use `openAi`)
- `n8n-nodes-base.editFields` (Often just a parameter inside `set` version 3+)
- Any node type not found in `workflows/` directory.

## 7. Workflow JSON Rules
- **Expressions**: Must use `={{ ... }}` syntax.
- **Connections**: Map node names to their outputs (main).
- **Metadata**: Include `meta` and `settings` blocks as seen in reference files.
- **IDs**: Use UUID-like strings for node IDs.

## 8. Credential Safety
- **NEVER** include real API keys, passwords, or tokens.
- Use `YOUR_CREDENTIAL_HERE` or specific placeholder strings.
- Credentials in nodes should look like:
  ```json
  "credentials": {
    "openAiApi": {
      "id": "placeholder-id",
      "name": "OpenAi account"
    }
  }
  ```

## 9. Folder Rule
All generated workflows **must** be saved in:
`generated workflows by codex`

## 10. Pre-Generation Checklist
- [ ] Node types are confirmed from the repo.
- [ ] Node versions match the latest confirmed versions.
- [ ] Expressions use `={{ ... }}`.
- [ ] No real credentials included.
- [ ] Connections correctly reference node names.
- [ ] Target folder is `generated workflows by codex`.
