---
title: "AI Engineering"
author: "Chip Huyen"

---
# Chapter 1. Introduction to Building AI Applications with Foundation Models
- People/Teams are using AI to:
	- Increase their productivity
	- Create economic value
	- Improve quality of life
- **Modal as service** which is done by few companies (OpenAI, Google, Anthropic, etc) made AI as a ==commodity== -- barrier for entry has decreased drastically.
- Building a foundation modal is damn expensive - requires data, compute resources and specialised talent
- Even before the LLM became prominent, AI was already powering lot of applications -- product recommendation, fraud detection, etc which were built using traditional ML models

> As AI Engineer, we need to understand **what AI is good and not yet good at**. 

## Rise of AI Engineering

### Language Model

- ML → Language Model → LLM
- First LM started emerging in 1950s. 

**How LM to LLM?**
They were able to grow to today's scale because of ==self-supervision==

**Language models**
- LM **encodes statistical information** about one (older models) or more language
- This information helps us to predict ==how likely a word is to appear in a given context==
- Example: 
	- Context: "My favorite color is ____"
	- LM that encodes English should predict "blue" more often than a "car"
- Statistical nature of languages was discovered centuries ago 
	- 1905 - [The Adventure of the Dancing Man](https://freedium.cfd/https://medium.com/ml-hobbyist/what-sherlock-holmes-can-teach-us-about-large-language-models-5a84ea5344a4) story - leveraging statistical information of English to decode sequence of mysteries stick figures 
		- https://josmfs.net/wordpress/wp-content/uploads/2021/12/Dancing-Men-211028.pdf
	- 1951 - [Prediction and Entropy of Printed English](https://www.princeton.edu/~wbialek/rome/refs/shannon_51.pdf) paper - statistics to decipher enemies' messages during WW2. It introduced many concepts like entropy which are used in LM today.
### Tokens
- Basic unit of language model is token
- ==A token can be a character, a word or a part of word (like -tion), depending on the model
- https://platform.openai.com/tokenizer 👇

![[2025-02-14 at 08.57.48@2x.png]]
- The token ids (numerical identifiers) for the above texts - `[15390, 7524, 1078, 1495, 6602, 2860, 5882, 20255, 5861]`
- The process of breaking down original text into tokens is called `tokenization`
- Thumb rule - roughly ¾ of a word (so 100 tokens ~= 75 words) for OpenAI models
- Similarly for other model - https://tiktokenizer.vercel.app

**Why LM uses token instead of text?**
- The set of all the tokens that a model can work with is the model's *vocabulary*
- We can use small number of tokens to construct a large number of ==distinct words== – similar to how few letters in alphabet to construct many words
- OpenAI model vocabulary
	- https://github.com/openai/tiktoken/blob/main/tiktoken/model.py
	- https://openaipublic.blob.core.windows.net/encodings/o200k_base.tiktoken (text is encoded into base64)
- Tokenization method and vocabulary size are decided by model developers
- TLDR
	- Compared to characters, tokens allow the model to break words into meaningful components. cook+ing = cooking. With both word carrying some meaning of original word.
	- Fewer unique tokens === reduced model's vocabulary size
	- Process unknown words. chagpting = chatgpt + ing

### Types of Language Models
1. Masked language models
2. Autoregressive language models
#### Masked language model - MLM
- It is trained to predict missing tokens anywhere in the sequence -- using context from ==both before and after== the missing tokens. Essentially, trained to fill in the blank.
- Example model: [BERT](https://arxiv.org/pdf/1810.04805) (Bidirectional Encoder Representations from Transformers)
- Use cases:
	- Non generative tasks like sentiment analysis and text classification
- Example:
	- My favourite ___ is blue. Model will predict "color"


#### Autoregressive language model
- It is trained to predict the next token in a sequence, using only the ==preceding tokens==
- It can continually generate one token after another.
- Use cases:
	- Text generation
- Example:
	- My favourite color is ___ Model will predict "blue"

![[Pasted image 20250215090148.png]]

---
- The output of language models are **open ended**
- It uses it's fixed, finite vocabulary to construct infinite possible outputs
- A model that can `generate open-ended output` → `generative` → `generative AI`
- LM are ==completion machine==: Give a text (prompt), it tries to complete the text
	- Completions are predictions, based on probabilities, and not guaranteed to be correct
	- Probabilistic nature: exciting and frustrating to use

#### Self-supervision 🙌
**What's special about LM that caused ChatGPT moment?**
TLDR: LM can be trained using  self-supervision

**Supervision:**
- Supervision refers to the process of training ML algorithms using labeled data -- expensive, slow to obtain (bottleneck)
	1.	Label examples: Show the model what behavior you want it to learn.
	2.	Train the model: Use labeled examples to teach the model.
	3.	Apply to new data: Use the trained model on new, unseen data.

- 2010s AI models were built on supervision like [AlexNet](https://proceedings.neurips.cc/paper_files/paper/2012/file/c399862d3b9d6b76c8436e924a68c45b-Paper.pdf)
- AlexNet:
	- Started deep learning revolution
	- Trained on ImageNet
	- It classified each of the image into one of the 1,000 categories like "car", "cat", "balloon", etc
- Supervision drawbacks: expensive and time-consuming
- Labeling everyday objects: relatively cheap, no expert training needed. However, specialized labeling (e.g., CT Scan) requires expertise and is expensive

**Self-supervision:** 
- Self-supervision helps to overcome drawbacks of supervision.
- In self-supervision, instead of requiring explicit labels, the model can infer labels from the input data.
- Language modeling is self-supervised, because ==each input sequence provide both the labels (tokens to be predicted) and the context the model can use to predict these labels ==

Training samples for the sentence "I love reading books.":

| Input (context) | Output (next token) |
|-----------------|-------------------|
| `<BOS>`| I |
| `<BOS>`, I | love |
| `<BOS>`, I, love | reading |
| `<BOS>`, I, love, reading | books |
| `<BOS>`, I, love, reading, books | . |
| `<BOS>`, I, love, reading, books, . | `<EOS>` |

- `<BOS>` and `<EOS>` mark beginning and end of sequence.  Each marker is typically treated as __one special token__ by the model
- EOS is really important because it helps LMs know when to end their responses.

**From LM to LLM:**
- Self-supervised learning means LMs can learn from text sequences without requiring any labeling.
- Text sequences are everywhere in the internet -- blog posts, books, reddit comments and other pirated content (which is commonly used by most AI companies 😅)
- It is possible to construct a massive training data, allowing language models to scale up to become LLMs

**LLM:**
- Hardly a scientific term -- subjective
- What is LLM today might be tiny tomorrow.
- Model's size is typically measured by it's **number of parameters**
- ==**Parameters** -- A variable within a ML model that is updated though the training process.==
- In general, more parameters === greater it's capacity to learn desired behaviours.

#### From Large Language Models to Foundation Models
- Perceiving the world is not just about language, but also involves other senses like vision, hearing, touch, and more.
- To be useful in the real world, AI needs to support multiple modalities. Recent Language Models (LM) are starting to support this.
* Foundation models:
	+ Can be built upon for different needs
	+ Breakthrough from traditional AI research structure
		+ Divided by data modalities:
			- **NLP**: Text only
			- **Computer Vision**: Vision only
			* Model Examples:
				+ **Text only**:
					- Translation
					- Spam detection
				+ **Image only**:
					- Object detection
					- Image classification
				+ **Audio only**:
					- Speech recognition (STT) - speech-to-text
					- Speech synthesis (TTS) - text-to-speech
#### Multimodal Model
- A model that can work with more than one modality is called **multimodal model**. 
- A generative multimodal modal -- Large multimodal model (LMM)
- Multimodal models generate tokens based on both text and image (or other supported modalities), unlike language models which only use text.
	- ![[Pasted image 20250215111244.png]]
- Similar to LM, LMM also need data to scale up -- self supervision works for multimodal models as well.
- OpenAI used varient of self-supervision called natural language supervision to train [CLIP](https://openai.com/index/clip/)
	- Instead of manually labeling image and text pair, they found it on the internet.
	- Using it the were able to generate a dataset of 400 million (image, text) pairs without manual labeling cost.
	- CLIP become the first model that could handle multiple image classification tasks without requiring additional training.
	- CLIP is embedding model (not generative) -- capture meanings of the original data.
	- Multimodal embedding are backbone of generative multimodal models like Flamingo, LLaVA, etc
- Foundation model: transition from task-specific models to general purpose models.
	- Previously, models were generated for specific task.
	- You can tweak general-purpose model to maximize its performance on specific task (generating product description with brand's style)

#### Tuning model's response
- Prompt Engineering: Detailed instructions with examples of the desirable outcome
- RAG: Using external context to supplement the instructions
- Finetune: Further train the model on a dataset of high quality dataset
- FM make it cheaper to develop AI applications and ==reduce time to market==

### From FM to AI Engineering
> AI Engineering refers to process of ==building applications on top of foundation models==
- Traditional ML - developing ML models
- AI Engineering - leveraging existing ones

Powerful foundation models leads these factors that lead to rapid growth of AI engineering as a discipline
1. General purpose AI capabilities
	- FM models are powerful because they can do more tasks, not just existing tasks better.
		- They make previously impossible tasks possible.
		- They enable apps that were not thought of to emerge.
		- They might even make currently impossible applications possible tomorrow.
2. Increased AI investments
	- Success of ChatGPT led to sharp increase in investments in AI.
	- As AI applications become cheaper to build and faster to go to market. ROI for AI become more attractive.
	- AI is mentioned as competitive advantage
	- Companies that mentioned AI in earning calls saw stock price increase more than those that didn't (avg 4.6%, compared to 2.4%)
3. Low barrier to entry to build AI applications
	- Model as service approach -- exposes model via API that receive user queries and return model outputs.
	- Without these APIs, using AI model require infra to host and serve this model -- which is way too expensive
	- Work with the model with English. No special language is required.

### Foundation Model Use Cases
- The potential use case of foundation models are vast and continuously evolving.
- AI use cases are categorized differently by various organizations (e.g., AWS: customer experience, employee productivity, process optimization; O’Reilly: programming, data analysis, customer support, etc.).
- [AI exposure](https://arxiv.org/abs/2303.10130) varies across occupations, with **creative and analytical fields being highly affected**.
	- A task/field is exposed if AI and AI-powered software can reduce the time needed to complete this task by at least 50%
	- ![[2025-02-15 at 13.10.03@2x.png]]

#### Enterprise & Consumer Applications

> Note: I was using AI to summarize key insights. Read the book to get full context about it.

| **Category**           | **Consumer Examples**          | **Enterprise Examples**        |  
|------------------------|--------------------------------|--------------------------------|  
| **Coding**            | Coding           | Coding    |  
| **Image/Video**      | Profile pics, editing apps    | Ad & marketing content       |  
| **Writing**          | Emails, blogs, social media  | Copywriting, SEO, reports    |  
| **Education**        | AI tutors, essay grading      | Employee upskill training, onboarding |  
| **Conversational Bots** | AI companions, chatbots    | Customer support, product copilots |  
| **Information Aggregation** | Summarization, Chat with docs | Summarization, Market research|  
| **Data Organization** | Image search, document search | Document processing & knowledge management |  
| **Workflow Automation** | Travel & event planning | Data extraction, Lead generation, automation tools |  

- **AI applications often overlap categories** (e.g., a chatbot can also summarize information).  
- **Enterprise AI adoption is faster for internal-facing apps** due to lower risk.  
	- Internal application helps develop their AI engineering expertise while minimizing the risk associated with it.
![[Pasted image 20250215153537.png]]

**Coding:**
- One of the earliest success of FM in production is GitHub Copilot -- code completion tool.
	- [$100M ARR](https://www.theinformation.com/briefings/microsoft-github-copilot-revenue-100-million-ARR-ai), 2 year after launch
- Other than general coding, there are tools that specialise in certain coding tasks

| **Task**                                       | **Example Tools**                                                                                                                                      |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Extract structured data                        | [AgentGPT](https://github.com/reworkd/AgentGPT)                                                                                                        |
| Convert English to code                        | [DB-GPT](https://github.com/eosphoros-ai/DB-GPT), [SQL Chat](https://github.com/sqlchat/sqlchat), [PandasAI](https://github.com/Sinaptik-AI/pandas-ai) |
| Generate website code from designs/screenshots | [screenshot-to-code](https://github.com/abi/screenshot-to-code), [draw-a-ui](https://github.com/sawyerhood/draw-a-ui)                                                                               |
| Translate between languages/frameworks         | [GPT-Migrate](https://github.com/joshpxyne/gpt-migrate), [AI Code Translator](https://github.com/mckaywrigley/ai-code-translator)                      |
| Write documentation                            | [Autodoc](https://github.com/context-labs/autodoc)                                                                                                     |
| Create tests                                   | [PentestGPT](https://github.com/GreyDGL/PentestGPT)                                                                                                    |
| Generate commit messages                       | [AI Commits](https://github.com/Nutlope/aicommits)                                                                                                     |

Note: Looks like majority of the repo is not active anymore.

- AI can help developers be twice productive for documentation
- 25-50% more productive for code generation and refactoring
- Regardless of whether AI will replace software engineers, It can certainly make  companies more productive. 
	- Disrupt the outsourcing industry, since outsourced tasks tend to be simpler ones outside of a company's code business.

**Image and Video Production:**
- AI is well-suited for creative tasks due to its probabilistic nature
- Successful AI startups in creative applications: 
	- **Midjourney** (image generation) 
	- **Adobe Firefly** (photo editing) 
	- **Runway, Pika Labs, Sora** (video generation) 
	- Midjourney reached **$200M ARR** in 1.5 years (late 2023).
- Perception shift:
	- **2019**: Facebook banned AI-generated profile pictures for safety reasons.
	- **2023**: Many social media apps offer AI profile picture tools.

**AI in Advertising and Marketing**
- For enterprise, ads and marketing have been quick to incorporate AI.
- AI can generate **promotional images and videos** directly.
- It can also assist with brainstorming & coming up with initial version for human iteration.
- A/B testing: Generating multiple ad variants
- AI can **adjust ads seasonally and geographically**. Eg:  Changing leaf colors in fall or Adding snow in winter.

**Writing:**
- AI has long been used to aid writing -- autocorrection and auto-completion feature in the smartphone is powered by AI
- For consumers, may use AI to communicate better.
- Unlike traditional books, AI generated books can be interactive.
	- A child's book identifies the words that a child has trouble with and generates stories centered around that word.
- It is kind of good with SEO -- maybe because it is trained on the internet dataset.
- - AI's ability to write can be abused.
	- Amazon is flooded with AI-generated books (AI slop)
	- Content farms -- junk website to make money from ads
**Education:**
- **Students depend on AI for homework** – Schools banned it but later allowed it.  
- **AI personalizes learning** – Adapts to different styles (audio, visual, coding).  
- **AI boosts language learning** – Duolingo uses it for lesson personalization.  
- **AI creates & evaluates content** – Quizzes, essays, debates, and feedback.  
- **AI-powered tutors are rising** – Khan Academy and similar platforms.  
- **Traditional education companies struggle** – Chegg’s stock crashed as AI replaced it.  
- **AI speeds up skill learning** – Helps students learn faster and surpass AI.  

**Conversational Bots:**
- **Conversational bots are highly versatile** – They assist with information, brainstorming, and even act as digital companions or therapists.  
- **AI companions are rapidly growing** – Digital relationships are becoming common, sparking concerns about their impact on dating.  
- **Bots can simulate societies** – Researchers use them to study social dynamics.  
- **Customer support bots are a major enterprise use case** – They reduce costs and improve response times.  🙌
- **AI copilots simplify complex tasks** – Helping users with taxes, insurance claims, and corporate policies.  
- **ChatGPT triggered a surge in conversational bots** – But voice assistants (Siri, Alexa) and 3D AI characters are also gaining traction.  
- **AI is revolutionizing NPCs in gaming** – Smarter, dynamic NPCs enhance experiences in games like The Sims and Skyrim.  

**Information Aggregation**
- **AI helps manage information overload** – Summarizes emails, Slack messages, and news.  
- **74% of generative AI users rely on it for summarization** – Salesforce’s 2023 research.  
- **AI enables "talk-to-your-docs"** – Retrieve info from contracts, papers, and disclosures conversationally.  
- **AI streamlines research and reporting** – Helps summarize and compare papers efficiently.  
- **Enterprises benefit from AI-driven info aggregation** – Reduces middle management burden.  
- **Instacart’s "Fast Breakdown" prompt is highly popular** – AI summarizes meetings, emails, and Slack discussions into action items.  
- **AI enhances competitive analysis** – Surfaces key customer insights and competitor trends.  
- **Information aggregation and organization go hand in hand** – AI structures and distills vast amounts of data.  

**Data Organization:**
- **Data production will keep increasing** – More photos, videos, logs, and contracts are generated every year.  
- **AI helps organize and search unstructured data** – Generates descriptions for images/videos and matches text queries with visuals.  
- **AI-powered search is already mainstream** – Google Photos and Image Search use AI to surface or even generate relevant images.  
- **AI excels at data analysis** – Can create visualizations, detect outliers, and make predictions (e.g., revenue forecasts).  
- **AI extracts structured data from unstructured sources** – Automates tasks like reading credit cards, receipts, and email footers.  
- **Enterprises benefit from AI-driven data organization** – Extracts insights from contracts, reports, and charts.  
