# Using AI Assistants

Integrate faster with Crossmint by ingesting the docs into your AI-based code helpers (like Cursor, GitHub Copilot, etc.).

{" "}

<Card title="Markdown docs" icon="book" iconType="duotone" href="https://docs.crossmint.com/llms-full.txt">
  AI assistant ready docs
</Card>

## Integrate with Cursor

1. Navigate to Cursor Settings > Features > Docs

2. Select "Add new doc" and paste the following URL:

```
https://docs.crossmint.com/llms-full.txt
```

3. Use `@docs -> Crossmint` to reference Crossmint's docs in your code.


---

> To find navigation and other pages in this documentation, fetch the llms.txt file at: https://docs.crossmint.com/llms.txt


## Crossmint Docs MCP Server

Learn how to use the **Crossmint Docs MCP Server**

### Server Details

Model Context Protocol (MCP) is a standard that enables AI agents to connect quickly and efficiently to external tools or data sources.

The Crossmint Docs MCP gives your agent the ability to access real-time the Crossmint documentation, which is more efficient than traditional `llms.txt` files. 

Instead of loading the entire documentation with every interaction the server receives your query and returns only the most relevant sections.

- **Name:** Crossmint Docs
- **URL:** https://docs.crossmint.com/mcp
- **Transport:** Streamable HTTP

### Installation

Depending on the tool you use, the configuration may vary. In this guide we'll share the configuration for the most common tools. 

<Tabs>
  <Tab title="Claude Code">
    Run the following command in your terminal:

    ```bash
    claude mcp add --transport http crossmint-docs https://docs.crossmint.com/mcp
    ```
  </Tab>

  <Tab title="Cursor">
    Add it globally by opening the command palette (`Cmd/Ctrl + Shift + P`) and selecting `> Cursor Settings > MCP > Add new global MCP server`:

    ```json
    {
        "mcpServers": {
            "Crossmint Docs": {
                "type": "http",
                "url": "https://docs.crossmint.com/mcp"
            }
        }
    }
    ```
  </Tab>

  <Tab title="VS Code">
    Add it globally by opening the command palette (`Cmd/Ctrl + Shift + P`) and selecting `MCP: Open User Configuration`:

    ```json
    {
        "servers": {
            "Crossmint Docs": {
                "type": "http",
                "url": "https://docs.crossmint.com/mcp"
            }
        }
    }
    ```
  </Tab>
</Tabs>

### Usage

Once you have configured and connected the MCP Server, your agent will have access to a single tool called `SearchCrossmintDocs`. This tool allows it to search through the Crossmint documentation to find relevant information, code examples, API references, and guides.

**Example queries (input):**
- "How to create a wallet on Story Protocol"
- "Amazon integration steps"
- "Headless checkout API examples"
- "How to implement webhooks"

**Example output:**

A list of results that includes the following fields: Title, Link, and Content, along with code examples when available.

```json
{
  "results": [
    {
      "title": "Server Wallets Quickstart ⚡",
      "link": "https://docs.crossmint.com/solutions/story-protocol/wallets/server-side-wallets",
      "content": "In this quickstart, you will create new user wallets on Story...",
      "codeExample": "const response = await fetch('https://staging.crossmint.com/api/2022-06-09/wallets', {\n  method: 'POST',\n  headers: {\n    'X-API-KEY': '<YOUR_API_KEY>',\n    'Content-Type': 'application/json'\n  },\n  body: JSON.stringify({\n    type: '<WALLET_TYPE>',\n    linkedUser: 'email:user@example.com'\n  })\n});"
    },
    {
      "title": "Amazon Integration Steps",
      "link": "https://docs.crossmint.com/solutions/ai-agents/agentic-commerce/inventory",
      "content": "Create a project in the Crossmint Console...",
      "codeExample": "const crossmintOrder = await fetch(`https://${baseUrl}.crossmint.com/api/2022-06-09/orders`, {\n  method: 'POST',\n  headers: {\n    'X-API-KEY': `${API_KEY}`,\n    'Content-Type': 'application/json'\n  },\n  body: JSON.stringify({\n    recipient: {\n      email: 'john@example.com'\n    },\n    lineItems: [{ productLocator: 'amazon:B00O79SKV6' }]\n  })\n});"
    }
  ]
}
```

## Learn more

<CardGroup cols={2}>
  <Card title="Agentic Commerce" icon="cart-shopping" href="/solutions/ai-agents/introduction">
    Allow agents to purchase physical goods programmatically
  </Card>

  <Card title="n8n" icon="diagram-project" href="/solutions/n8n/overview">
    Full-featured n8n integration for Crossmint Wallet and Checkout APIs
  </Card>
</CardGroup>