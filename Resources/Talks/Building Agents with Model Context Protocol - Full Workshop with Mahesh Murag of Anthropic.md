https://www.youtube.com/watch?v=kQmXtrmQ5Zg&t=404s&ab_channel=AIEngineer

![[2025-03-06 at 09.20.49.png]]

![[2025-03-06 at 09.21.24.png]]

- It is like API & LSP.
- LSP is big part of the inspiration for MCP. You can build X feature once and any IDE that supports LSP.
- MCP - Standardize the interaction b/w AI applications interacts with external systems
- Part of protocol
	- Prompts
	- Tools
	- Resources

Without MCP: Everybody does it in their own way
![[CleanShot 2025-03-06 at 18.20.22.png]]


With MCP
![[CleanShot 2025-03-06 at 18.20.51.png]]

MCP Server: It is the way of federating the access to various systems and tools that are relavent to the AI application

**Why MCP?**
![[CleanShot 2025-03-06 at 18.27.36.png]]

![[CleanShot 2025-03-06 at 18.30.08.png]]

Building with MCP

MCP Client - IDE
MCP Server

![[2025-03-15 at 11.45.38.png]]

![[2025-03-15 at 11.58.08.png]]

![[2025-03-15 at 11.58.42.png]]

Number of tools: 50-100 it is good with modern LLM (Claude). Technically no limit but don't overwhelm with context
- Tool for searching tools 😅
- Hierarchical group of tools
	- 1 for read
	- 1 for write

- Cline has MCP auto generator tool
- Versioning - there is no best practices yet but as long as MCP standard is followed it should not lead to any breaking changes

## Sampling

![[2025-03-15 at 12.33.53.png]]

![[2025-03-15 at 12.36.19.png]]

 Why MCP server instead or regular HTTP server?
  - Composability and layered approach
  - Each of these can be an agents
  - Protocol capabilities
	  - Resource notifications
	  - Server to client communication
	  - Server requesting more information from the client (that are built into the MCP protocol itself)
  - They're more intelligent than just exposing data to the LLM. Each of them has autonomy. They're more like agent- any server can interact with another

- MCP protocol exposes metadata between the server and the client
![[2025-03-15 at 12.54.28.png]]

What's next for MCP?

MCP Inspector 
![[2025-03-15 at 12.56.38 1.png]]

Auth is added in MCP spec recently
- Server handles the handshake
- Server holds the oAuth tokens and stuffs
- Server then federates the interaction between the user and the server

![[2025-03-15 at 13.06.31.png]]

Open - but hosted by MCP team

![[2025-03-15 at 13.08.57.png]]

Verification
![[2025-03-15 at 13.10.41.png]]

![[2025-03-15 at 13.11.28.png]]

---

> Generated using Google Notebook based on the transcript

**1. Introduction to MCP and its Motivation:**

- **Core Concept:** Models are only as good as the context provided to them. This is the central motivation behind MCP.
- _"So our motivation behind MCP was the core concept that models are only as good as the context we provide to them."_
- **Evolution from Chatbots:** Earlier AI assistants relied on manual context input (copy-pasting, typing). MCP addresses the shift towards systems with direct hooks into user data and context for more powerful and personalized AI applications and agents.
- **MCP as an Open Protocol:** MCP is designed as an open protocol to enable seamless integration between AI apps and agents with user tools and data sources.
- _"And so we saw the opportunity to launch MCP, which is an open protocol that enables seamless integration between AI apps and agents and your tools and data sources."_
- **Inspiration from Existing Protocols:** MCP draws inspiration from established protocols like APIs (standardizing web app interaction) and LSP (Language Server Protocol, standardizing IDE interaction with language-specific tools). LSP, in particular, serves as a key inspiration, aiming to standardize interaction between AI applications and external systems similar to how LSP standardizes IDE-language tool interaction.
- _"LSP came later, and that standardizes how IDEs interact with language specific tools. LSP is a big part of our inspiration..."_
- **Three Primary Interfaces of MCP:** The protocol standardizes interaction through three main interfaces:
- **Prompts:** User-controlled predefined templates for common interactions.
- **Tools:** Model-controlled functionalities exposed by servers for the LLM to invoke.
- **Resources:** Application-controlled data exposed by servers for the application to utilize.

