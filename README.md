# BrainFlow MCP Server

Connect Claude Desktop, Cursor, and GitHub Copilot to your BrainFlow team memory.

## What this does

This MCP server lets AI assistants query your company's shared email memory via natural language. The assistant sends a question, the server translates it to SQL, runs it against your BrainFlow database, and returns a sourced answer.

**Works with:** BrainFlow accounts only. [Sign up](https://brain-flow.ai) to get started.

---

## Setup

### 1. Generate an API key

In your BrainFlow dashboard:

1. Go to **API Keys**
2. Click **Generate key**
3. Name it (e.g. "Claude Desktop")
4. Copy the key — you will only see it once

### 2. Connect to Claude Desktop

Add this to your Claude Desktop config:

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

Replace `YOUR_KEY_HERE` with your actual API key.

**Clients without header support:** If your MCP client (e.g. Kimi, some VS Code extensions) does not support custom headers, append the key as a query parameter instead:

```
https://brain-flow.ai/mcp/sse?api_key=bf_mcp_YOUR_KEY_HERE
```

Restart Claude. Start asking questions.

---

## Security

- **Read-only.** The server cannot write, delete, or modify anything. It only runs `SELECT` queries.
- **API keys required.** Every request must include a valid key. Keys are managed in your BrainFlow dashboard.
- **Company data secured.** Your data stays in your database. No external APIs are called.
- **Audit trail.** Each key records when it was last used.

For security issues, email security@brain-flow.ai.
