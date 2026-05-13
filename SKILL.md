# BrainFlow MCP Skill

Query your team's shared email memory from any AI assistant.

## Overview

This skill connects Claude Desktop, Cursor, GitHub Copilot, and other MCP-compatible assistants to your BrainFlow database. Ask questions about emails, deals, tasks, and team activity in plain English. The AI translates your question to SQL, queries your data, and returns sourced answers with links to original threads.

## What you can ask

### Sales & clients
- "What's the average reply time for client Acme Corp?"
- "How many offers did we send last week?"
- "Which deals are stuck longer than 14 days?"

### Team activity
- "Who sent the most emails last month?"
- "Show me unresolved high-priority tasks."
- "What did we commit to Beta Inc in March?"

### Documents & contracts
- "Which emails mention the Alpha contract?"
- "Find the latest pricing document."

### Trends & insights
- "How many emails did we receive this week?"
- "Which clients emailed us about GDPR?"

## Setup

### 1. Generate an API key

In your BrainFlow dashboard:

1. Go to **API Keys**
2. Click **Generate key**
3. Name it (e.g. "Claude Desktop")
4. Copy the key — you will only see it once

### 2. Connect to Claude Desktop

In Claude Desktop, go to **Settings → MCP Servers → Add Custom Server**.

- **Name:** `BrainFlow`
- **URL:** `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

Replace `YOUR_KEY_HERE` with your actual API key.

### 3. Restart and query

Restart Claude Desktop. Ask your first question:

> "What did we discuss with Acme Corp last month?"

Claude will query your BrainFlow memory and return a sourced answer.

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

If your client does not support headers, use the query param URL: `https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE`

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

## Requirements

- Active BrainFlow subscription (Startup or Corporate)
- At least one team member registered
- Emails already in your BrainFlow memory

## Support

For issues or questions: hello@brain-flow.ai