**2. The Problem MCP Solves: Fragmentation:**

- **Pre-MCP Landscape:** Anthropic observed significant fragmentation in how different teams and the broader industry were building AI systems. This included inconsistent custom implementations for accessing context, varying prompt logic, and different approaches to tool and data access federation.
- _"And what we were seeing is across the industry, but also even inside of the companies that we were speaking to, there was a ton of fragmentation about how to build AI systems in the right way."_
- **Standardized AI Development with MCP:** MCP aims to create a world of standardized AI development by providing a common interface for AI clients (applications, IDEs, agents) to connect to MCP servers without requiring additional work for each new integration.
- _"The world with MCP is a world of standardized AI development... there's now a standard interface for any of those client applications to connect to any MCP server with zero additional work."_
- **MCP Server Functionality:** An MCP server acts as a wrapper or a way to federate access to various relevant systems and tools, such as databases, CRMs (like Salesforce), and local system resources (like version control).

**3. Value Proposition of MCP:**

- **For Application Developers:** MCP compatibility allows clients to connect to any server with minimal effort, eliminating the "N times M problem" of numerous potential interactions.
- _"The value for application developers is once your client is MCP compatible, you can connect it to any server with zero additional work."_
- **For Tool and API Providers:** Building an MCP server once grants access to a wide range of MCP-compatible AI applications, increasing adoption.
- _"If you're a tool or API provider or someone that wants to give LLMs access to the data that matters, you can build your MCP server once and see adoption of it everywhere across all of these different AI applications."_
- **For End Users:** MCP leads to more powerful and context-rich AI applications capable of understanding user context and taking real-world actions.
- _"For end users, obviously, this leads to more powerful and context rich AI applications."_
- **For Enterprises:** MCP provides a clear separation of concerns, enabling different teams to own and maintain specific data infrastructure interfaces (as MCP servers) while other teams can build AI applications in a centralized and efficient manner, similar to a microservices architecture.
- _"For enterprises, there's now a clear way to separate concerns between different teams that are building different things on the roadmap... like a world with microservices as well..."_

**4. MCP Adoption and Usage:**

- **Growing Adoption:** MCP has seen significant early adoption in AI applications, IDEs (allowing context integration during coding), and server-side development.
- **Community and Official Servers:** Over 1,100 community-built open-source servers exist, alongside official integrations from companies like Cloudflare and Stripe. There's also active open-source contributions to the core protocol and infrastructure.

**5. Building with MCP: Tools, Resources, and Prompts (Detailed):**

- **Tools (Model Controlled):**Servers expose tools to client applications.
- The LLM within the client decides when to invoke these tools based on descriptions provided in the server definition.
- Tools enable actions like data retrieval (read), data submission/action taking (write), database updates, and local file system operations.
- **Resources (Application Controlled):**Servers expose data (images, text files, JSON, etc.) to the application.
- The client application determines how to use these resources.
- Resources facilitate richer interactions beyond text-based chatbots.
- Use cases include serving static or dynamic files, with the server potentially interpolating information based on user or application context.
- In Anthropic's "Cloud for Desktop," resources manifest as attachments that users can manually or automatically (by model decision) include in the conversation.
- **Prompts (User Controlled):**Predefined templates for common interactions with a specific server.
- Users invoke these prompts (e.g., through slash commands in IDEs like Zed).
- The client application interpolates user input (e.g., a PR ID) into the predefined prompt template provided by the MCP server.
- Useful for standardizing interactions like document Q&A with specific formatting or data presentation rules.

**6. MCP and Agent Frameworks:**

