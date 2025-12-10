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

### Server Details

Model Context Protocol (MCP) is a standard that enables AI agents to connect quickly and efficiently to external tools or data sources.

The Crossmint Docs MCP Server provides real-time access to the Crossmint documentation, offering a more efficient alternative to traditional `llms.txt` files. Instead of loading the entire documentation with every interaction which unnecessarily increases token usage the server receives your query and returns only the most relevant sections. This approach modularizes token consumption, improves performance, and ensures that the latest version of the documentation is always consulted.

- **Name:** Crossmint Docs
- **URL:** https://docs.crossmint.com/mcp
- **Transport:** Streamable HTTP

### Installation

Depending on the tool you use, the configuration may vary.

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

Once you have configured and connected the MCP Server, you will have access to a single tool called `SearchCrossmintDocs`. This tool allows you to search through the Crossmint documentation to find relevant information, code examples, API references, and guides.

**Input**

Your query message.

**Output**

A list of results that includes the following fields: Title, Link, and Content, along with code examples when available.

### Mintlify

The Crossmint documentation and its MCP Server are powered by **Mintlify**. You can find more detailed technical information in their [documentation](https://www.mintlify.com/docs/ai/model-context-protocol#using-your-mcp-server).