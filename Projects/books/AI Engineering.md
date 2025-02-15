---
title: "AI Engineering"
author: "Chip Huyen"

---
# Chapter 1: Introduction to Building AI Applications with Foundation Models

## Why AI Matters

People/Teams are using AI to:
- Increase productivity
- Create economic value
- Improve quality of life

**Model as a Service** provided by companies like OpenAI, Google, and Anthropic has made AI a **commodity**, drastically reducing entry barriers.

### Challenges in Building Foundation Models

- Expensive: Requires vast amounts of data, compute resources, and specialized talent.
- AI existed before LLMs: Traditional ML models powered applications like product recommendations and fraud detection.

> **As AI Engineers, we need to understand what AI is good at and what it struggles with.**

---

## Rise of AI Engineering

### Evolution of Language Models

- ML → Language Models (LM) → Large Language Models (LLM)
- **First language models** emerged in the 1950s.

#### How did LM evolve into LLM?

- **Self-supervision** enabled models to scale massively.
- LMs **encode statistical information** about language(s), allowing them to predict word likelihoods.

**Example:**

- Context: "My favorite color is ____"
- An English LM would predict "blue" over "car."

### Statistical Nature of Language Models

- **1905:** Sherlock Holmes’ _[The Adventure of the Dancing Men](https://medium.com/ml-hobbyist/what-sherlock-holmes-can-teach-us-about-large-language-models-5a84ea5344a4#bypass)_ used statistical language patterns.
- **1951:** _[Prediction and Entropy of Printed English](https://www.princeton.edu/~wbialek/rome/refs/shannon_51.pdf)_ paper applied statistical methods to decode messages during WWII.

---

## Tokens: The Building Blocks of LMs

- **A token** can be a character, a word, or a word segment (e.g., “-tion”).
- Tokenization is the process of breaking text into tokens.
- OpenAI tokenization: ~100 tokens ≈ 75 words (roughly ¾ of a word).

**Why use tokens instead of text?**

- Models work with a **finite vocabulary** of tokens (which is decided by model developers)
- Tokens allow efficient word construction: e.g., _cooking_ = _cook_ + _ing_.
- Helps with unknown words: _chagpting_ → _chatgpt_ + _ing_.

![[2025-02-14 at 08.57.48@2x.png]]
- The token ids (numerical identifiers) for the above texts - `[15390, 7524, 1078, 1495, 6602, 2860, 5882, 20255, 5861]`
### OpenAI’s Tokenization Resources

- [Tokenizer Tool](https://platform.openai.com/tokenizer)
- [Vocabulary File](https://openaipublic.blob.core.windows.net/encodings/o200k_base.tiktoken)

---

## Types of Language Models

### 1. Masked Language Models (MLM)

- **Trained to predict missing tokens** using context before and after.
- Example: [BERT](https://arxiv.org/pdf/1810.04805)
- **Use Cases:** Sentiment analysis, text classification.

**Example:**

- "My favorite ____ is blue." → Model predicts "color."

### 2. Autoregressive Language Models (ARLM)

- **Trained to predict the next token** using preceding tokens.
- Can **generate** text sequentially.
- **Use Cases:** Text generation, conversation models.

**Example:**

- "My favorite color is ____" → Model predicts "blue."

---

## Self-Supervision: The Game-Changer

### Supervised Learning

- Requires **labeled** data.
- **Expensive** and slow to obtain (e.g., medical image labeling).

### Self-Supervised Learning

- **Removes the need for explicit labels.**
- LMs learn from massive text data without human annotation.
- Example: Predicting the next word in a sentence.

**Training Data Example:**

|Input (context)|Output (next token)|
|---|---|
|`<BOS>`|I|
|`<BOS>`, I|love|
|`<BOS>`, I, love|reading|

- **`<BOS>` (beginning of sequence)** and **`<EOS>` (end of sequence)** help the model structure responses.
- **Self-supervised training enabled scaling LMs into LLMs.**

---

## From Large Language Models to Foundation Models

- AI is not just about language; it must support multiple **modalities** (vision, audio, text, etc.).

### Foundation Models

- **General-purpose AI models** built upon for various tasks.
- Different data modalities:
    - **Text**: Translation, spam detection.
    - **Image**: Object detection, classification.
    - **Audio**: Speech recognition (STT), speech synthesis (TTS).

### Multimodal Models

- **Can process multiple types of data** (e.g., text + image).
- **Generative multimodal models** = Large Multimodal Models (LMMs).
- **Example:** OpenAI’s [CLIP](https://openai.com/clip) used **self-supervision** to process **400M image-text pairs** without manual labeling.

---

## Fine-Tuning and Enhancing Model Responses

### Three Main Methods:

1. **Prompt Engineering:** Writing detailed instructions with examples.
2. **Retrieval-Augmented Generation (RAG):** Using external context to supplement prompts.
3. **Fine-Tuning:** Training the model on domain-specific data for better performance.

**Foundation Models Lower AI Development Costs & Time-to-Market.**

---

## The Rise of AI Engineering

> **AI Engineering = Building applications on top of foundation models.**

**Traditional ML vs. AI Engineering:**

- ML: Developing new models.
- AI Engineering: Leveraging existing models.

### Factors Driving AI Engineering Growth
1. **General-purpose AI capabilities**
    - AI is **not just improving tasks** but enabling **new applications**.
2. **Increased AI Investments**
    - ChatGPT’s success led to **massive AI investments**.
    - Companies mentioning AI saw **higher stock gains**.
3. **Lower Entry Barriers**
    - **Model as a Service (API-based)** makes AI accessible without complex infrastructure.

---

### Foundation Model Use Cases
- The potential use case of foundation models are vast and continuously evolving.
- AI use cases are categorized differently by various organizations (e.g., AWS: customer experience, employee productivity, process optimization; O’Reilly: programming, data analysis, customer support, etc.).
- [AI exposure](https://arxiv.org/abs/2303.10130) varies across occupations, with **creative and analytical fields being highly affected**.
	- A task/field is exposed if AI and AI-powered software can reduce the time needed to complete this task by at least 50%
	- ![[2025-02-15 at 13.10.03@2x.png]]

## Enterprise & Consumer Applications

> **Note:** These insights are AI-generated summaries. For full context, read the book.

### AI Applications Across Categories

| **Category**                | **Consumer Examples**             | **Enterprise Examples**             |
|-----------------------------|-----------------------------------|-------------------------------------|
| **Coding**                  | Code generation, debugging        | Developer copilots, automation      |
| **Image/Video**             | Profile pics, editing apps        | Ad & marketing content              |
| **Writing**                 | Emails, blogs, social media       | Copywriting, SEO, reports           |
| **Education**               | AI tutors, essay grading          | Employee training, onboarding       |
| **Conversational Bots**     | AI companions, chatbots           | Customer support, product copilots  |
| **Information Aggregation** | Summarization, Chat with docs     | Market research, reporting          |
| **Data Organization**       | Image/document search             | Knowledge management, processing    |
| **Workflow Automation**     | Travel & event planning           | Lead generation, data extraction    |

### Key Takeaways

- **AI applications overlap** (e.g., chatbots also summarize info).
- **Enterprise AI adoption is faster for internal apps** due to lower risk and AI expertise development.

### AI’s Impact on Coding

- **GitHub Copilot**: First major AI coding tool, reaching [$100M ARR](https://www.theinformation.com/briefings/microsoft-github-copilot-revenue-100-million-ARR-ai) within 2 years.
- **Specialized AI coding tools** exist for:
  - Extracting structured data → [AgentGPT](https://github.com/reworkd/AgentGPT)
  - Converting English to code → [DB-GPT](https://github.com/eosphoros-ai/DB-GPT), [SQL Chat](https://github.com/sqlchat/sqlchat)
  - Generating UI from screenshots → [screenshot-to-code](https://github.com/abi/screenshot-to-code)
  - Translating code between languages → [GPT-Migrate](https://github.com/joshpxyne/gpt-migrate)
  - Writing documentation → [Autodoc](https://github.com/context-labs/autodoc)
  - Creating tests → [PentestGPT](https://github.com/GreyDGL/PentestGPT)
  - Generating commit messages → [AI Commits](https://github.com/Nutlope/aicommits)

### AI’s Productivity Boost

- **2x faster documentation writing**.
- **25-50% more productive** in code generation & refactoring.
- **Disrupts outsourcing** by automating simple coding tasks.

---

## Image & Video Production

- AI excels in **creative tasks** due to its probabilistic nature.
- Major AI startups in creative fields:
  - **Midjourney** (image generation) → [$200M ARR in 1.5 years (2023)](https://midjourney.com/)
  - **Adobe Firefly** (photo editing)
  - **Runway, Pika Labs, Sora** (video generation)
- **Perception shift:** AI-generated profile pics went from being banned (2019) to mainstream (2023).

### AI in Advertising & Marketing

- AI **generates promotional content** directly.
- Helps with **brainstorming & content iteration**.
- **A/B testing**: Generates multiple ad variants.
- **Adaptive ads**: Adjusts visuals seasonally/geographically (e.g., changing leaves for fall).

## Writing

- AI enhances writing via **autocorrection & autocomplete**.
- **SEO-friendly content** (trained on web data).
- **Interactive AI books** (e.g., children's books adapt to words they struggle with).
- **Content farming issues**:
  - AI-generated books flood Amazon.
  - Junk websites exploit AI for ad revenue.

## Education

- **AI-powered homework assistants** – Initially banned, now accepted.
- **Personalized learning** – Adapts to visual, audio, or coding styles.
- **Language learning** – Used by Duolingo.
- **AI-generated & evaluated content** – Quizzes, essays, feedback.
- **AI tutors rising** – Khan Academy and similar platforms.
- **Disrupts traditional education** – Chegg’s stock crashed due to AI competition.
- **Speeds up learning** – Helps students outpace AI itself.

## Conversational Bots

- **AI companions are growing** – Digital relationships becoming common.
- **Bots simulate societies** – Used for research in social dynamics.
- **Customer support AI** – Reduces costs, improves response times.
- **AI copilots simplify complex tasks** – Helps with taxes, insurance, policies.
- **Revolutionizing NPCs in gaming** – Smarter, dynamic characters.

## Information Aggregation

- **Tackles information overload** – Summarizes emails, Slack, news.
- **74% of GenAI users use it for summarization** (Salesforce 2023).
- **"Talk-to-your-docs" feature** – Extracts contract/paper insights via chat.
- **Enterprise adoption** – AI reduces middle-management burden.
- **Instacart’s "Fast Breakdown" prompt** – Summarizes meetings into action items.
- **Enhances competitive analysis** – Surfaces key trends & insights.

---

## Data Organization

- **Data production is increasing** – More images, logs, reports.
- **AI organizes & searches unstructured data** – Generates metadata & improves search.
- **AI-powered search is mainstream** – Google Photos, AI-generated search results.
- **AI excels in data analysis** – Creates visualizations, detects trends, predicts outcomes.
- **Extracts structured data** – Reads receipts, credit cards, emails.
- **Enterprises use AI for knowledge management** – Extracts insights from contracts & reports.

## Workflow Automation
- **End-user Automation:** Automates everyday tasks like booking restaurants, planning trips, and filling forms.
- **Enterprise Automation:** Streamlines repetitive tasks (lead management, invoicing, data entry) and leverages AI for data synthesis.
- **AI Agents:** Integrates external tools to significantly boost productivity and economic value.
- **Selective Development:** Not every potential AI application should be built.

---

## Planning AI Application
- It is easier to build cool demo with foundation models. It's very hard to create a profitable product.

- **Use Case Evaluation:**
 1. If you don't do this, competitors with AI can make you obsolete. 
 2. If you don't do this, you'll miss opportunities to boost profits and productivity.
	 - AI can make user acquision cheaper
	 - Increase user retention
	 - Sales lead generation
 3. You're unsure where AI will fit into your business yet, but you don't want to be left behind.
	- While a company should not chase every hype train, many have failed by waiting too long to take the leap (Nokia, Kodak, etc)
	- Investing resources into understanding how it works -- not a bad idea if you can afford it.
If AI poses an existential thread to your business, you need to do AI in-house instead of outsourcing it to a competitor.

If you're using AI to boost profits and productivity, you might have plenty of buy options that can save you time and money while giving you better performance

**The role if AI and humans in the application:**
1. Critical or complementary
	- If app can work without work then it is complementary to app.
	- Eg: FaceID won't work without facial recognition but Gmail can work without smart compose
2. Reactive or proactive
	- Reactive feature shows its response in reaction to user's request or specific action, whereas proactive feature shows its response when their's an opportunity for it.
	- Reactive feature - need to happen fast
	- Proactive 
		- Precomputed and shown opportunistically, so latency is less important
		- Higher quality bar -- since low quality can be intrusive or annoying to the user
3. Dynamic or static
	- Dynamic feature are updated continually with user feedback, whereas static features are updated periodically.
	- FaceID needs to be updated periodically with faces changes over time. However, object detection in Google Photos is updated only when Google Photos is upgraded
	- Dynamic feature: each user has their own model, continaully finetuned on their data or other mechanisms for personalization -- ChatGPT memory feature.
	- Static feature might have one model for each group of users.
		- Updated only when the shared model is updated.