- **Complementary Nature:** MCP and agent frameworks are seen as complementary rather than replacements for each other.
- **Connecting Existing Systems:** Agent frameworks can use MCP to easily connect to various servers and access tools and resources in a standardized way through connectors or adapters (e.g., LangGraph has released MCP connectors).
- **Focus of Agent Frameworks:** Agent frameworks provide value in knowledge management, agentic loops, and how agents respond to data, while MCP focuses on the standardized layer for bringing context to the agent or framework.
- **Abstraction Layer:** MCP acts as an abstraction layer, allowing agent builders to focus on the agent's core loop, context management, and model selection, rather than the specifics of individual server integrations.

**7. Demo: Cloud for Desktop and GitHub/Asana Integration:**

- The demo showcases "Cloud for Desktop" (an MCP client) interacting with GitHub and Asana through MCP servers.
- The user instructs Claude to triage issues from a GitHub repository. Claude (the model) automatically invokes the "list issues" tool from the GitHub server.
- Claude then triages the top issues and adds them as tasks to an Asana project. This involves Claude using tools from the Asana server (e.g., "list workspaces," "search projects," "add task").
- Key takeaways:
- The Asana and GitHub servers were community-built with minimal code.
- MCP enables different tools built by different entities to interoperate within a central application.
- "Cloud for Desktop" acts as a central dashboard for accessing context and running daily tasks.

**8. MCP as the Foundational Protocol for Agents:**

