---
title: "Introducing Model Context Protocol (MCP)"
source: "https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart"
author:
  - "[[ChatGPT alternative for power users]]"
published: 2024-11-25
created: 2025-03-16
description: "Model Context Protocol (MCP) is an open-source standard released by Anthropic in November 2024 that enables AI models to interact with external data sources through a unified interface."
tags:
  - "clippings"
---
---

1. [The Protocol](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#the-protocol)
1. [Server](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#server)
2. [Client](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#client)
3. [Transport](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#transport)
4. [Host](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#host)
2. [Open-Source Components](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#open-source-components)
1. [Frameworks](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#frameworks)
2. [SDKs](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#sdks)
3. [Ecosystem](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#ecosystem)
4. [Servers](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#servers)
1. [Community Servers](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#community-servers)
3. [Early Adoption and Use Cases](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#early-adoption-and-use-cases)
1. [Sourcegraph Cody](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#sourcegraph-cody)
2. [Zed Editor](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#zed-editor)
4. [Testing MCP using Claude Desktop](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#testing-mcp-using-claude-desktop)
5. [Alternatives](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#alternatives)
6. [What's Next?](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#what-is-next)
7. [Limitations](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#limitations)
8. [Early Thoughts](https://glama.ai/blog/2024-11-25-model-context-protocol-quickstart#early-thoughts)

When large language models first appeared, users had to copy and paste code into a text interface to interact with them. This quickly proved insufficient, leading to custom integrations for better context loading. However, these were fragmented and required individual development. The [Model Context Protocol](https://www.anthropic.com/news/model-context-protocol) (MCP) solves this by offering a universal protocol for efficient AI interaction with both local and remote resources.

Have questions about MCP? Join the [Model Context Protocol Discord](https://discord.gg/TFE8FmjCdS) and ask in the `#general` channel.

## The Protocol

High-level overview of the protocol:

- **Hosts** are LLM applications (like Claude Desktop or IDEs) that initiate connections
- **Clients** maintain 1 connections with servers, inside the host application
- **Servers** provide context, tools, and prompts to clients

### Server

If you are already familiar with [tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use), then MCP will feel familiar.

Let's take a quick look at one of the example server implementatations: the [Brave Search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) server.

Internally, the server implementation defines tools it has access to, and communicates their availability to the client.

server.setRequestHandler(ListToolsRequestSchema, async () \=> ({ tools: \[WEB\_SEARCH\_TOOL, LOCAL\_SEARCH\_TOOL\], }));

Here, `WEB_SEARCH_TOOL` is an object that describes the available tool, e.g.

{ name: "brave\_web\_search", description: "Performs a web search using the Brave Search API, ideal for general queries, news, articles, and online content. " + "Use this for broad information gathering, recent events, or when you need diverse web sources. " + "Supports pagination, content filtering, and freshness controls. " + "Maximum 20 results per request, with offset for pagination. ", inputSchema: { type: "object", properties: { query: { type: "string", description: "Search query (max 400 chars, 50 words)" }, count: { type: "number", description: "Number of results (1-20, default 10)", default: 10 }, offset: { type: "number", description: "Pagination offset (max 9, default 0)", default: 0 }, }, required: \["query"\], }, }

As far as I can tell, this is identical to the [Anthropic Claude Tool Use API](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) or [OpenAI Function Calling](https://platform.openai.com/docs/guides/gpt/function-calling).

It then exposes a request handler.

server.setRequestHandler(CallToolRequestSchema, async (request) \=> { // ... });

The request handler matches the inbound request to a tool, and then calls whatever function is associated with that tool.

case "brave\_web\_search": { if (!isBraveWebSearchArgs(args)) { throw new Error("Invalid arguments for brave\_web\_search"); } const { query, count \= 10 } = args; const results \= await performWebSearch(query, count); return { content: \[{ type: "text", text: results }\], isError: false, }; }

Each MPC server has a URI (e.g., `tool://brave_web_search/brave_web_search`), runs as a separate process, and communicates with clients via a JSON-RPC. Example, you can launch the Brave Search server via the following command:

You can obtain a free Brave Search API key by signing up for a [Brave account](https://api.search.brave.com/).

$ export BRAVE\_API\_KEY\=your\-api\-key $ npx \-y @modelcontextprotocol/server\-brave\-search

### Client

The client needs to know what server it can connect to.

const transport \= new StdioClientTransport({ command: "tool://brave\_web\_search/brave\_web\_search" });

Then, it needs to connect to the server:

await client.connect(transport);

The purpose of the connection is to negotiate capabilities through the protocol. During the connection:

- Client sends initialize request with protocol version and capabilities
- Server responds with its protocol version and capabilities
- Client sends initialized notification as acknowledgment
- Normal message exchange begins

Finally, the client can send messages to the server.

const resources \= await client.request( { method: "brave\_web\_search" }, BraveWebSearchResultSchema );

There are 4 types of messsages defined by the protocol:

- Request: Messages that expect a response
- Notification: Messages that do not expect a response
- Result: Successful responses to requests
- Error: Failure responses to requests

### Transport

MCP supports multiple transport mechanisms:

- Stdio transport
- Uses standard input/output for communication
- Ideal for local processes
- HTTP with SSE transport
- Uses Server-Sent Events for server-to-client messages
- HTTP POST for client-to-server messages

All transports use [JSON-RPC 2.0](https://www.jsonrpc.org/) to exchange messages.

### Host

The host is the application that initiates connections to servers (e.g. Claude Desktop).

The host is responsible for discovering the capabilities of the servers, and planning how to utilize them to solve end user problems.

This part of the protocol is pretty vague. However, as far as I understand, the expectation is that the host implements a custom routing logic. You can see an example of such implementation in my earlier article [Implementing Tool Functionality in Conversational AI](https://glama.ai/blog/2024-10-17-implementing-tool-functionality-in-conversational-ai).

## Open-Source Components

### Frameworks

These are high-level frameworks that make it easier to build MCP servers.

- [FastMCP](https://github.com/jlowin/fastmcp) (Python)
- [FastMCP](https://github.com/punkpeye/fastmcp) (TypeScript)

### SDKs

- [TypeScript](https://github.com/modelcontextprotocol/typescript-sdk)
- [Python](https://github.com/modelcontextprotocol/python-sdk)

### Ecosystem

- [Inspector](https://github.com/modelcontextprotocol/inspector) - Developer tool for testing and debugging MCP servers.
- [Specification](https://github.com/modelcontextprotocol/specification) - Specification for the MCP protocol.

### Servers

- [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) - Secure file operations with configurable access controls
- [GitHub](https://github.com/modelcontextprotocol/servers/tree/main/src/github) - Repository management, file operations, and GitHub API integration
- [Google Drive](https://github.com/modelcontextprotocol/servers/tree/main/src/gdrive) - File access and search capabilities for Google Drive
- [PostgreSQL](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) - Read-only database access with schema inspection
- [Slack](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) - Channel management and messaging capabilities
- [Memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) - Knowledge graph-based persistent memory system
- [Puppeteer](https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer) - Browser automation and web scraping
- [Brave Search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) - Web and local search using Brave's Search API
- [Google Maps](https://github.com/modelcontextprotocol/servers/tree/main/src/google-maps) - Location services, directions, and place details
- [Fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) - Web content fetching and conversion for efficient LLM usage

#### Community Servers

- [MCP YouTube](https://github.com/anaisbetts/mcp-youtube) – Uses `yt-dlp` to download subtitles from YouTube.
- [mcp-security-scanner](https://github.com/DMontgomery40/mcp-security-scanner) – A security vulnerability scanner built with MCP plugins for analyzing JavaScript code.
- [Cloudflare MCP Server](https://github.com/cloudflare/mcp-server-cloudflare) – This is a Model Context Protocol (MCP) server for interacting with Cloudflare services. It provides a unified interface for managing Cloudflare KV Store, R2 Storage, D1 Database, Workers, and Analytics.
- [mcp-get](https://github.com/michaellatman/mcp-get) – A command-line tool for installing and managing Model Context Protocol (MCP) servers.

We now have web-based MCP server directory at [https://glama.ai/mcp/servers](https://glama.ai/mcp/servers).

Future updates to the list will be published to [https://github.com/punkpeye/awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers)

## Early Adoption and Use Cases

Several organizations and tools have already adopted MCP:

- [Sourcegraph Cody](https://sourcegraph.com/blog/cody-supports-anthropic-model-context-protocol): Enhancing context retrieval for coding tasks.
- [Zed Editor](https://zed.dev/blog/mcp): Extending capabilities for developers through MCP.

### Sourcegraph Cody

From the [Cody blog post](https://sourcegraph.com/blog/cody-supports-anthropic-model-context-protocol):

> Here's an example of Cody connecting to a Postgres database to write a Prisma query after looking at the database schema:

![Cody MCP Postgres](https://glama.ai/images/cody-mcp-postgres-GJFBLIVN.png)

Cody connecting to a Postgres database to write a Prisma query after looking at the database schema

### Zed Editor

From the [Zed Editor blog post](https://zed.dev/blog/mcp):

> Here's an example of using a Zed extension for PostgreSQL to instantly inform the model about our entire database schema, so when we ask it to write a query for us, it knows exactly what tables and columns exist, and what their types are.

Using the Postgres Context Server to have the Assistant write a schema-aware query.

Sourcegraph's blog post also has an [example of building Linear integration with TypeScript and MCP](https://sourcegraph.com/blog/cody-supports-anthropic-model-context-protocol#building-a-linear-mcp-integration).

## Testing MCP using Claude Desktop

[Claude Desktop app](https://claude.ai/download) is the easiest way to test MCP.

Open your Claude Desktop App configuration at `~/Library/Application Support/Claude/claude_desktop_config.json` in a text editor.

`~/Library/Application Support/Claude/claude_desktop_config.json` likely will not exist on your machine. You need to create it.

`~/Library/Application Support/Claude/config.json` is a different, unrelated file. Do not edit it.

Add this configuration:

{ "mcpServers": { "brave\_search": { "command": "npx", "args": \["@modelcontextprotocol/server-brave-search"\], "env": { "BRAVE\_API\_KEY": "your-api-key" } } } }

This tells Claude Desktop:

- There's an MCP server named `brave_search`
- Launch it using `npx @modelcontextprotocol/server-brave-search`

Save the file, and restart Claude Desktop.

Now, you can ask Claude Desktop to "search the web for" something.

For example, try asking Claude Desktop to "search the web for glama.ai".

You will be at first prompted to allow Claude Desktop to use MCP:

permission-dialog

![Permission Dialog](https://glama.ai/images/permission-dialog-5AACN2YP.png)

Asking Claude Desktop to use MCP

Click "Allow for This Chat" to allow Claude Desktop to use MCP.

After this, you will see Claude Desktop using the Brave Search MCP server to search the web for "glama.ai" and get the results.

## Alternatives

There are a few open-source projects that come to mind that solve the same problem as MCP.

- [Web Applets](https://github.com/unternet-co/web-applets/) – An open spec & SDK for creating apps that agents can use.

## What's Next?

I don't expect MCP to gain widespread adoption until it has HTTP transport support.

However, I do imagine a future where general purpose LLM clients like [Glama](https://glama.ai/) or Claude Desktop will have a marketplace of MCP servers, and users will be able to plug and play these services into their workflows.

## Limitations

The are very few real-world applications that use MCP today. However, this will change with time.

As for Claude Desktop,

- The setup process for MCP servers in the Claude Desktop app is currently manual.
- You have to give Claude Desktop permission to use MCP every time you re-open the app. See this [workaround](https://x.com/svenmakes/status/1861333236997128345).
- [MCP is only supported locally](https://x.com/alexalbert__/status/1861079950411141180) (servers must run on your own machine).
- Most instructions are for macOS. However, here is someone who [successfully used MCP on Windows](https://gist.github.com/feveromo/7a340d7795fca1ccd535a5802b976e1f).

## Early Thoughts

I think it is a welcome initiative by Anthropic. However, will need some time to see whether it gains traction.

Meanwhile, my money is on the [Computer Use](https://glama.ai/blog/2024-10-22-automate-computer-using-claude) becoming the standard for AI-powered automation, including everything that MCP is trying to solve.

Have questions about MCP? Join the [Model Context Protocol Discord](https://discord.gg/TFE8FmjCdS) and ask in the `#general` channel.

Written by Frank Fiegel ([@punkpeye](https://twitter.com/punkpeye))