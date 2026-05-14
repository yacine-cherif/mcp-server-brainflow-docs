# BrainFlow MCP Skill

Query your team's shared email memory from any AI assistant.

## Overview

This skill connects Claude, ChatGPT, Gemini, Cursor, GitHub Copilot, and other MCP-compatible assistants to your BrainFlow database. Ask questions about emails, deals, tasks, and team activity in plain English. The AI translates your question to SQL, queries your data, and returns sourced answers with links to original threads.

## Why shared team memory matters

Every day, critical business knowledge lives in email threads — client commitments, pricing decisions, project timelines, and vendor negotiations. When that knowledge is trapped in individual inboxes, your team pays a hidden tax:

- **New hires spend weeks catching up** on client history that already exists in someone else's inbox
- **Deals stall when account managers are out** because no one knows what was promised last week
- **Teams duplicate work** because marketing doesn't know sales already spoke to that prospect
- **Leadership burns hours in status meetings** instead of reading the actual conversations

BrainFlow turns your team's email history into a shared memory that any AI assistant can query. Ask "What did we commit to Delta Corp?" and get the answer in seconds — sourced, with links to the original threads.

**The result:** less time searching, fewer dropped balls, and a team that operates with full context.

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

## Setup

### 1. Generate an API key

In your BrainFlow dashboard:

1. Go to **Settings → API Keys**
2. Click **Generate key**
3. Name it (e.g. "Claude Desktop")
4. Copy the key — you will only see it once

### 2. Install the MCP bridge

```bash
npm install -g mcp-remote
```

### 3. Add your AI assistant

**Claude (Web)**  
Go to **Customize → Connectors → Add custom connector**  
- **Name:** `BrainFlow`  
- **URL:** `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

**Claude Desktop**  
Add this to your Claude Desktop config file:

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

**ChatGPT** (requires Developer Mode beta)  
Settings → Apps → Advanced settings → Enable Developer Mode → Create app  
- **Name:** `BrainFlow`  
- **URL:** `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

**Gemini**  
```bash
gemini mcp add brainflow https://brain-flow.ai/mcp/sse --header "x-api-key:bf_mcp_YOUR_KEY_HERE"
```

Replace `YOUR_KEY_HERE` with your actual API key.

### 4. Restart and query

Restart your AI assistant. Ask your first question:

> "What did marketing and sales agree on for the Q4 launch timeline?"

Your assistant will query your BrainFlow memory and return a sourced answer.

## GitHub Copilot (VS Code)

Add to your VS Code `settings.json`:

```json
{
  "mcp": {
    "inputs": [],
    "servers": {
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
}
```

## Cursor

1. Open Cursor Settings (Cmd/Ctrl + ,)
2. Go to MCP
3. Add the BrainFlow server config above
4. Query in Composer while you code

## Security

- **Read-only.** Only SELECT queries are allowed. No write, delete, or modify operations.
- **API key required.** Every request must include a valid key.
- **Company-scoped.** Queries are automatically filtered to your company.
- **Audit trail.** Every key usage is tracked with timestamps.
- **Hashed keys.** API keys are SHA-256 hashed. Plaintext is never stored.

## Pricing

The BrainFlow MCP server is **included free** with every BrainFlow subscription. There is no separate charge for MCP access.

| Plan | Users | MCP Access | Rate Limits | Self-hosting |
|------|-------|------------|-------------|--------------|
| **Founder** | 1 | ✅ Full access | Standard | — |
| **Startup** | Up to 10 | ✅ Full access | Higher | — |
| **Corporate** | Up to 100 | ✅ Full access | Highest | ✅ Available |

- **Founder plan:** Full MCP access with standard fair-use rate limits. Perfect for solo founders who want AI-powered memory.
- **Startup plan:** Higher throughput for growing teams up to 10 members.
- **Corporate plan:** Highest throughput, up to 100 team members, and optional self-hosted deployment.

[View full pricing →](https://brain-flow.ai/pricing)

## Requirements

- Active BrainFlow subscription
- At least one team member registered
- Emails already in your BrainFlow memory

## Support

For issues or questions: hello@brain-flow.ai
