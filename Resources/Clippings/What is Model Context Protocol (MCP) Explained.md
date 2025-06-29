---
title: "What is Model Context Protocol (MCP): Explained"
source: "https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/"
author:
  - "[[Sunil Kumar Dash]]"
published: 2025-03-11
created: 2025-03-16
description: "This blog post explain Model Context Protocol (MCP). You will learn the MCP architecture, it's uses, workflow, and answer FAQs around MCP."
tags:
  - "clippings"
---
## Introduction

Anthropic released MCP (Model Context Protocol) in November 2024. The developer community initially responded positively, yet few realized its full potential. Fast-forward to March 2025, and suddenly, MCP has become the hottest topic in the AI space

This shift became clear when popular consumer IDEs like Cursor, Cline, and Goose officially supported MCP. As more client applications adopted it, server-side integration became increasingly important, amplifying its impact.

Yet, despite all the hype, many developers still wonder: “What exactly is MCP? Should I care? Is this really the next big thing or just another AI fad?” The confusion is accurate and understandable.

In this article, I’ll demystify MCP, clarify its purpose, and unpack why it matters (or doesn’t).

![NearCyan on MCP](https://composio.dev/wp-content/uploads/2025/03/Screenshot-2025-03-10-at-1.33.59-PM-1024x202.png)

- [So, what is MCP?](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-so-what-is-mcp)
- [Why should you care about MCP?](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-why-should-you-care-about-mcp)
- [Is it revolutionary?](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-is-it-revolutionary)
- [MCP Architecture](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-mcp-architecture)
- [Host](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-1-host)
- [Client](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-2-client)
- [Server](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-3-server)
- [The “protocol” in MCP](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-the-protocol-in-model-context-protocol)
- [What MCP looks underneath](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-what-mcp-looks-like-underneath-protocol-layers)
- [Messages](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-1-messages)
- [Transportation Mechanisms](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-2-transport-mechanisms)
- [Lifecycle Management](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#3-lifecycle-management)
- [Cursor x Linear lifecycle example](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-mcp-interaction-lifecycle-cursor-ide-to-linear-slack-example)
- [Drawbacks of MCP](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-limitations-of-mcp)
- [ComposioMCP](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-composio-mcp-managed-mcp-servers-with-built-in-auth)
- [Frequently Asked Questions on MCP](https://composio.dev/blog/what-is-model-context-protocol-mcp-explained/#h-frequently-asked-questions-on-mcp)

## So, what is MCP?

To make things clearer, it’s neither a framework like LangChain nor a tool; it’s a protocol similar to HTTP for the web or SMTP for messaging.

A more relevant example could be LSP (Language Server Protocol), which standardizes adding support for programming languages across an ecosystem of development tools. Similarly, MCP standardizes the integration of additional context and tools into the ecosystem of AI applications.

It provides the universal rules that allow any client to communicate with any server, regardless of who built either component, creating a foundation for a diverse and interoperable AI ecosystem. Anthropic defines it as the USB-C port equivalent for agentic systems. It standardizes the connection between AI applications, LLMs, and external data sources (Databases, Gmail, Slack, etc.).

The Machines are the clients, the peripheral devices are tools, and the MCP is the Type-C port. So, it doesn’t matter who makes the device or peripherals; they work together seamlessly.

![MCP archirecture diagram](https://composio.dev/wp-content/uploads/2025/03/Noah-MCP-1024x576.png)

Image Credit: [Norah Sakal](https://www.linkedin.com/in/norah-klintberg-sakal/)

MCP defines how clients should communicate with servers and how servers should handle tools (APIs, Functions, etc.) and resources (read-only files like logs, db records, etc.) More on this later.

## Why should you care about MCP?

### Benefits of Standardization

1. 1\. **Unified Integration**: A single protocol for connecting any LLM to any tool
2. 2\. **Reduced Development Time**: Standard patterns for resource access and tool execution
3. 3\. **Clear Separation of Concerns**: Data access (resources) and computation (tools) are cleanly separated
4. 4\. **Consistent Discovery**: Uniform mechanisms for finding available capabilities (tools, resources, prompts, roots, sampling)
5. 5\. **Cross-Platform Compatibility**: Tools built for one system work with others

## Is it revolutionary?

Short answer: No.

You can live without MCP. It is not revolutionary but brings standardization to the otherwise chaotic space of agentic development. If your application is MCP client-compliant, you can connect to any MCP client-compliant server. In an alternate world, as a client developer, you have to tailor the servers according to your needs, and others cannot build for your platform. The same is true for server developers.

For example, Inside Cursor, you can connect to any MCP server if they follow the protocols.

At this point, you will be more or less clear about the purpose of the MCP. Now, let’s understand MCP for crystal clear clarity.

## MCP Architecture

The Model Context Protocol has several key components that work together. Here’s a high-level diagram from [Matt Pocock](https://x.com/mattpocockuk/status/1897932371799810314) on Twitter.

![MCP(Model context protocol) flow diagram](https://composio.dev/wp-content/uploads/2025/03/mcp-matt.jpeg)

The complete MCP architecture consists of four parts

- • **Host**: Coordinates the overall system and manages LLM interactions
- • **Clients**: Connect hosts to servers with 1:1 relationships
- • **Servers**: Provide specialized capabilities through tools, resources, and prompts
- • **Base Protocol**: Defines how all these components communicate

In the above chart, the Client and Host are merged; we will keep them separate to clarify things. So, let’s go through each component and understand MCP from within.

### 1\. Host

Hosts are the LLM applications that expect data from servers. Hosts can be an IDE, Chatbot, or any LLM application. They are responsible for

- • Initializing and managing multiple clients.
- • Client-server lifecycle management
- • Handles user authorization decisions
- • Manages context aggregation across clients

Examples are Claude Desktop, Cursor IDE, Windsurf IDE, etc.

### 2\. Client

Each client has these key responsibilities:

- • **Dedicated connections**: Each client maintains a one-to-one stateful connection with a single server. This focused relationship ensures clear communication boundaries and security isolation.
- • **Message routing**: Clients handle all bidirectional communication, efficiently routing requests, responses, and notifications between the host and their connected server. We will see a small example of it in Cursor IDE with Linear and Slack.
- • **Capability management**: Clients monitor what their connected server can do by maintaining information about available tools, resources (contextual data), and prompt templates.
- • **Protocol negotiation**: During initialization, clients negotiate protocol versions and capabilities, ensuring compatibility between the host and server.
- • **Subscription management**: Clients maintain subscriptions to server resources and handle notification events when those resources change.

### 3\. Server

Servers are the fundamental building block that enriches LLMs with external data and context. The key server primitives include:

- • **The tools** are executable functions that allow LLM to interact with external apps. Tools function similarly to functions in [traditional LLM calls](https://composio.dev/blog/tool-calling-in-llama-3-a-guide-to-build-agents/). A tool can be a POST request to API endpoints; for example, a tool defined as LIST\_FILES with a directory name as a parameter will fetch the files in the directory and send them back to the client. The tools can also be API calls to external services like Gmail, Slack, Notion, etc.
- • **Resources:** These are any. Text files, Log files, DB schema, File contents, and Git history. They provide additional context to the LLMs.
- • **Prompt Templates**: Pre-defined templates or instructions that guide language model interactions.

Tools are model-controlled, while Reosuces and Prompts are user-controlled. The models can automatically discover and invoke tools based on a given context.

## The “protocol” in Model Context Protocol

The Protocol forms the foundation of the Model Context Protocol (MCP) architecture. It defines how different components (hosts, clients, and servers) communicate. For more in-depth information, refer to the official [MCP Specification.](https://spec.modelcontextprotocol.io/specification/2024-11-05/)

### What MCP Looks Like Underneath (Protocol Layers)

The protocol consists of several key layers

- • **Protocol Message**: Core JSON-RPC message types
- • **Lifecycle Management**: Client-server connection initialization, capability negotiation, and session control
- • **Transport Mechanisms**: How client-servers exchange messages, usually two types, Stdio for local servers and SSE (Server Sent Events) for hosted servers.
- • **Server Features**: Resources, prompts, and tools exposed by servers
- • **Client Features**: Sampling and root directory lists provided by clients.

Out of the above five, the Base protocol, i.e. JSON-RPC message types and Lifecycle management, is crucial for every MCP implementation. Other components may be implemented as per the needs of the specific application.

### Key parts of the protocol

### 1\. Messages

At its core, MCP uses JSON-RPC 2.0 as its messaging format, providing a standardized way for clients and servers to communicate. The Base Protocol defines three fundamental message types:

1. 1\. **Requests**: Messages are sent to initiate an operation from client to server and vice versa. Example:

```
{
  jsonrpc: "2.0";
  id: string | number;
  method: string;
  params?: {
    [key: string]: unknown;
  };
}
```

1. 2\. **Responses**: Messages sent in reply to requests

```
{
  jsonrpc: "2.0";
  id: string | number;
  result?: {
    [key: string]: unknown;
  }
  error?: {
    code: number;
    message: string;
    data?: unknown;
  }
}
```

1. 3\. **Notifications**: One-way messages that don’t require a response

```
{
  jsonrpc: "2.0";
  method: string;
  params?: {
    [key: string]: unknown;
  };
}
```

### 2\. Transport Mechanisms

The protocol can be implemented over different transport layers depending on deployment needs:

- • **stdio**: Communication over standard input/output streams
- • The client and server receive JSON messages via stdin and respond via stdout
- • Simplifies local process integration and debugging
- • Well-suited for local servers like File, Git server, etc.

![MCP stdio transport](https://composio.dev/wp-content/uploads/2025/03/Screenshot-2025-03-11-at-3.32.08-PM-1024x687.png)

- • **HTTP with Server-Sent Events (SSE)**:
- • Establishes a bidirectional communication pattern over HTTP
- • The server maintains an SSE connection for pushing messages to clients
- • Clients send commands via standard HTTP POST requests
- • Enables distributed architecture with multiple concurrent clients
- • Better suited for hosted servers.

![MCP SSE transport](https://composio.dev/wp-content/uploads/2025/03/Screenshot-2025-03-11-at-5.06.53-PM-1024x687.png)

- • **Custom transports**: Implementations can create additional transport mechanisms as needed

### 3\. Lifecycle Management

The Base Protocol implements a structured lifecycle for connections between clients and servers:

1. 1\. **Initialization Phase**:
- • Clients and servers negotiate protocol versions
- • They exchange capability information (Clients share tools and sampling with servers, and Servers share tools, resources, and prompts with clients).
- • They share implementation details.
2. 2\. **Operation Phase**:
- • Normal protocol communication occurs
- • Both parties respect the negotiated capabilities
3. 3\. **Shutdown Phase**:
- • Graceful termination of the connection

![Client Server life cycle management](https://composio.dev/wp-content/uploads/2025/03/Screenshot-2025-03-11-at-1.08.12-PM-977x1024.png)

Let’s understand what we have learned so far through a simple example. Where

- • The host is Cursor IDE
- • The servers are Linear and Slack

Here’s a detailed workflow of the MCP interaction lifecycle process:

### Initialization Phase

1. 1\. **Connection Establishment**: When a user activates the Linear integration in Cursor IDE, the IDE initiates a connection to the Linear MCP server, typically through stdio or WebSockets.
2. 2\. **Capability Negotiation**:
- • Cursor sends an `initialize` request containing its capabilities (what features it supports)
- • The Linear server responds with its capabilities (available resources, tools, protocol version)
- • Cursor evaluates compatibility, ensuring both sides support the necessary protocol features
3. 3\. **Feature Discovery**:
- • Cursor requests available tools (`tools/list`)
- • Linear responds with tools like `create_ticket`, `assign_ticket`, `add_comment`, etc.
4. 4\. **Ready Notification**: The cursor sends an `initialized` notification to indicate it’s ready to begin normal operation.

### Operation Phase

1. **1\. Tool Execution**:
- • The user tells Cursor, “Create a bug ticket for the login page crash”
- • The LLM in Cursor determines it needs to use a tool
- • Cursor sends a `tools/call` request for `create_ticket` with appropriate parameters
- • The linear server creates the ticket and returns the result
- • The cursor displays the result to the user
2. 2\. **Cross-Service Integration**:
- • The user says, “Notify the team on Slack about this new ticket.”
- • Cursor connects to the Slack MCP server (a separate connection with its own lifecycle)
- • Cursor sends a `tools/call` request to the Slack server
- • The slack server posts the message and returns the success
- • Cursor confirms the notification was sent

### Maintenance Phase

1. 1\. **Health Checks**:
- • The cursor periodically sends `ping` requests to ensure the connection is still alive
- • The linear server responds to confirm the availability

### Termination Phase

1. 1\. **Graceful Shutdown**:
- • When the user closes the workspace or disables the integration
- • The cursor sends a `shutdown` request to the Linear
- • Linear acknowledges with a response
- • The cursor sends an `exit` notification
- • The linear server releases resources associated with the session
2. 2\. **Error Recovery**:
- • If a connection fails unexpectedly
- • Cursor implements retry logic with exponential backoff
- • Upon successful reconnection, the initialization lifecycle begins again

This standardized lifecycle ensures reliable, predictable interactions between any MCP host and server, regardless of their specific implementations. Whether it’s Cursor connecting to Linear for ticket management or Slack for messaging, the same protocol patterns apply, making integrations consistent and interoperable.

## Limitations of MCP

### 1\. Authentication

One of MCP’s current limitations is its lack of a standardized authentication mechanism. The protocol itself doesn’t specify how authentication should be handled, leaving it to implementers to create their own solutions. This can lead to inconsistent security practices across different MCP servers and clients.

### 2\. Lack of reliable Servers

As a relatively new protocol, MCP’s ecosystem is still developing. There are fewer servers, and a lot of applications do not have official MCP servers.

## Composio MCP: Managed MCP servers with built-in Auth

Composio MCP solves the core challenges of authentication and ecosystem maturity. Our managed servers provide built-in authentication support for over 100 applications, automatically handling OAuth, API keys, and basic auth flows. We’ve created pre-built MCP servers for services like Linear, Slack, GitHub, and Google Workspace, so you can focus on building AI experiences rather than integration details.

This eliminates the challenge of maintaining your own MCP servers and handling complex authentication flows. It is suitable for integrating apps with gated resource access.

## Frequently Asked Questions on MCP

## Frequently Asked Questions on MCP

1. 1\. How is MCP different from Langchain or any other framework?  
LangChain is a framework, while MCP is a protocol. Framework, you risk vendor locking, this is not the case with protocols. As long as you follow the protocol guidelines, you will be fine. Even LangChain can adopt MCP as a standard for building stateful agents.
2. 2\. How are MCP servers different from tool calling?  
Isn’t it easier to call tools directly instead of jumping through hoops? Yes, but a protocol ensures that developers define and call tools uniformly, making it easier to develop both clients(host apps) and servers (integrations).
3. 3\. Managing LLM contexts is not that difficult, so why a protocol?  
Again, the goal is to reduce as much developmental overhead as possible. For example, Cursor developers will only care about client implementation, and Linear will only be concerned about server implementation. As long as both comply with the base protocol standard (which we described in detail), both are good.
4. 4\. Is it necessary?  
No, but as the MCP client grows, demand for MCP servers will skyrocket.

I will be adding more FAQs as I come across.