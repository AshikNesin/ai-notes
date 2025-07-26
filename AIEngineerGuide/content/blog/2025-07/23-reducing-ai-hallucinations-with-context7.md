---
title: Reducing AI Hallucinations with Context7
date: 2025-07-23
description: 
tags:
  - TIL
  - context7
  - hallucination
url: blog/reducing-ai-hallucinations-with-context7
via_url:
---
LLM have cut off date which means it might not have up to date information about recent things like documentation which leads to hallucinations (AI generating something on it's own).

Once of the way to reduce the hallucination, is to pass the information to LLM when generating something.

[Context7](https://context7.com/) makes it easy for you to do it for any documentation.

Basically what they've done is they've indexed lots of documentation and make it available for anyone to use for free.

Basically you can wire this up with your AI IDE like Cursor or anywhere it supports MCP like claude code.


![[2025-07-23 at 20.58.41@2x.png]]
![[2025-07-23 at 21.13.32@2x.png]]
## Remote MCP

Their remote MCP is 👉 `https://mcp.context7.com/mcp`

You can refer to their docs on how to set it up for your tool. And yeah, the entire thing is open source - MIT  license.

[GitHub - upstash/context7: Context7 MCP Server -- Up-to-date code documentation for LLMs and AI code editors](https://github.com/upstash/context7)

Happy building apps!