- **Growing Importance:** MCP is anticipated to become the foundational protocol for agents due to its protocol features and the increasing capabilities of models to effectively utilize provided data.
- **MCP and Augmented LLMs:** MCP aligns with the concept of an "augmented LLM" (as described in Anthropic's blog), where the LLM is enhanced with access to retrieval systems, tools, and memory. MCP provides the standardized bottom layer for these augmentations.
- **Enabling Agent Discovery and Expansion:** MCP allows agents to discover and interact with new capabilities and data sources even after initialization, without needing to be pre-programmed with all necessary integrations.
- **Focus on the Core Agent Loop:** MCP allows agent builders to concentrate on the core logic of the agent (task execution loop, context management, memory usage) while relying on MCP for standardized context acquisition.

**9. Demo: MCP Agent Framework (Last Mile AI):**

- Demonstrates an open-source framework called "MCP agent" for building agents using MCP.
- A simple application (around 80 lines of Python) defines agents for researching quantum computing's impact on cybersecurity.
- The task involves sub-agents for research, fact-checking, and report writing.
- Each sub-agent is given access to specific MCP servers (Brave for search, a fetch tool, and the file system) through declarative configuration. The agent builder did not build these servers.
- The framework handles plan formation (a series of steps involving tool invocations).
- MCP acts as an abstraction layer, allowing the agent builder to focus on the agent's task and available servers/tools.
- The demo shows the agent autonomously performing research, fact-checking, and generating a report by interacting with the specified MCP servers.

**10. Protocol Capabilities for Agents:**

- **Sampling:** Allows an MCP server to request LLM inference calls (completions) from the client.
- This enables servers to access intelligence without needing to host or directly interact with an LLM.
- Servers can specify parameters like preferred models, system/task prompts, temperature, and max tokens.
- Clients retain control over LLM interactions (privacy, cost, malicious calls).
- Sampling enables richer server-side logic and intelligence, especially for servers the client may not be familiar with.
- **Composability:** Any application, API, or agent can act as both an MCP client and an MCP server.
- This allows for chaining of interactions, where a client (e.g., a user interacting with an agent) can trigger a server (the orchestrator agent), which in turn acts as a client to invoke other specialized servers/agents (e.g., research, coding).
- Enables the creation of complex, multi-layered LLM systems where each component specializes in a task.

**11. MCP Roadmap:**

- **Remote Servers and Auth:Key Development:** Implementing OAuth 2.0 support within the MCP protocol.
- **Functionality:** Enables remotely hosted MCP servers accessible via URLs (using SSC instead of standard IO).
- **Authentication Flow:** The server orchestrates the OAuth handshake with the target service (e.g., Slack), obtaining user authorization through a browser-based flow. The server holds the OAuth token, and the client receives a session token for subsequent interactions.
- **Benefits:** Reduces development friction, makes servers discoverable like websites, and allows agents/LLMs to reside on different systems than the server.
- **MCP Registry API:Motivation:** Addressing the current fragmentation and lack of centralized discovery for MCP servers.
- **Description:** A unified, hosted metadata service for MCP servers, owned by the MCP team but developed openly.
- **Functionality:** Provides a layer above existing package systems (NPM, PyPI, etc.) for discovering and pulling in servers.
- **Key Benefits:**Standardizes discovery and protocol information (standard IO vs. SSC, URL presence).
- Provides information about the server builder (identity, trust).
- Enables verification of official servers (e.g., by the company owning the underlying service).
- Simplifies publishing and finding MCP servers.
- **Versioning:** Will support versioning of the entire MCP ecosystem, tracking changes in APIs, tools, and resources.
- **DevEx and Documentation:** Will serve as a central hub for documentation on building clients and servers, implementing auth, and best practices.

**12. Key Q&A Insights:**

- **Tools vs. Resources:** Resources are application-controlled, allowing the client to decide when to put them in context, while tools are typically model-controlled. This separation provides flexibility for richer application-server interactions beyond just model context.
- **Vector Databases as Tools:** Exposing a vector database as a tool is suitable when the LLM needs to decide if and when to query it. If it's always needed, direct injection might be simpler.
- **MCP and Agent Frameworks (Recap):** They are complementary. MCP provides the connectivity, while frameworks manage the agentic loop and knowledge.
- **Resources and Prompts - More Than Static:** They can be dynamic, interpolated with user or application context. Resources also support notifications, allowing servers to inform clients of updates.
- **Agent Systems for Proprietary Data:** MCP's open nature allows running servers within VPCs or on local systems for accessing proprietary data.
- **Separation of Agent Logic:** Focus shifts to model selection, context management, orchestration, and the user interface when MCP handles context acquisition.
- **Number of Servers for an LLM:** Modern models can handle many tools (50-100+). Strategies for managing large numbers include tool search tools and hierarchical organization.
- **Automatic Server Generation:** Simpler servers (API wrappers) can be automatically generated, as seen in the Klein IDE.
- **Engagement with Service Owners:** Anthropic is actively engaging with owners of services and data, resulting in official MCP server integrations.
- **Server Versioning:** Currently relies on package versioning (npm, pip). Best practices for handling server changes are still evolving. A registry will help with this.
- **Distribution and Extension System:** The upcoming registry will serve as the primary distribution and extension mechanism.
- **Security and Registry:** The registry should support official integrations, verification processes, and community feedback to enhance security. The server itself controls access to the underlying application through authentication.
- **Long Tail of Servers:** The registry should accommodate local, unverified, and verified servers.
- **Distinguishing API Wrappers from Complex Servers:** The registry should allow specifying and filtering servers based on their complexity and functionality beyond simple API wrapping.
- **Client Control over Servers:** While the model controls tool invocation, prompt engineering and potential future "tool annotations" can offer clients some influence.
- **MCP DevEx Tools:** Tools like the "inspector" in the Anthropic repository aid in debugging and understanding server interactions. Best practices for debugging are still developing.
- **Governance and Security:** The server builder is primarily responsible for controlling client access through authentication and authorization mechanisms. OAuth 2.0 support is a key step in this direction.

**Conclusion:**

Anthropic's Multi-Context Protocol represents a significant step towards standardizing how AI applications and agents interact with external data sources and tools. By addressing the fragmentation prevalent in the pre-MCP landscape, the protocol offers substantial value to developers, tool providers, end users, and enterprises. The upcoming roadmap, including remote server support with OAuth and a centralized MCP registry, promises to further accelerate the adoption and utility of MCP, particularly in the burgeoning field of AI agents. While challenges remain in areas like server versioning, debugging best practices, and comprehensive security measures, the foundation laid by MCP and the planned developments indicate a strong trajectory for its role as a foundational protocol for intelligent, context-aware AI systems.