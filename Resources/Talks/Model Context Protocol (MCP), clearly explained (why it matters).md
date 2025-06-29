https://www.youtube.com/watch?v=7j_NE6Pjv-E&ab_channel=GregIsenberg

![[2025-03-15 at 13.22.47.png]]

- It sort of big deal and not really at the same time 😅
- Programmers love standards
	- Why? - It allows us to build system to communicate with each other
	- Example: REST

![[2025-03-15 at 13.25.42.png]]

- LLM in current state - It is only good for predicting the next text
	- By themself they're very dumb
- LLM + Tools - Tool is like an API
	- It becomes bit more powerful when we connect tools with them
	- Problem: Tools needs to be glued by ourself which is tedious
	- Manual work needs to be done
	- Whole system gets impacted with the sources changes little bit (change in API) and as a result it gets cascaded into your system as well

- LLM + MCP
	- Think of every tool that I've to connect to make my LLM valuable as different language
		- Every service provider constructs their API differently
		- Gluing bunch of things together
		- It works but at scale it is difficult 
	- MCP: Layer between your LLM and the services and tools
		- This layer translates all the different languages into unified languages that makes complete sense to the LLM
	- Evaluation of LLM + Tools
	- Service + LLM can communicate efficiently

## MCP Ecosystem

![[2025-03-15 at 13.40.46.png]]
Client - LLM facing side of the ecosystem
Protocol - 2-way connection between client and the server
Server - Translates that external service - it's capabilities and what it can do to the client.

**What's the key benefit?**
When something is changed, the MCP Server (often the official company) has to make the change.

From technical perspective, Anthropic has just created standard. Standard allow us to communicate in a way that make sense to all of us and MCP is that for LLM

==MCP: Making LLM more capable ==

![[2025-03-15 at 13.53.12.png]]