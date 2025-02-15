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
#### Masked language models - MLM
- It is trained to predict missing tokens anywhere in the sequence -- using context from **both before and after** the missing tokens. Essentially, trained to fill in the blank.
- Example model: BERT (Bidirectional Encoder Representations from Transformers)
- 

