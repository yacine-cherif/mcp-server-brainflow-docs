# BrainFlow MCP Server

Connect Claude, ChatGPT, Gemini, Cursor, and GitHub Copilot to your BrainFlow team memory.

## What this does

This MCP server lets AI assistants query your company's shared email memory via natural language. The assistant sends a question, the server translates it to SQL, runs it against your BrainFlow database, and returns a sourced answer.

**Works with:** BrainFlow accounts only. [Sign up](https://brain-flow.ai) to get started.

## Why shared team memory matters

Every day, critical business knowledge lives in email threads — client commitments, pricing decisions, project timelines, and vendor negotiations. When that knowledge is trapped in individual inboxes, your team pays a hidden tax:

- **New hires spend weeks catching up** on client history that already exists in someone else's inbox
- **Deals stall when account managers are out** because no one knows what was promised last week
- **Teams duplicate work** because marketing doesn't know sales already spoke to that prospect
- **Leadership burns hours in status meetings** instead of reading the actual conversations

BrainFlow turns your team's email history into a shared memory that any AI assistant can query. Ask "What did we commit to Delta Corp?" and get the answer in seconds — sourced, with links to the original threads.

**The result:** less time searching, fewer dropped balls, and a team that operates with full context.

---

## What you can ask

### Cross-team handoffs
- "What commitments did sales make to Delta Corp that operations should know about?"
- "Has anyone from engineering spoken to Acme Corp about the API issues?"
- "Which prospects did the BD team reach out to that we already have contracts with?"

### Team activity & decisions
- "Can you summarize the marketing team's exchanges over the last week?"
- "What did the product team decide about the Q3 roadmap in their last sync?"
- "Show me unresolved high-priority tasks across all teams."

### Shared documents & contracts
- "What did legal say about the Alpha contract terms?"
- "Find all Q3 budget discussions across departments."

### Company-wide insights
- "Summarize all client feedback the support team collected this month."
- "Which topics came up most in leadership emails this quarter?"

---

## How it works

### 1. Create your BrainFlow account

Sign up at [brain-flow.ai](https://brain-flow.ai) and create your company workspace.

![Create account](docs/01-create-account.png)

### 2. Get your BrainFlow API key

Generate an API key from your BrainFlow Dashboard. This is what you'll use to connect your AI assistant.

![BrainFlow API key](docs/02-brainflow-api-key.png)

### 3. Include it in CC

Add your BrainFlow email to the CC of any email thread you want to remember. BrainFlow automatically ingests and indexes the conversation.

![Include in CC](docs/03-include-in-cc.png)

### 4. Query with natural language

Connect your AI assistant via MCP and ask questions about any thread your team has shared.

![Query example](docs/04-query-example.png)

---

## Setup

### 1. Generate an API key

In your BrainFlow dashboard:

1. Go to **API Keys**
2. Click **Generate key**
3. Name it (e.g. "Claude Desktop")
4. Copy the key — you will only see it once

### 2. Connect your AI assistant

**Claude (Web)**  
Go to **Customize → Connectors → Add custom connector**  
- **Name:** `BrainFlow`  
- **URL:** `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

**Claude Desktop**  
Go to **Settings → Developer → Edit Config**:

```json
{
  "mcpServers": {
    "brainflow": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://brain-flow.ai/mcp/sse",
        "--header",
        "x-api-key:bf_mcp_YOUR_KEY_HERE"
      ]
    }
  }
}
```

**ChatGPT** (requires Developer Mode)  
Settings → Apps → Advanced settings → Enable Developer Mode → Create app  
- **Name:** `BrainFlow`  
- **URL:** `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

**Gemini**  
```bash
gemini mcp add brainflow https://brain-flow.ai/mcp/sse --header "x-api-key:bf_mcp_YOUR_KEY_HERE"
```

Replace `YOUR_KEY_HERE` with your actual API key. Restart your assistant and start asking questions.

---

## Pricing

The BrainFlow MCP server is **included free** with every BrainFlow subscription. You only pay for your BrainFlow plan — there is no separate MCP charge.

| Plan | Users | MCP Access | Rate Limits | Self-hosting |
|------|-------|------------|-------------|--------------|
| **Founder** | 1 | ✅ Full access | Standard | — |
| **Startup** | Up to 10 | ✅ Full access | Higher | — |
| **Corporate** | Up to 100 | ✅ Full access | Highest | ✅ Available |

- **Founder plan:** Full MCP access with standard fair-use rate limits. Perfect for solo founders who want AI-powered memory.
- **Startup plan:** Higher throughput for growing teams up to 10 members.
- **Corporate plan:** Highest throughput, up to 100 team members, and optional self-hosted MCP server deployment for enterprises with strict compliance requirements.

[View full pricing →](https://brain-flow.ai/pricing)

## Security

- **Read-only.** The server cannot write, delete, or modify anything. It only runs `SELECT` queries.
- **API keys required.** Every request must include a valid key. Keys are managed in your BrainFlow dashboard.
- **Company data secured.** Your data stays in your database. No external APIs are called.
- **Audit trail.** Each key records when it was last used.

For security issues, email hello@brain-flow.ai.
