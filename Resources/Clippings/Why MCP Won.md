---
title: Why MCP Won
source: https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true
author:
  - Swyx
published: 
created: 2025-03-15
description: Learnings from Anthropic's extraordinarily successful Launch and Workshop
tags:
  - clippings
---
### Learnings from Anthropic's extraordinarily successful Launch and Workshop

Dear AI Engineers,

**I’m sorry for all the MCP filling your timeline right now.**

The **Model Context Protocol**[launched in November 2024](https://buttondown.com/ainews/archive/ainews-anthropic-launches-the-model-context/) and it was [decently well received](https://x.com/alexalbert__/status/1861079762506252723), but the [initial flurry of excitement](https://x.com/alexalbert__/status/1861464485011300839?s=46&t=6FDPaNxZcbSsELal6Sv7Ug) (with everyone from [Copilot](https://x.com/mariorod1/status/1861088610650337448) to [Cognition](https://x.com/ScottWu46/status/1861130277675794700) to [Cursor](https://x.com/ericzakariasson/status/1885756582367035892) adding support) died down[1](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-1-158760081) right until [the Feb 26-27 AI Engineer Summit](https://www.latent.space/p/2025-summit-online), where a chance conversation with [Barry Zhang](https://x.com/search?q=%40aidotengineer%20%40barry_zyj&src=typed_query&f=top) led to us booking [Mahesh Murag](https://x.com/aiDotEngineer/status/1895882186756407680) (who wrote the MCP servers). I simply thought it’d be a nice change from Anthropic’s [2023](https://www.youtube.com/watch?v=6d60zVdcCV4) and [2024](https://www.youtube.com/watch?v=hkhDdcM5V94&t=2s) prompting workshops, but then this happened:

<iframe src="https://www.youtube-nocookie.com/embed/kQmXtrmQ5Zg?rel=0&amp;autoplay=0&amp;showinfo=0&amp;enablejsapi=0" frameborder="0" allow="autoplay; fullscreen" allowfullscreen="true" width="728" height="409"></iframe>

Normally workshops are great for live attendees but it’s rare for an online audience to keep the attention span for a full 2 hours. But then [livetweets of the workshop](https://x.com/opentools_/status/1893696402477453819) started going viral, because for the first time the community was getting announcements of the highly anticipated official registry, and also comprehensive deep dives into every part of the protocol spec like this:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe07df610-fa0b-4e18-bca5-6ade934cb64a_2274x1264.png)

We then bumped up the editing[2](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-2-158760081) process to release the workshop video, and, with almost [300k combined views](https://x.com/aiDotEngineer/status/1895882186756407680) in the past week, this happened:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fc325ceca-4bdf-44cf-b727-978bb49a89e1_1106x1716.png)

everybody complaining about too much MCP

One “reach” goal I have with Latent Space is to try to offer editorial opinions slightly ahead of the consensus. In November we said [GPT Wrappers Are Good, Actually](https://x.com/latentspacepod/status/1857793791567999007), and now [a16z is excited about them](https://x.com/andrewchen/status/1886858755633221978). In December we told $200/month Pro haters that [You’re all wrong, $2k/month “ChatGPT Max” is coming](https://www.latent.space/p/chatgpt-max) and now we have confirmation that [$2-20k/month agents are planned](https://x.com/ns123abc/status/1897311174737453199). But I have to admit MCP’s popularity caught even me offguard, mostly because I have seen many attempted [XKCD 927](https://xkcd.com/927/)’s come and go, and MCP was initially presented as a way to write local, privacy-respecting integrations for Claude Desktop, which I’m willing to bet only a small % of the AI Engineer population have even downloaded (as opposed to say [ChatGPT Desktop](https://www.youtube.com/watch?v=yJHw33cVeHo) and even [Raycast AI](https://www.youtube.com/watch?v=hoEL6ddVcC0)).

Even though we made the workshop happen, I still feel that I underestimated MCP.

To paraphrase Ben Thompson, the #1 feature of any network is the people already on it. Accordingly, **the power of any new protocol derives from its adoption (aka ecosystem)**, and it’s fair to say that MCP has captured enough critical mass and momentum right now that it is already the presumptive winner of the 2023-2025 “agent open standard” wars. At current pace, **MCP will overtake OpenAPI in July**:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F3c23222d-bb03-445b-9806-483eb06c3b75_2554x1640.png)

[See for yourself](https://www.star-history.com/#modelcontextprotocol/servers&crewAIInc/crewAI&langchain-ai/langgraph&pydantic/pydantic-ai&openai/swarm&Div99/agent-protocol&meta-llama/llama-stack&Timeline). Add Langchain if you’re curious but it skews the chart too much

Widely accepted standards, like Kubernetes and React and HTTP, accommodate the vast diversity of data emitters and consumers by [converting exploding MxN problems into tractable M+N ecosystem solutions](https://x.com/swyx/status/1629553997416910849), and are therefore immensely valuable IF they can get critical mass. Indeed even OpenAI had the previous AI standard[3](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-3-158760081) with even [Gemini](https://ai.google.dev/gemini-api/docs/openai), [Anthropic](https://docs.anthropic.com/en/api/openai-sdk) and [Ollama](https://ollama.com/blog/openai-compatibility) advertising OpenAI SDK compatibility.

I’m not arrogant enough to think the AIE Summit workshop *caused* this acceleration; we merely poured fuel on a fire we already saw spreading. But as a [student of developer tooling startups](https://dx.tips/), many of which try and fail to create momentum for open standards[4](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-4-158760081), I feel I cannot miss the opportunity to study this closer while it is still fresh, so as to serve as a handbook for future standard creation. Besides, I get asked my MCP thoughts 2x a day so [it’s time](https://x.com/swyx/status/1351197649727352836) to write it down.

## Why MCP Won (in short)

*aka “won” status as de facto standard, over not-exactly-equivalent-but-alternative approaches like OpenAPI and LangChain/LangGraph. In rough descending order.*

1. **MCP is “AI-Native” version of old idea**
2. **MCP is an “open standard” with a big backer**
3. **Anthropic has the best developer AI brand**
4. **MCP based off LSP, an existing successful protocol**
5. **MCP dogfooded with complete set of 1st party client, servers, tooling, SDKs**
6. **MCP started with minimal base, but with frequent roadmap updates**
7. **Non-Factors:** Things that we think surprisingly did *not* contribute to MCP’s success

- Lining up launch partners like Zed, SourceGraph Cody, and Replit
- Launching with great documentation

I will now elaborate with some screengrabs.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F34123523-7082-4895-b8e4-b26077683c61_1610x868.png)

oh [look](https://x.com/mattpocockuk/status/1897742389592440970/photo/2), another [god box](https://x.com/swyx/status/1629553997416910849): "We can solve any problem by introducing an extra level of indirection."

## MCP is “AI-Native” version of old idea

A lot of the “old school developer” types, myself included, would initially be confused by MCP’s success because, at a technical level, MCP is mostly capable of the same[5](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-5-158760081) kinds of capabilities enabled by existing standards like OpenAPI / OData / GraphQL / SOAP / etc. *So the implicit assumption is that the older, Lindy, standard should win.*

However, to dismiss ideas on a technical basis is to neglect the sociological context that human engineers operate in. In other words, saying that “the old thing does the same, you should prefer the old thing” falls prey to the same [Lavers’ Law](https://css-tricks.com/its-always-year-zero/) fallacy of fashion every developer comes to, the same kind of attitude that leads one to dismiss [the Rise of the AI Engineer](https://www.latent.space/p/ai-engineer) because you assume it sufficiently closely maps on to an existing job. To paraphrase [Eugene Wei’s Status as a Service](https://www.eugenewei.com/blog/2019/2/19/status-as-a-service), each new generation of developer actively looks for new ground to make their mark, basically because you already made your mark in yours.

The [reflexive](https://www.swyx.io/mimicry-reflexivity) nature of the value of protocols - remember, they only have value because they can get adoption - mean that there is very little *ex ante* value to any of these ideas. MCP is valuable because the AI influencers deem it so, and therefore it *does become valuable*.

It’s also valuable that it is a revision of an **old idea**, meaning that it actually does fill a need we know we have, and not a made up need that is unproven.

However it is **ALSO** too dismissive to say that MCP is exactly equivalent to OpenAPI and it is mere cynical faddish cycles that drive its success. This is why I choose to describe this success factor as “**AI Native**” - in this case, MCP was born from lessons felt in [Claude Sonnet’s #1 SWE-Bench result](https://www.latent.space/p/claude-sonnet) and articulated in [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents), primarily this slide:

![Image](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffc16bfa4-418c-4e2e-a614-b76a1e793682_2034x1110.jpeg)

An “AI Native” standard that reifies patterns already independently reoccurring in every single Agent will always be more ergonomic to use and build tools for than an agnostic standard that was designed without those biases.

**Hence MCP wins over OpenAPI.**

Second, going back to this slide, focus on the differences articulated between **Tools** (Model-controlled), **Resources** (Application-controlled), and **Prompts** (User-controlled).

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe07df610-fa0b-4e18-bca5-6ade934cb64a_2274x1264.png)

MCP’s “AI Native”ness being born *after* the initial wave of LLM frameworks, means that it has enough breathing room to resist doing the “obvious” thing of starting from LLM interoperability (now solved problems and likely owned by [clients](https://modelcontextprotocol.io/clients) and [gateways](https://www.latent.space/p/gateway)), and only focus on the annoying unsolved problems of putting dynamic context access at the center of its universe (very literally saying the motivation of MCP is that “[Models are only as good as the context provided to them](https://youtu.be/kQmXtrmQ5Zg?si=ziw3VJ3Rb2V1Tevp&t=103)”).

**Hence MCP wins over [LangChain](http://langchain/) et al.**

## MCP is an “open standard” with a big backer

This one is perhaps the most depressing for idealists who want the best idea to win: a standard from a Big Lab is very simply more likely to succeed than a standard from anyone else. Even ones with tens of thousands of Github stars and tens of millions of dollars in top tier VC funding. There is nothing fair about this; if the financial future of your startup incentivizes you at all to lock me in to your standard, I’m not adopting it. If the standard backer seems too big to really care about locking you in to the standard, then I will adopt it[6](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-6-158760081).

**Hence MCP wins over [Composio](https://github.com/ComposioHQ/composio) et al.**

Any "open standard”[7](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-7-158760081) should have a spec, and [MCP has a VERY good spec](https://spec.modelcontextprotocol.io/specification/2024-11-05/). This spec alone defeats a lot of contenders, who do not provide such detailed specs.

**Hence MCP wins over many open source frameworks,** and arguably even OpenAI function calling, whose [docs](https://platform.openai.com/docs/guides/function-calling#defining-functions) fall just short of a properly exhaustive spec.

## Anthropic has the best developer AI brand

Perhaps as important as the fact that a big backer is behind it, is *which* big backer. **If you’re going to build a developer standard, it helps to be beloved by developers.** Sonnet has been king here for almost 9 months.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F44e05941-159b-499e-92b9-0e9b2808e5e9_2138x1538.png)

https://aider.chat/docs/leaderboards/by-release-date.html

A bit of a more subtle point that might be missed by newer folks - Anthropic has always explicitly emphasized supporting more tools than OpenAI has - we don’t really have benchmarks/ablations for large tool counts, so we don’t know the differential capabilities between model labs, but intuitively **MCP enables far more average tools in a single call** than is “normal” in tools built without MCP (merely because of ease of inclusion, not due to any inherent technical limitation). So models that can handle higher tool counts better will do better.

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F66510105-27cd-4c8f-a906-ba6b33c0d0a6_998x1630.png)

https://x.com/swyx/status/1775993946935906645

**Hence MCP wins over equivalent developer standards by, say, [Cisco](https://x.com/llama_index/status/1897701302060433736?s=61).**

## MCP based off LSP, an existing successful protocol

The other part of the ““open standard” with a big backer” statement requires that the standard not have any fatal flaws. Instead of inventing a standard on the fly, from scratch, and thus risking relitigating all the prior mistakes of the past, the Anthropic team smartly adapted Microsoft’s very successful [Language Server Protocol](https://microsoft.github.io/language-server-protocol/).

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb3098b44-18ae-4f70-8420-055ee1bbf45f_976x696.png)

https://x.com/dsp\_/status/1897821339332882617

And again, from the workshop, a keen awareness of how MCP compares to LSP:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F287e9c38-db9a-4abb-9a88-bc3e3e590355_2252x1214.png)

The best way to understand this point is to look at any other open source AI-native competitor that tried to get mass adoption, and then try to think about how easy it might be for you to [add them to Cursor/Windsurf as easily as an MCP](https://supabase.com/docs/guides/getting-started/mcp). The basic insight is fungibility between clients and servers: Often these competitors are designed to be consumed in one way — as open source packages in another codebase — rather than emitting messages that can be consumed by anyone[8](https://www.latent.space/p/why-mcp-won?publication_id=1084089&post_id=158760081&action=share&triggerShare=true&isFreemail=true&r=5uuks&triedRedirect=true#footnote-8-158760081). Another good choice was sticking to [JSON RPC](https://modelcontextprotocol.io/docs/concepts/transports) for messages - again inheirited from LSP.

**Hence MCP wins over other standard formats that are more “unproven”**.

## MCP dogfooded with complete set of 1st party client, servers, tooling, SDKs

MCP launched with:

- **Client**: [Claude Desktop](https://x.com/alexalbert__/status/1861079874385203522)
- **Servers**: [19 reference implementations](https://modelcontextprotocol.io/examples), including interesting ones for [memory](https://x.com/swyx/status/1861441838114337233), [filesystem (Magic!)](https://www.reddit.com/r/ClaudeAI/comments/1h4yvep/mcp_filesystem_is_magic/) and [sequential thinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)
- **Tooling**: [MCP Inspector, Claude Desktop DevTools](https://modelcontextprotocol.io/docs/tools/debugging)
- **SDKs**: [Python](https://github.com/modelcontextprotocol/python-sdk) and [TS SDKs](https://github.com/modelcontextprotocol/typescript-sdk), but also a [llms-full.txt](https://modelcontextprotocol.io/tutorials/building-mcp-with-llms) documentation

Since then, the more recent [Claude Code](https://ai-claude.net/code/) also sneaked in a ***SECOND***official MCP client from Anthropic, this time in CLI form:

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F68dff7d2-6882-4b50-8fc3-fdede0e46a25_942x608.png)

https://x.com/willccbb/status/1898858751685255398

This all came from real life use cases from Anthropic developers.

**Hence MCP wins over less dogfooded attempts from other BigCos like Meta’s [llama-stack](https://github.com/meta-llama/llama-stack).**

## MCP started with a minimal base, but with frequent roadmap updates

One of the most important concepts in devtools is having a [minimal surface area](https://www.youtube.com/watch?v=4anAwXYqLG8):

![](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F58a591e2-9c39-4d2b-bb76-cbc46ab41cb1_2104x1478.png)

[youtube](https://www.youtube.com/watch?v=4anAwXYqLG8)

Reasonable people can disagree on how minimal MCP is