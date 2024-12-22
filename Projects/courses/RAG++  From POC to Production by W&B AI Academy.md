## Chapter 1

https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter01.ipynb


Metadata is extra information for that data point which can be used to group together similar data points, or filter out a few data points

## Chunking

Why Chunk? Chunking is important because most embedding models have token limits (e.g., 512 tokens). It also helps reduce the amount of text sent to the LLM, improving efficiency.

When the text is small-sized, embedding models tend to generate better vectors as they can capture more fine-grained details and nuances in the text, resulting in more accurate representations.

The optimal size depends on your data, expected queries, and model capabilities. Experiment with different sizes to find the best balance for your use case.

### Cleaning the data
Cleaning up data is crucial for most AI pipelines and applies to a RAG/Agentic pipeline as well. Usually, higher quality chunks provided to an LLM generates a higher quality response.

here, it is particularly important for several reasons:

- **Tokenization issues**: Special tokens can interfere with the model's tokenization process, leading to unexpected interpretations of the text.
- **Vocabulary pollution**: Unusual tokens can inflate the model's vocabulary, potentially diluting the importance of meaningful terms.
- **Semantic distortion**: Special characters or formatting tokens (e.g., HTML tags) can alter the semantic meaning of sentences if not properly handled.
- **Consistency**: Removing or standardizing special tokens ensures consistent representation across different data sources.
- **Model efficiency**: Cleaner data often leads to more efficient model training and inference, as the model doesn't need to process irrelevant tokens.

By cleaning the data, we ensure that our model focuses on the meaningful content rather than artifacts or noise in the text.

https://github.com/wandb/edu/blob/1132cf1a59dabcb8974d6f9767ee021ae065a823/rag-advanced/notebooks/scripts/preprocess.py


## Vectorizing the data

One of the key ingredient of most retrieval systems is to represent the given modality (text in our case) as a vector.  

This vector is a numerical representation representing the "content" of that modality (text).

Text vectorization (text to vector) can be done using various techniques like [bag-of-words](https://en.wikipedia.org/wiki/Bag-of-words_model), [TF-IDF](https://en.wikipedia.org/wiki/Tf–idf) (Term Frequency-Inverse Document Frequency), and embeddings like [Word2Vec](https://en.wikipedia.org/wiki/Word2vec), [GloVe](https://nlp.stanford.edu/projects/glove/), and transformer based architectures like BERT and more, which capture the semantic meaning and relationships between words or sentences.

In this chapter, we'll use TF-IDF (Term Frequency-Inverse Document Frequency) for vectorizing our contents. Here's why:

- **Simplicity**: TF-IDF is straightforward to implement and understand, making it an excellent starting point for RAG systems.

- **Efficiency**: It's computationally lightweight, allowing for quick processing of large document collections.

- **No training required**: Unlike embedding models, TF-IDF doesn't need pre-training, making it easy to get started quickly.

- **Interpretability**: The resulting vectors are directly related to word frequencies, making them easy to interpret.


While more advanced methods like embeddings often provide better performance, especially for semantic understanding, we'll explore these in later chapters as we progress through the course.

Why Vectorize? Vectorization converts text into numerical representations (vectors), allowing us to perform similarity searches.

We'll use a simple TF-IDF vectorizer to create vectors for our chunks. It essentially creates vectors based on the frequency of words in each chunk compared to their frequency in the entire dataset.

https://github.com/wandb/edu/blob/1132cf1a59dabcb8974d6f9767ee021ae065a823/rag-advanced/notebooks/scripts/retriever.py#L17


## Key Takeaways

In this chapter, we've built a simple RAG pipeline from scratch. Here's what we've learned:

- **Data Processing**: How to ingest, chunk, and clean data using W&B Artifacts and Weave
- **Retrieval**: Implementing a basic TF-IDF based retriever
- **Response Generation**: Using Cohere's API and `command-r` model to generate responses based on retrieved context
- **RAG Pipeline**: Combining retrieval and generation into a cohesive system
- **Logging and Tracking**: Utilizing W&B Weave for efficient experiment tracking

---

![[2024-11-27 at 07.54.02@2x.png]]


![[2024-11-27 at 07.54.40@2x.png]]

https://github.com/wandb/wandbot

![[2024-11-27 at 07.58.20@2x.png]]

https://wandb.ai/wandbot/wandbot_public/reports/WandBot-GPT-4-Powered-Chat-Support--Vmlldzo0MTE5MDM5?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.

https://wandb.ai/wandbot/wandbot_public/reports/Refactoring-Wandbot-our-LLM-powered-document-assistant-for-improved-efficiency-and-speed--Vmlldzo3NzgyMzY4?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.

https://wandb.ai/wandbot/wandbot_public/reports/RAGs-To-Riches-Bringing-Wandbot-into-Production--Vmlldzo1ODU5ODk0?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.


https://wandb.ai/wandbot/wandbot-eval/reports/How-to-Evaluate-an-LLM-Part-1-Building-an-Evaluation-Dataset-for-our-LLM-System--Vmlldzo1NTAwNTcy?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.
https://wandb.ai/wandbot/wandbot-eval/reports/How-to-Evaluate-an-LLM-Part-2-Manual-Evaluation-of-Wandbot-our-LLM-Powered-Docs-Assistant--Vmlldzo1NzU4NTM3?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.
https://wandb.ai/wandbot/wandbot-eval/reports/How-to-evaluate-an-LLM-Part-3-LLMs-evaluating-LLMs--Vmlldzo1NzEzMDcz?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.


https://wandb.ai/wandbot/wandbot_public/reports/Evaluation-Driven-Development-Improving-WandBot-our-LLM-Powered-Documentation-App--Vmlldzo2NTY1MDI0?_gl=1*1hswusv*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.

### 80/20 Rule

![[2024-11-27 at 08.01.13@2x.png]]

![[2024-11-27 at 08.02.13@2x.png]]

In building Wandbot, we leveraged the 80/20 rule, roughly 80% of user queries can be effectively addressed by focusing on just 20% of the available information. 

Here's how we applied the 80/20 rule:

**Focus on the essentials:** We prioritized making sure the most important 20% of our documentation was top-notch and easily accessible.

**Iterate and improve**: We started by tackling the most common problems and gradually expanded from there.

**Manage technical debt:** We balanced quick fixes with building a system that would be easy to maintain in the long run.

  

We also know that LLMs aren't perfect. They can sometimes "hallucinate" – meaning they might generate incorrect or nonsensical information. We focused on minimizing hallucinations for the most frequent queries first.

Building an AI system like Wandbot involves balancing risks and rewards.

  

**Here's how we managed risks:**

- Phased rollout: We didn't launch Wandbot all at once. We started small and gradually expanded its use.
- Addressing challenges: We found ways to deal with inaccurate responses (by adding source citations), privacy concerns (by anonymizing data), and the need for human help (by making it easy for users to contact support).

**And here are the rewards we saw:**

- Happier users: People loved getting instant and accurate answers.
- Reduced support workload: Our support team had more time to focus on complex issues.
- Global reach: Wandbot provided expert assistance to users around the world, 24/7.

### RAG best practices

![[2024-11-27 at 08.04.18@2x.png]]

![[2024-11-27 at 08.05.28@2x.png]]

Building a great RAG system like Wandbot involves following some important best practices. Here are some key lessons we learned:

**1. Start with a clear purpose:**

Define exactly what you want your RAG system to do.  
Set specific goals and metrics to measure its success. For Wandbot, we wanted to improve how users navigate our documentation, so we tracked metrics like user satisfaction and search success rate.

**2. Ensure high-quality data:**

Your RAG system is only as good as the information it can access.  
Make sure your knowledge base is accurate, complete, and up-to-date.

**3. Embrace evaluation and iteration:**

Continuously test and evaluate your system's performance.~  
Use the results to identify areas for improvement and make changes accordingly.

**4. Develop a comprehensive evaluation framework:**

Don't just focus on accuracy.`  
Consider other factors like relevance, faithfulness to the source material, and user satisfaction.

**5. Involve subject matter experts:**

Even though LLMs are powerful, they can still make mistakes.  
Have experts review the system's responses regularly to ensure they are accurate and make sense.

**6. Prioritize user experience:**

Design a user interface that is intuitive and easy to navigate.  
Make it easy for users to find the information they need.

**7. Be transparent:**

Let users know they are interacting with a bot.  
Provide citations for the information your system provides so users can verify it if they want.

**8. Commit to continuous improvement:**

User needs and information change over time.  
Keep your knowledge base up-to-date and make ongoing improvements to your RAG system.

### Challenges and solutions

![[2024-11-27 at 08.08.06@2x.png]]

![[2024-11-27 at 08.08.36@2x.png]]

## Evaluation

![[2024-11-27 at 08.51.56@2x.png]]




![[2024-11-27 at 08.51.13@2x.png]]


![[2024-11-27 at 08.54.47@2x.png]]

![[2024-11-27 at 08.55.22@2x.png]]

![[2024-11-27 at 08.55.38@2x.png]]


Evaluating a RAG system involves assessing not just the overall performance but also the quality of its individual components.

**Types of Evaluation:**

**End-to-End (System) Evaluation:**

We start by evaluating the final response generated by the entire RAG pipeline. This is important because the response is often non-deterministic – meaning it can vary even for the same input query. We typically compare the generated response against a "ground truth" or ideal response to assess its quality.

**Component Evaluation:**

Since RAG systems have multiple parts (retrieval, re-ranking, generation), we also need to evaluate these components individually. This helps us pinpoint areas for improvement. For example, we might evaluate the retrieval system by comparing the retrieved context against a ground truth context or by asking an LLM to judge if the generated response is actually based on the retrieved context.

**Evaluation Without Ground Truth:**

Not all evaluations require ground truth. Here are some cases where we can evaluate without it:

- Direct Evaluation: We can measure specific aspects of a response directly. For example, we can use tools to assess the toxicity or racial bias of a generated response, or we can check if the response is grounded in the source text (e.g., by looking for citations).
- Pairwise Evaluation: We can compare two or more responses generated for the same query and judge which one is better based on criteria like tone, coherence, or informativeness.

**Evaluation with Ground Truth (Reference Evaluation):**

When we have a gold standard reference (a "correct" answer), we can perform reference evaluation. This is often used to evaluate the structure of a response or to check if it includes specific information that is expected.

**Evaluation Methods in Practice:**

- Eyeballing: The quickest way to evaluate is to simply look at the responses and see if they seem reasonable. However, this is not very reliable and won't catch all problems, especially edge cases.
- Manual Evaluation: Hiring human annotators (experts in the relevant domain) to evaluate responses is expensive and time-consuming, but it's the most reliable method.
- LLM as a Judge: We can use a powerful LLM to automatically score responses or evaluate components of our system. This is becoming increasingly popular as LLMs get better at understanding and evaluating language.

**Evaluation Datasets and Metrics:**

The effectiveness of your evaluation depends on your dataset and the metrics you choose.

- Relevance to Production: Your evaluation dataset should closely resemble the real-world data your system will encounter (the "production distribution"). Similarly, your evaluation metrics should be relevant to your specific use case.
- Challenges with Public Benchmarks: Public benchmarks can be helpful for comparing different systems, but they often don't perfectly match your specific production distribution or use case.
- Human Evaluation and User Testing: While slower and more expensive, human evaluation and user testing provide the most direct and relevant assessments of system performance.

**The Ideal Evaluation Approach:**

The goal is to build a small but highly representative evaluation dataset and leverage LLM judges to evaluate different components of your RAG system. By using techniques like LLM alignment (training LLMs to be better judges), we can push this mode of evaluation towards being both highly correlated with real-world performance and efficient enough for rapid iteration cycles.

https://wandb.ai/wandbot/wandbot_public/reports/Evaluation-Driven-Development-Improving-WandBot-our-LLM-Powered-Documentation-App--Vmlldzo2NTY1MDI0?_gl=1*149jk74*_gcl_au*MzY5MTg5OTEyLjE3MzI2NDQyNTY.

**Key Takeaway:** Evaluating RAG systems involves assessing both the overall system performance and the quality of individual components using a variety of methods, datasets, and metrics tailored to your specific application and use case.



## Eval retrivers

It's a search problem

![[2024-11-27 at 09.18.37@2x.png]]
![[2024-11-27 at 09.19.10@2x.png]]

![[2024-11-27 at 09.21.13@2x.png]]

Evaluating a RAG system's retriever involves understanding how well it can find relevant context for a given user query.

**Two Main Approaches:**

**Reference Evaluation:** We compare the context retrieved by our system against a set of ground truth contexts. This involves ranking the retrieved context based on its similarity to the ground truth.

**Direct Evaluation:** We can ask another LLM to act as a judge and assess whether the retrieved context is relevant to the user query.

In most cases, reference evaluation provides a more reliable measure of retriever quality because it relies on a predefined "correct" context.

  

**Generating Ground Truth Context:**

One way to create ground truth context is to:

- **Cluster Similar Chunks:** Group similar pieces of text (chunks) from your knowledge base together based on their semantic meaning.
- **Generate Queries:** For each cluster, create one or more queries that can only be answered using the information within that cluster. This ensures that the relevant context for those queries is well-defined.

  

**Information Retrieval (IR) Metrics:**

We can adapt traditional IR metrics commonly used in search engine evaluation to assess the performance of our RAG retrievers.

**Ranking-Based Metrics:** These metrics focus on the order in which relevant documents are retrieved:

- Hit Rate: Did we retrieve at least one relevant document?
- Mean Reciprocal Rank (MRR): How high was the first relevant document ranked?
- Normalized Discounted Cumulative Gain (NDCG): Considers both the relevance and the position of all retrieved documents.

**Predictive Quality Metrics:** These metrics measure the accuracy of the retriever in identifying relevant documents:

- Precision: Out of the documents we retrieved, how many were actually relevant?
- Recall: Out of all the relevant documents, how many did we retrieve?
- Mean Average Precision (MAP): The average precision across multiple queries.
- F1-Score: A balanced measure that combines precision and recall.

  

**Evaluating a TF-IDF Retriever:**

Let's walk through an example of evaluating a simple TF-IDF retriever (which we built in Chapter 1) using these metrics.

1. Load Data and Index: We'll load the chunked data from Chapter 1 and index it using the TF-IDF retriever (implemented as a Weaviate model).
2. Define Scoring Functions: The retriever_metrics.py file contains implementations of all the IR metrics we discussed. Each function takes the retrieved context and the ground truth context as input and returns a score. These functions are decorated with @weave.op to make them usable within the Weaviate evaluation framework.
3. Set up the Evaluation Pipeline: We'll use the Weave Evaluation tool to create an evaluation pipeline. This pipeline defines the evaluation dataset, the retriever to be evaluated, and the metrics to be calculated.
4. Run the Evaluation: We execute the evaluation pipeline, and Weaviate automatically calculates all the specified metrics for our TF-IDF retriever.
5. Analyze Results: We can view the evaluation results in two ways:
    - Summary Scores: Weaviate provides a summary table showing the mean score for each metric.
    - Weave Dashboard: The Weaviate dashboard offers a more detailed view, including per-sample scores, trace timelines (showing the retrieval process for each query), and filtering options to explore the results in depth.
### LLM as a judge
	**LLM as a Judge, here's how it works:**

1. System Prompt: We provide the LLM with a clear set of instructions (the system prompt). These instructions explain to the LLM its task – in this case, to evaluate the relevance of retrieved context to a given question and answer pair.
2. Rubric/Scoring Criteria: The system prompt also includes a rubric or scoring criteria. This defines the specific rules the LLM should follow when assigning scores. For example, we might tell the LLM to assign a score between 0 and 2, where 0 means irrelevant, 1 means neutral, and 2 means highly relevant.
3. Relevance Code: The LLM then examines each piece of retrieved context and assigns a relevance code based on the instructions and rubric. The output might look like a list of context IDs with their corresponding relevance scores.

  

**Metrics Based on LLM Judgments:**

We can then use the LLM's judgments to calculate metrics that reflect the retriever's performance:

- Mean Relevance: We can calculate the average relevance score across all retrieved contexts. A higher mean relevance suggests that the retriever is generally finding relevant information.
- Rank Score: This metric considers the position of the relevant chunks in the retrieved list. Ideally, the most relevant chunks should be ranked higher. The rank score might penalize systems that bury relevant information deep down in the retrieved list.

**Evaluation Pipeline with LLM Judge:**

We can integrate this LLM-based evaluation into our Weaviate evaluation pipeline:

- Define the LLM Evaluator: We need to create a function that sends the retrieved context and the question-answer pair to the LLM, gets the relevance scores, and calculates the mean relevance and rank score.
- Add to the Pipeline: We include this LLM evaluator function as one of the metrics in our Weaviate evaluation pipeline.
- Run the Evaluation: When we run the pipeline, Weaviate will automatically use the LLM to evaluate the retriever and report the mean relevance and rank score along with the other IR metrics.
### Assertions

![[2024-11-27 at 09.25.58@2x.png]]

**TLDR:** Heuristics-based evaluation provides a quick and easy way to check the structural aspects of your RAG system's output, while reference-based evaluation using traditional metrics allows for a more in-depth comparison with ground truth responses, helping you assess the overall quality and accuracy of your system's generated content.

Before we dive into more complex evaluation methods like using LLMs as judges, it's beneficial to start with simpler, heuristics-based approaches. This involves defining basic rules and checks to assess the structure and format of your RAG system's output.

**Direct Evaluation with Heuristics:**

Heuristics-based evaluation focuses on direct assessment without relying on ground truth answers. Here are some examples of structural checks you can implement:

- Check for specific elements: Does the response contain bullet points if the user asked for a list? Does it include code snippets if the query was about code?
- Enforce length constraints: Is the response within a reasonable length? Is it too short or too long?
- Validate structured output: If your RAG system is expected to generate structured output (e.g., JSON), you can check if the response is a valid JSON object.

These heuristics help enforce certain expectations about the output format, which can improve the robustness and reliability of your RAG system. They can catch obvious errors or inconsistencies before you move on to more sophisticated evaluation methods.

**Assertions and Unit Tests:**

You can implement these heuristics as assertions or unit tests within your RAG application code. This allows you to automatically check for these conditions during development and prevent unexpected outputs from reaching your users.

**Reference-Based Evaluation with Traditional Metrics:**

For a more comprehensive evaluation of response quality, we can use reference-based evaluation. This involves comparing the generated response to a ground truth or reference response.

Here are some common metrics used in reference-based evaluation:

- Similarity Ratio: This measures the degree of overlap between the generated response and the reference response, often after normalizing the text (e.g., removing punctuation and converting to lowercase). A higher similarity ratio indicates a closer match.
- Levenshtein Distance: This metric calculates the minimum number of edits (insertions, deletions, substitutions) needed to transform the generated response into the reference response. A lower Levenshtein distance suggests a higher similarity.
- ROUGE and BLEU: These metrics (commonly used in machine translation and text summarization) also assess the overlap between generated text and reference text, but they consider different aspects like word sequences (ROUGE) and precision (BLEU).

### Traditional NLP limitations

![[2024-11-27 at 09.27.17@2x.png]]

![[2024-11-27 at 09.28.10@2x.png]]

### LLM evaluation in action

**TLDR:** LLM evaluators offer a powerful way to assess the quality of generated responses in RAG systems. Analyzing the LLM judge's reasoning, providing feedback on its decisions, and iteratively refining the system prompt are crucial steps in aligning the LLM's judgments with human expectations and improving the overall evaluation process.

  

Let's see how an LLM evaluator can be used in practice to assess the quality of generated responses in a RAG system like Wandbot.

**Evaluation Criteria for Wandbot**

For our use case, we're primarily concerned with three aspects of response quality:

- Correctness: Does the response accurately answer the user's question?
- Relevancy: Is the response relevant to the user's query?
- Faithfulness: Is the response factually consistent with the information retrieved from the knowledge base?

In this [Colab](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter02.ipynb) example, we'll focus on implementing the correctness metric using an LLM evaluator. The relevancy and faithfulness metrics are left as an exercise for you to explore.

**Setting up the evaluation and analyzing results in the Weave Dashboard:**

We'll use [Weave Evaluation](https://weave-docs.wandb.ai/guides/core-types/evaluations?utm_source=course&utm_medium=course&utm_campaign=rag_course) to set up and run the evaluation, just like we did for the retriever.

The Weave dashboard provides a convenient way to explore the evaluation results in detail.

- Understanding a 0% Score: Let's say we run the evaluation and get a score of 0% for correctness. To understand why, we need to dig deeper.
- Analyzing the System Prompt: The first step is to examine the system prompt given to the LLM judge. This prompt contains the instructions and scoring criteria that the LLM uses to make its judgments. We can find the system prompt in the trace timeline for the evaluation run. In this example, the Cohere API is used as the LLM judge, and the cohere.async client's v2.chat method is responsible for making the API call.
- Understanding the Scoring Criteria: The system prompt will typically outline the information provided to the LLM (context, response, query), the evaluation criteria (e.g., correctness, relevance, faithfulness), and the scoring range (e.g., 0-2). For example, a score of 0 might indicate an incorrect response, while a score of 2 might represent a correct and comprehensive answer.
- Examining Examples: We can then look at specific examples from the evaluation dataset to see why the LLM judge assigned particular scores. The dashboard allows us to view the question, the generated response, the ground truth answer, and the LLM judge's reasoning for its score.
- The Judge's Decision: The LLM judge might also provide a decision (e.g., "correct" or "incorrect") based on its score. For example, it might only consider a response "correct" if it receives the highest possible score.

**Providing Feedback and Aligning the LLM Judge:**

- Feedback Mechanism: The Weaviate dashboard often provides a feedback mechanism, allowing you to provide feedback on the LLM judge's decisions. For example, you might use emojis (thumbs up/down) to indicate whether you agree or disagree with the LLM's assessment.
- Analyzing Feedback: This feedback data can be valuable for understanding discrepancies between human judgments and the LLM's judgments. By analyzing the cases where you disagree with the LLM, you can identify patterns and potential areas for improvement.
- Aligning the LLM Judge: You can use this feedback to refine the LLM evaluator. This might involve:
- Adjusting the System Prompt: Modifying the instructions or scoring criteria to better align with human preferences.
- Providing Additional Examples: Adding more examples to the LLM's training data to help it learn to make better judgments.

### LLM eval limitations

![[2024-11-27 at 09.58.15@2x.png]]

### Pairwise evaluation

![[2024-11-27 at 09.59.05@2x.png]]

![[2024-11-27 at 09.59.44@2x.png]]


**TLDR:** Human evaluation, particularly in the form of pairwise comparisons or A/B testing, can be a valuable addition to the evaluation process for RAG systems. It provides a way to validate the findings of automated evaluation methods and gain confidence in the system's performance improvements before deploying it to real users, especially when dealing with nuanced or subjective aspects of response quality.

Even though we were satisfied with the results of our LLM evaluator, which showed an 8% improvement in Wandbot's performance after the refactoring, we decided to take an extra step and conduct a human evaluation using pairwise comparison.

**Human Evaluation with Pairwise Comparison (A/B Testing):**

This involved setting up a simple A/B test where we compared the responses generated by the old version of Wandbot with those generated by the new, refactored version.

**The Process:**

- Platform: We used [Argilla](https://docs.argilla.io/latest/?utm_source=course&utm_medium=course&utm_campaign=rag_course) (a data annotation tool) to set up the A/B test. Alternatively, a simple radio app could also be used for this purpose.
- Evaluators: We asked our in-house Machine Learning Engineers (MLEs), who are familiar with the domain and the application, to act as evaluators.
- Task: For each query in the evaluation dataset, the evaluators were presented with two responses – one from the old system and one from the new system. They were asked to choose which response they felt better answered the given query.

**The Results:**

The results of the A/B test showed that the new, refactored system was preferred 60% of the time compared to the old system, which was preferred only 40% of the time.

**Benefits of Human Evaluation:**

This human evaluation provided us with additional confidence in the performance improvements indicated by the LLM evaluator. It confirmed that the changes we made not only resulted in higher scores according to the LLM judge but also led to a noticeable improvement in the quality of responses as perceived by human users.

**When to Use Human Evaluation:**

While human evaluation can be valuable, it's also more time-consuming and expensive than automated evaluation methods. Therefore, it's often used strategically, such as:

- Validating LLM Evaluators: Confirming the findings of LLM evaluators, especially when making significant changes to the system.
- Assessing Subjective Aspects: Evaluating aspects of response quality that are difficult to capture with automated metrics, such as clarity, helpfulness, or user satisfaction.
- Making High-Stakes Decisions: When deploying a new system or making changes that could have a significant impact on users, human evaluation can provide extra assurance.

### Conclusion

![[2024-11-27 at 10.00.43@2x 1.png]]

This concludes our chapter on evaluating LLM applications, specifically focusing on RAG systems. Let's recap the key takeaways:

1. Prioritize Evaluation:

Make sure to allocate sufficient time and resources to the evaluation process. Thorough evaluation is essential for building high-quality and reliable RAG systems.

2. Evaluate Components and the Whole System:

Evaluate both the individual components of your RAG system (e.g., retriever, generator) and the overall end-to-end performance. This helps you pinpoint specific areas for improvement and ensure that all parts of the system are working together effectively.

3. Choose the Right Evaluation Approach:

Select the most appropriate evaluation approach (direct, pairwise, or reference) based on your specific use case and the aspects of response quality you want to assess. You might use a combination of approaches to get a comprehensive understanding of your system's performance.

4. Build and Iterate on Your Evaluation Set:

Start building your evaluation set early in the development process. Don't wait until the end. Keep iterating and refining your evaluation set over time to ensure it remains relevant and representative of your application's real-world usage.

5. Use LLM Evaluators Wisely:

LLM evaluators can be powerful tools, but they need to be used thoughtfully. Make sure to:

- Carefully craft the system prompt to provide clear instructions and scoring criteria.
- Align the LLM evaluator's judgments with human preferences through feedback and iteration.
- Be aware of the potential for non-determinism and run multiple trials.

6. Invest in Evaluation Infrastructure:

Spend time integrating your evaluation pipeline with good tooling and infrastructure early on. This will allow you to automate the evaluation process, track results efficiently, and iterate more rapidly.

By following these best practices, you can build robust and reliable RAG systems that meet your users' needs and deliver high-quality responses.

  

**Key Takeaway:** Evaluating RAG systems is an ongoing process that requires careful planning, the selection of appropriate methods and metrics, and a commitment to continuous improvement. By investing in evaluation, you can build more robust, reliable, and effective LLM applications.

## Chapter 3. Data Ingestion and Preprocessing
![[2024-12-12 at 07.22.46@2x.png]]
### Notebook 3: Data preparation, chunking and BM25 Retrieval
**TLDR:** Proper tokenization and text cleaning are crucial steps in data ingestion. Using the correct tokenizer and removing irrelevant characters ensures that the RAG system can process the information effectively and improves the accuracy and efficiency of retrieval. Publishing the pre-processed dataset to a Weave dataset promotes reproducibility and allows for easy tracking of changes.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter03.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

In this hands-on session, we're going deeper into data ingestion and pre-processing techniques for our RAG system. We'll focus on tokenization, chunking, and explore different retrieval methods, emphasizing the importance of evaluating their impact on the pipeline's performance.

**Tokenization:**

In Chapter 1, we tokenized our text into words, but it's essential to use the tokenizer that corresponds to the language model we'll be using. Here, we're using the Cohere tokenizer to align with the Cohere language model we'll employ later. We update our raw data with the accurate token counts generated by the Cohere tokenizer, highlighting the potential difference between simple word counts and model-specific token counts.

Why is tokenization important?

- Context Windows: Language models have a limited context window – the maximum number of tokens they can process at once. Accurate tokenization helps manage these windows effectively.
- Computational Costs: The number of tokens directly influences the computational resources required to run the RAG system. Accurate token counts help estimate these costs

  

**Pre-processing Markdown:**

We need to clean and prepare our Markdown text for use in the RAG system.

We use a function (convert_contents_to_text) that first converts the raw Markdown to HTML, then utilizes Beautiful Soup (a library for parsing HTML) to remove elements like image links, images, and other formatting information, extracting the plain text content.

The make_text_tokenization_safe function removes any special characters that might interfere with tokenization. These characters are specific to the tokenizer we're using (Cohere in this case) and can vary between language models.

Why Clean the Text? Cleaning the text is vital for:

- Improving Retrieval Accuracy: Removing irrelevant characters or formatting helps the retrieval system focus on the meaningful content.
- Ensuring Smooth Tokenization: Special characters can sometimes disrupt the tokenization process, leading to errors or unexpected results.

  

**Publishing to Weave Dataset:**

We publish the pre-processed dataset to a Weave dataset for easy tracking, versioning, and reproducibility. This allows us to manage different versions of our dataset as we experiment with various pre-processing techniques.

### Notebook 3: Chunking in practice
**TLDR:** Semantic chunking, by grouping sentences based on meaning, offers a more context-aware approach to dividing text into chunks. This method helps improve the retrieval relevance of the RAG system, leading to more accurate and meaningful responses. Examining the specific chunking code can provide valuable insights into how this approach is implemented in practice.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter03.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

We're now moving on to chunking, a crucial step in preparing our data for efficient retrieval. In this hands-on session, we're employing a semantic chunking approach.

**Semantic Chunking** (aka Grouping by Meaning) 

Instead of dividing the text into fixed-length chunks, semantic chunking aims to group sentences together based on their meaning or topic.

It helps with: 

- Preserving Context: This method helps maintain the contextual relationships between sentences, ensuring that related information is kept together within a chunk.
- Adaptive Chunk Sizes: Chunk sizes can vary depending on the length of the semantic units in the text, resulting in more meaningful and coherent chunks.
- Semantic chunking can significantly improve the relevance of retrieved information. By keeping related sentences together, the RAG system is more likely to find chunks that contain the complete and relevant context for a given query.

### Notebook 3: BM25 Retrieval
- Best Matching 25
**TLDR:** Choosing the right retrieval method is crucial for RAG system performance. While TF-IDF is a simple and widely used method, more advanced techniques like BM25 often provide better accuracy and relevance. Evaluating different retrieval methods using a tool like Weave can help you determine the best approach for your specific application and data.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter03.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Now that we've prepared our data through tokenization and chunking, let's explore different retrieval methods and evaluate their impact on our RAG pipeline.

**TF-IDF (Term Frequency-Inverse Document Frequency):** This is a basic retrieval method that we used in Chapter 1. It assigns weights to terms in documents based on their frequency within the document and across the entire corpus.

**BM25 (Best Matching 25):** BM25 is a more advanced retrieval method that builds upon TF-IDF. It addresses some of the limitations of TF-IDF by:

- Considering Document Length: BM25 normalizes the term frequency based on the length of the document, preventing longer documents from being unfairly favored.
- Handling Term Frequency Saturation: BM25 uses a saturation function to prevent terms that appear very frequently in a document from having an overly strong influence on the relevance score.
- Probabilistic Model: BM25 employs a probabilistic model to estimate the relevance of documents to a query, making it more robust and accurate.

Ingesting Data and Evaluating Retrievers:

We'll prepare both the TF-IDF and BM25 retrievers by ingesting the pre-processed and chunked data. We'll then use Weights & Biases Weave to evaluate the performance of both retrievers. This will include assessing their retrieval accuracy (how well they can find relevant chunks for a given query) and their impact on the overall RAG pipeline. The Weave dashboard will allow us to compare the results of the evaluations, showing us which retrieval method performs better on various metrics.

In the Weave dashboard, we'll likely observe that the BM25 retriever generally outperforms the TF-IDF retriever on most evaluation metrics. This highlights the advantages of using a more sophisticated retrieval method like BM25, which considers additional factors like document length and term frequency saturation.

### Data ingestion
![[2024-12-12 at 07.32.41@2x.png]]

Data ingestion is the foundation of any RAG system. It's the process that takes raw information from various sources and transforms it into a format that the RAG system can effectively use for retrieval and response generation.

The quality of your data ingestion process has a direct impact on how well your RAG system performs. Imagine trying to find information in a library where all the books are piled up randomly – it would be nearly impossible! Similarly, if your RAG system's data is poorly organized and formatted, it will struggle to retrieve relevant information and generate accurate responses.

Good data ingestion, on the other hand, is like having a well-organized library with a clear cataloging system. It allows the RAG system to quickly and easily find the information it needs.

**The Three Pillars of Data Ingestion:**
![[2024-12-12 at 07.33.08@2x.png]]

We can break down the data ingestion process into three core components, or pillars:

**Data Parsing:**

This is the first step, where we handle the variety of formats your data might come in. Whether it's PDFs, Word documents, web pages, or code files, data parsing converts them all into a standardized format that the RAG system can understand.

**Chunking:**

Once we have the data in a consistent format, we need to break it down into smaller, more manageable chunks. This is crucial for efficient retrieval. Instead of searching through entire documents, the RAG system can focus on smaller chunks that are more likely to contain the relevant information.

**Metadata Management:**

Metadata is like adding tags or labels to your data. It provides extra information about the content without requiring the system to read through everything. This can include things like the author, date, source, topic, or keywords associated with a particular chunk of data. Metadata helps the RAG system understand the context and relevance of the information, improving retrieval accuracy.

  

**Working Together for a Robust RAG System:**

These three pillars work together to create a robust data ingestion pipeline. Data parsing ensures that the system can handle various data formats, chunking makes retrieval more efficient, and metadata management adds valuable context.

### Data parsing
![[2024-12-12 at 07.34.34@2x.png]]
**Key Steps in Data Preparation:**

**1. Cleaning and Extraction:**

The first step is to clean your data and extract the relevant information. This might involve removing unnecessary elements like headers, footers, advertisements, or boilerplate text. You want to focus on the core content that will be valuable for your RAG system.

**2. Conversion to Plain Text:**

LLMs work best with plain text. So, we need to convert all our data into this format. This might involve extracting text from PDFs, Word documents, or HTML pages.

**3. Segmentation:**

Next, we divide the text into smaller segments or chunks. This is crucial for efficient retrieval and prevents the "lost in the middle" problem, where important information might be buried within a large block of text.

**4. Vector Representations:**

We then convert these text chunks into numerical vector representations. This allows us to store and search the data efficiently using a vector database.

**5. Storing in a Vector Database:**

Finally, we store the vectorized data in a vector database, which is optimized for similarity search. This becomes our organized and easily searchable knowledge base for the RAG system.

  

**Data Parsing:**

Data parsing plays a vital role in this process. It's responsible for converting different document formats into the standardized plain text format that we need.

There are many great tools available for data parsing:

- Unstructured: A powerful library for extracting information from unstructured documents like PDFs, Word files, and HTML.
- Firecrawl: A tool for web scraping and extracting data from websites.
- Multi-on: An AI platform that offers document processing and automation capabilities.
- Textract (AWS): A cloud-based service from Amazon Web Services that can extract text and data from various document types.
- Azure Document Intelligence: A similar cloud service from Microsoft Azure for analyzing and extracting information from documents.

**Tailored Approach (Wandbot Example):**

While these off-the-shelf tools are useful, sometimes a more tailored approach is necessary. For example, in building Wandbot, we encountered specific document types that required custom parsing solutions:

- Custom Markdown Parser: We developed a custom parser to handle Markdown documents, ensuring that the structure and context of the text were preserved.
- NBConvert for Jupyter Notebooks: We used NBConvert to convert Jupyter notebooks into Markdown format, which could then be processed by our custom Markdown parser.
- Concrete Syntax Trees for Code: For code analysis, we used concrete syntax trees to capture the syntactic structure of the code, allowing us to extract meaningful information about the code's functionality.


![[2024-12-12 at 07.35.23@2x.png]]

### Chunking
![[2024-12-12 at 07.36.47@2x.png]]

**TLDR:** Chunking is a critical step in data ingestion for RAG systems. Choosing the right chunking method and finding the optimal balance between context and focus can significantly impact the performance of your system. For more complex applications, consider exploring advanced chunking techniques to create a more nuanced and effective

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter03.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Chunking is a fundamental concept in data ingestion for RAG systems. It involves breaking down large documents into smaller, more manageable units called chunks.

Chunking serves two main purposes:

- Creating Context-Rich Segments: Chunks need to contain enough information to be meaningful on their own. They should provide sufficient context for the RAG system to understand the information and generate relevant responses.
- Enabling Efficient Retrieval: Chunks should be small enough to be easily processed and retrieved. If chunks are too large, the retrieval process can become slow and inefficient. It also increases the risk of the "lost in the middle" problem, where relevant information might be buried deep within a large chunk.

There are several different approaches to chunking:

- Fixed-Length Chunking: This is the simplest method, where you divide the text into chunks of a fixed length, either based on the number of words or the number of characters.
- Semantic Chunking: This approach aims to divide the text based on natural breaks in meaning or topic. It's like dividing a book into chapters, where each chapter focuses on a specific theme or idea.
- Content-Based Chunking: This method adapts the chunking strategy to the structure and format of the document. For example, you might chunk a code file based on function definitions or a web page based on HTML tags.

  

**Developing an Optimal Chunking Strategy**

There's no one-size-fits-all solution for chunking. The best approach depends on your specific use case and the nature of your data. Here are some factors to consider:

- Well-Defined Use Case and Success Metrics: Start by clearly defining what you want your RAG system to do and how you will measure its success. This will guide your chunking strategy.
- Evaluation-Driven Development: Experiment with different chunking methods and evaluate their performance using your chosen metrics. Use the evaluation results to iteratively refine your chunking strategy.
- Data Quality: Ensure that your input data is clean and well-structured. Garbage in, garbage out!
- Robust Evaluation Framework: Develop a comprehensive evaluation framework that can accurately assess the effectiveness of your chunking strategy.

  

**Tailored Chunking (Wandbot Example)**

In Wandbot, we used a tailored approach to chunking:

- Semantic-Based Chunking (for Markdown): For our Markdown documentation, we used a semantic-based approach that preserved the natural structure of the articles. We kept headers, sections, and paragraphs together within chunks to maintain the logical flow of information.
- Structure-Based Chunking (for Code): For code examples, we used a structure-based method to ensure that function definitions and code blocks remained intact within chunks.

  

**Balancing Context and Focus**

The key to effective chunking is finding the right balance between providing sufficient context and keeping the chunks focused. If chunks are too large, they become unwieldy and difficult to process. If they are too small, they might lack the necessary context to be meaningful.

  

**Advanced Chunking Techniques**

For more complex RAG systems, you might need more sophisticated chunking techniques:

- Hierarchical Chunking: This involves creating a hierarchy of chunks, where parent chunks provide broader context and child chunks offer more specific details. This can be useful for representing different levels of information within a document.
- Small-to-Big Chunking: This technique starts with small, focused chunks and then expands to include more context as needed. It can be particularly helpful for handling long sections of text.

Benefits of Advanced Chunking:

- Providing Broader Context: Hierarchical chunking allows you to provide broader context from parent chunks when answering specific queries.
- Maintaining Coherence: Sentence window chunking (a type of small-to-big chunking) helps maintain the coherence of responses, especially when pulling information from lengthy documents.

Nuanced Chunking:

The goal of advanced chunking techniques is to be more nuanced in how you break down content. You're not just dividing it into uniform pieces, but you're doing so in a way that preserves and enhances meaning, leading to more coherent and contextually relevant responses from your RAG system. knowledge base.

![[2024-12-12 at 07.38.06@2x.png]]

![[2024-12-12 at 07.39.25@2x.png]]

### Metadata management
**TLDR:** Metadata is a powerful tool for enhancing RAG systems. By adding meaningful metadata to your data, you can improve the retrieval process, provide additional context, and ultimately enable your system to generate more accurate and relevant responses.


Metadata plays a vital role in enhancing the effectiveness of RAG systems. It provides additional context and information about the data, helping the system understand the meaning and relevance of the content.

Metadata is essentially data about your data. It's like the label on a jar that tells you what's inside without having to open it.

In RAG systems, we typically work with two types of metadata:

- Document Metadata: This provides information about the entire document, such as:
    - Title: The title of the document.
    - Source: Where the document came from (e.g., website, book, internal documentation).
    - Summary: A brief overview of the document's content.
- Chunk Metadata: This gives context to specific segments of text within a document, such as:
    - Structural Information: Is this chunk a header, a paragraph, a code block, etc.?
    - Programming Language (for Code): What programming language is used in this code chunk?
    - Version-Specific Information: Is this chunk relevant to a specific version of a product or software?

  

**Extracting and Enhancing Metadata:**

We can use various techniques from Natural Language Processing (NLP) to extract and enhance metadata:

- Entity Extraction: Identifying and classifying named entities in the text, such as people, places, organizations, or dates.
- Classification: Categorizing the content and assigning tags or labels based on its topic or theme.
- Relationship Extraction: Identifying relationships between different entities in the text (e.g., "person X works at company Y").

  

**Wandbot's Metadata Strategy:**

In Wandbot, we use a two-pronged approach to metadata:

- Document-Level Metadata: We capture information about the source of the document (e.g., official docs, GitHub repo, blog post), the type of document (e.g., API documentation, tutorial, conceptual guide), and the language of the document.
- Chunk-Level Metadata: We extract structural information (e.g., header, code block, paragraph), identify the programming language used in code chunks, and tag version-specific information. This is especially helpful when users ask about specific features or functions.

  

**Benefits of Effective Metadata:**

A well-designed metadata strategy can significantly improve the accuracy and relevance of responses generated by a RAG system. Here's how:

- Enhanced Retrieval: Metadata helps the system quickly narrow down the search space to find the most relevant chunks of information. For example, if a user asks about a specific function in a particular version of a software, the system can use version-specific metadata to quickly identify the relevant code chunks.
- Improved Contextual Understanding: Metadata provides additional context that helps the system understand the meaning and relevance of the content. For example, knowing that a chunk is a header or a code block gives the system clues about how to interpret the information within that chunk.
- More Accurate Responses: By combining content with relevant metadata, the RAG system can generate more accurate and contextually appropriate responses.

![[2024-12-12 at 07.41.33@2x.png]]


![[2024-12-12 at 07.43.31@2x.png]]

### Data ingestion challenges
**TLDR:** Data ingestion is a critical but complex process in RAG development. Be prepared to face challenges like incorrect parsing, format discrepancies, incoherent chunking, and outdated knowledge. By using a combination of tailored solutions, systematic evaluation, and a staged approach, you can effectively address these issues and create a robust and reliable data ingestion pipeline for your RAG system. Continuous monitoring and refinement of your ingestion process are essential for maintaining the accuracy and effectiveness of your RAG application.


Data ingestion is a complex process, and it's not uncommon to encounter challenges along the way. Here are some common pitfalls we faced during the development of Wandbot:

**Data Parsing Issues:**

- Incorrect Parsing: Out-of-the-box data parsing tools are often designed to handle a wide range of document formats, but they might not always parse our specific documentation or code correctly. This can lead to missing information or incorrect interpretation of the content.
- Format Discrepancies: Our dataset might include information from various sources, and these sources might use different formats or conventions. These inconsistencies can make it difficult to create a unified and standardized knowledge base.
- Incoherent Chunks: Choosing the wrong chunking method or using inappropriate chunk sizes can lead to incoherent chunks – chunks that split apart related information. This can negatively impact the quality of the RAG system's responses, as it might miss crucial context.
- In rapidly evolving fields like AI, information can become obsolete very quickly. It's essential to have mechanisms in place to keep the knowledge base up-to-date, so the RAG system provides accurate and current information.

**Solutions for Ingestion Issues:**

- Tailored Parsing Approach: We addressed our parsing issues by developing a custom parsing approach that was tailored to the specific structure and format of our documentation and code.
- Systematic Chunking Evaluation: We implemented a systematic evaluation process for our chunking strategy, continuously testing different methods and chunk sizes to find the best approach. We used metrics to assess the coherence and relevance of the chunks.
- Staged Evaluation: Instead of trying to evaluate and fix all issues at once, we adopted a staged approach. We broke down the evaluation process into manageable groups, running evaluations on major groups of commits. This allowed us to identify and address problems more effectively.

**Ongoing Process:**

It's important to remember that troubleshooting data ingestion issues is an ongoing process. As your RAG system evolves, you'll encounter new challenges and need to adapt your ingestion pipeline accordingly.

![[2024-12-12 at 07.44.31@2x.png]]

### Best practices
**TLDR:** Building a successful RAG system involves more than just technical implementation. It requires a thoughtful approach to data ingestion, a commitment to continuous evaluation, and a collaborative spirit to address challenges and optimize performance. By applying the lessons learned from Wandbot, you can create a more effective, efficient, and adaptable RAG system that meets the needs of your users.

  

As we conclude this chapter on data ingestion and pre-processing, let's look back at some key insights we gained from building and maintaining Wandbot:

**1. Tailored Preprocessing is Essential:**

There's no one-size-fits-all approach to data ingestion for RAG systems. Your pipeline needs to be tailored to the unique characteristics of your data and the specific requirements of your use case. For example, the way you parse documents, chunk text, and manage metadata should be optimized for your particular data format and the types of queries your RAG system is expected to handle.

**2. Balancing Efficiency and Accuracy:**

Striving for perfect accuracy in every aspect of the data ingestion process can sometimes lead to a system that's slow and inefficient. It's important to find the right balance between efficiency and accuracy. You might need to make trade-offs in certain areas to achieve a responsive and reliable system.

**3. Continuous Evaluation is Key:**

RAG systems are not "set it and forget it" solutions. They require ongoing monitoring and evaluation to ensure they continue to perform well. Regularly assess the accuracy, relevance, and timeliness of your system's responses, and use the evaluation results to identify areas for improvement.

**4. Collaboration Drives Innovation:**

Some of the most significant breakthroughs in our development process came from collaborative problem-solving sessions involving team members from different disciplines. Bringing together diverse perspectives and expertise can lead to creative solutions and more effective optimization strategies.

  

These insights from our experience with Wandbot can be valuable for anyone building a RAG system.

Remember:

- Customize your ingestion pipeline to suit your needs.
- Find the right balance between efficiency and accuracy.
- Continuously evaluate your system's performance and make adjustments.
- Embrace collaboration to solve challenges and drive innovation.
![[2024-12-12 at 07.46.21@2x.png]]

## 4. Query Enhancement
**TLDR:** Query enhancement is a crucial step in building sophisticated and user-friendly RAG systems. By improving the system's ability to understand user intent, query enhancement leads to more accurate retrieval, more relevant responses, and a better overall user experience. This chapter will equip you with the knowledge and tools to effectively enhance queries in your own RAG applications.

![[2024-12-12 at 07.49.40@2x.png]]

Think of query enhancement as giving your RAG system a superpower – the ability to read between the lines and understand the true meaning behind a user's question.

User queries can often be ambiguous, incomplete, or contain errors. They might use slang, jargon, or make assumptions about what the system already knows. Query enhancement helps to address these issues by:

- Clarifying the User's Intent: It helps the RAG system to more accurately understand what the user is really asking.
- Improving Retrieval Accuracy: By providing a clearer and more complete query, the system can better find the most relevant information in the knowledge base.
- Generating More Relevant Responses: With a better understanding of the user's intent, the system can generate responses that are more focused, informative, and helpful.

This chapter will cover four key techniques for query enhancement. We'll explore each of these techniques in detail, providing practical examples from our experience with Wandbot to demonstrate how they work in real-world applications.

### Notebook 4: Query enhancement

**TLDR:** Query enhancement can be a powerful technique for improving RAG systems, but it's important to approach it with a balanced perspective. Consider the potential benefits and drawbacks, carefully evaluate the impact on performance and user experience, and adapt your evaluation methods accordingly.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter04.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

In this hands-on session, we explored how to **implement and evaluate query enhancement** techniques in a RAG system.

We started by creating a _QueryEnhancer_ module, which performs three key tasks:

- Language Identification: It detects the language of the query, which is essential for multilingual support (in this case, English, Japanese, and Korean).
- Intent Classification: It determines the user's intent or purpose behind the query. For example, is the user asking about a product feature, requesting technical support, or seeking general information?
- Subquery Generation: For complex queries, it breaks them down into smaller, more focused sub-queries. This helps the RAG system retrieve more specific and relevant information.

Next, we built a _QueryEnhancedRAGPipeline_ that integrates the query enhancer into our existing RAG pipeline. This enhanced pipeline leverages the output from the query enhancer in several ways:

- Multiple Query Retrieval: It uses the generated sub-queries to perform multiple searches, potentially retrieving a wider range of relevant information.
- Context Deduplication: It removes duplicate or redundant information from the retrieved context before passing it to the LLM, optimizing the LLM's input and potentially improving response quality.
- Intent-Based Workflow: It uses the classified intent to handle queries differently. For example, it might handle off-topic or inappropriate queries in a specific way, such as providing a generic response or redirecting the user to another resource.

We then compared the performance of our query-enhanced RAG pipeline to a simpler RAG pipeline from the previous chapter.

**Similar Correctness Scores:** Both pipelines achieved similar correctness scores, indicating that the query enhancements didn't necessarily improve the accuracy of the factual information in the responses.

**Higher Response Quality (Simple Pipeline):** The simple RAG pipeline showed slightly better overall response quality, suggesting that the additional complexity introduced by query enhancement might have affected the coherence or readability of the responses.

**Significantly Higher Latency (Query-Enhanced Pipeline):** The query-enhanced pipeline exhibited significantly higher latency, meaning it took longer to generate responses. This is likely due to the additional processing steps involved in query enhancement.

  

These results highlight important considerations when designing RAG systems:

- Complexity vs. Improvement: Adding complexity doesn't always translate into direct improvements in automated metrics. It's important to carefully evaluate the trade-offs between complexity and performance gains.
- Latency Impact: Increased latency can significantly impact the user experience. If the system takes too long to respond, users might get frustrated and abandon the interaction.
- Evaluation Methods: As you add more complex features to your RAG pipeline, you might need to refine your evaluation methods to better capture the nuances of the system's performance.


### 4 key techniques for query enhancement
![[2024-12-12 at 07.52.52@2x.png]]
**TLDR:** Query enhancement is essential for building sophisticated RAG systems that can effectively handle complex and nuanced user queries. By clarifying user intent, improving retrieval accuracy, and generating more relevant responses, query enhancement enhances the overall user experience and makes RAG systems more valuable and practical.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter04.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Query enhancement is crucial for building effective RAG systems. It acts as an interpreter, refining user queries into a form the system can understand and process more effectively.

Imagine trying to understand a conversation where you only hear snippets of random sentences. You'd likely miss the context and the true meaning. This is similar to what a RAG system experiences without query enhancement.

By enhancing user queries, we can:

- Clarify User Intent: Help the system understand what the user is really asking, even if the query is ambiguous or incomplete.
- Improve Retrieval Accuracy: Guide the system to find the most relevant information in the knowledge base.
- Generate More Relevant Responses: Provide the system with enough context to create more focused and helpful answers.

  

**Four Key Techniques:**

![[2024-12-12 at 07.53.44@2x.png]]
1. Conversation History Utilization:

- Giving the System a Memory: This technique allows the RAG system to remember previous interactions with the user.
- Example: If a user asks a follow-up question, the system can refer to the previous conversation to provide a more relevant response.

![[2024-12-12 at 07.54.40@2x.png]]

2. Intent Recognition:

- Understanding the "Why": This helps the system determine the user's goal or purpose behind the query.
- Example: Classifying a query like "How do I log metrics?" as related to "product features" guides the retrieval process toward relevant documentation.

![[2024-12-12 at 07.55.44@2x.png]]

3. Keyword Extraction and Expansion:

- Enhancing Domain Specificity: This involves identifying and enhancing important keywords and phrases to improve retrieval accuracy, especially for domain-specific knowledge.
- Example: Adding keywords like "logging metrics," "experiment tracking," and "W&B usage" to the query "How do I log metrics?" helps the system find more relevant information.

![[2024-12-12 at 07.56.48@2x.png]]

4. Query Decomposition: ✨

- Breaking Down Complexity: This technique breaks down complex, multi-part queries into simpler sub-queries that the system can process more effectively.
- Example: Decomposing the query "How do I log metrics?" into sub-queries about the steps involved, examples, and best practices allows the system to address all aspects of the question.
![[2024-12-12 at 07.57.42@2x.png]]


  

**Wandbot Example:**

In Wandbot, we implemented all four of these query enhancement techniques. This significantly improved the system's ability to understand user queries, resulting in more accurate retrieval and more relevant, helpful responses.


### Enhancing context
**TLDR:** Metadata extraction adds a valuable layer of contextual understanding to RAG systems. By identifying and utilizing relevant metadata, you can create a more nuanced, efficient, and user-friendly RAG experience, especially in cases where supporting multiple languages or adapting to specific user contexts is important.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter04.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Metadata extraction is a powerful technique for enhancing the context of user queries in RAG systems. It's like giving your system extra senses – allowing it to perceive more information about the user and their situation.

Metadata extraction involves identifying and extracting additional information about the user's query. This metadata might include things like:

- Language: The language in which the query is written.
- Location: The user's geographical location.
- Time: The time of day the query was submitted.
- User Profile: Information about the user's past interactions or preferences (if available).

This extracted metadata provides valuable context that helps the RAG system to:

- Interpret the Query More Accurately: For example, knowing the user's language allows the system to use the appropriate language-specific resources and avoid misinterpretations.
- Personalize the Response: Metadata like user profile information can be used to tailor the response to the individual user's needs.

  

**Wandbot Example: Language Detection**

In Wandbot, we use metadata extraction to detect the language of the user's query. This is essential for our multilingual support, as Wandbot can handle queries in both English and Japanese.

- Routing to Language-Specific Resources: By identifying the query's language, we can direct the system to retrieve information from the appropriate language-specific documentation.
- Generating Responses in the Correct Language: We can ensure that the generated response is also in the language the user understands.

![[2024-12-12 at 07.59.25@2x.png]]

**Benefits of Metadata Extraction:**

- Contextual Adaptation: The RAG system can adapt its behavior based on the extracted metadata, leading to more relevant and personalized interactions.
- Improved Efficiency: Metadata can help streamline the retrieval process, as the system can quickly narrow down its search based on the extracted information.
- Consistent and Appropriate Responses: By taking metadata into account, the RAG system can generate responses that are more consistent with the user's context and expectations.

### LLM in query enhancement
![[2024-12-12 at 08.00.30@2x.png]]
**TLDR:** Using LLMs with function calling capabilities is a powerful and efficient approach to query enhancement in RAG systems. It can significantly improve the accuracy, relevance, and adaptability of the system, leading to a better user experience.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter04.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)
- [LLM Engineering: Structured outputs](https://www.wandb.courses/courses/steering-language-models) course

  

Traditionally, query enhancement has relied heavily on techniques from Natural Language Processing (NLP), such as classification models for intent recognition and keyword extraction algorithms. However, with the advancements in LLMs, we can now leverage their powerful capabilities for query enhancement.

Wandbot utilizes LLMs with function calling capabilities to enhance user queries. This means we can instruct the LLM to perform specific actions and generate structured output in a desired format (often JSON).

The Process:

- Prompting the LLM: We provide the LLM with the user's query and instruct it to enhance the query by:
- Classifying the intent: Determining the user's goal or purpose.
- Extracting relevant keywords: Identifying important terms and phrases.
- Generating sub-queries: Breaking down complex queries into smaller parts.
- Structured Output (JSON): The LLM generates its output in a structured JSON format, making it easy to parse and use within the RAG system.
- Validation with Pydantic: We use Pydantic models to validate the LLM's output, ensuring that it conforms to our expected schema. This helps prevent errors and ensures data consistency.

**Benefits of Using LLMs:**

Improved Accuracy and Nuance: LLMs, with their vast knowledge and contextual understanding, often outperform traditional NLP models in tasks like intent classification and keyword extraction. They can also generate more nuanced and sophisticated query reformulations, especially for complex queries.

No Need for Training NLP Models: By using LLMs, we can avoid the time and effort required to train separate NLP models for query enhancement.

Flexibility and Intelligence: LLMs provide a high degree of flexibility and adaptability in handling various types of queries. They can readily adjust to changes in language or domain-specific terminology.

  

**Impact on RAG Performance:**

By enhancing queries with the help of LLMs, we can enable our RAG system to understand user intent better, retrieve more relevant information from the knowledge base and generate more contextually appropriate and accurate responses.

[**LLM Engineering: Structured outputs**](https://www.wandb.courses/courses/steering-language-models)

If you want to dive deeper into the world of structured outputs we can recommend the LLM Engineering: Structured outputs course. Improve your LLM engineering skills with Jason Liu, the author of the Instructor library. Learn about structured JSON output handling, function calling, complex validations with Pydantic and more in this short and helpful course!


### Query enhancement case study: Wandbot

![[2024-12-12 at 08.01.57@2x.png]]
**TLDR:** Query enhancement is essential for building high-performing RAG systems. By following best practices, addressing common challenges, and embracing an evaluation-driven approach, you can create a robust, efficient, and user-friendly RAG system that delivers accurate and relevant information to your users.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter04.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Query enhancement, as we've seen, can significantly impact the performance and effectiveness of RAG systems. In the case of Wandbot, implementing the query enhancement techniques we discussed led to impressive improvements:

- Response accuracy increased from 55% to 72%.
- Intent classification became more accurate.
- Keyword extraction became more relevant.
- Query decomposition helped handle complex queries effectively.
- Multilingual support improved.

  

**Measuring Improvements:**

We use various Key Performance Indicators (KPIs) and metrics to track the impact of these changes:

- Retrieval Relevance: We assess how well the system is finding relevant information from the knowledge base.
- Response Accuracy: We evaluate the correctness and completeness of the generated responses.
- User Satisfaction: We gather feedback from users to understand their overall experience with the system.

  

**Holistic Evaluation:**

It's crucial to take a holistic approach to evaluation. We don't just focus on isolated metrics but consider the overall impact on the system's performance and the user experience.

Evaluation is not a one-time task. We regularly assess these KPIs and use the insights to guide our ongoing refinement process. This evaluation-driven approach is crucial for continuous improvement.

  

**Best Practices:**

Here are some key best practices for developing and maintaining effective RAG systems:

- Evaluation-Driven Development: Make evaluation an integral part of your development process. Regularly analyze user interactions and system performance, and use the insights to make adjustments.
- Continuous Learning and Adaptation: The field of AI is constantly evolving. Stay up-to-date with new advancements and adapt your RAG system accordingly.
- Logging and Monitoring: Implement robust logging and monitoring systems early on. This will provide valuable data for identifying issues, tracking performance, and making informed decisions about optimizations.

  

**Challenges and Solutions:**

Here are some common challenges you might face and potential solutions:

**Ambiguous Queries:** Improve your intent classification models to better handle unclear or ambiguous queries.

**Flexibility vs. Precision:** Find the right balance between flexibility (handling a wide range of queries) and precision (generating very specific responses). This might involve fine-tuning your query rewriting techniques.

**Multilingual Support:** Ensure your system can accurately detect the language of a query and has access to appropriate language-specific resources.

**Latency:** Optimize your RAG system for speed without sacrificing accuracy. This might involve using more efficient algorithms, caching results, or optimizing your infrastructure.

![[2024-12-12 at 08.02.49@2x.png]]

## 5.1 Advanced Retrieval and Reranking
**TLDR:** This chapter will equip you with advanced retrieval and reranking techniques to build more sophisticated and effective RAG systems. By understanding these techniques and how to apply them, you can significantly improve the quality, relevance, and efficiency of your RAG system's retrieval capabilities.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources) include the entire set of video transcripts (26k tokens) and 7 notebooks (20k tokens) available as markdown for easy copy-paste to an LLM. 

  

In this chapter, we'll level up our understanding of retrieval in RAG systems. We'll move beyond the basic retrieval methods we covered earlier and explore advanced techniques to significantly enhance the quality and relevance of the information we retrieve.

Simple retrieval systems, while useful, can struggle with complex or nuanced queries. They might:

- Miss Relevant Information: Basic keyword matching might not capture the full meaning or intent of a complex query.
- Retrieve Too Much Information: The system might return a large number of results, making it difficult for the user to find what they need.
- Fail to Prioritize Relevance: The retrieved results might not be ranked in order of importance, burying the most relevant information.

To address these limitations, we need more sophisticated retrieval and reranking techniques:

**Query Translation:** Transforming the user's query into a more effective form for retrieval. This might involve techniques like query expansion, where related terms or synonyms are added to the query.

**Metadata Filtering:** Using metadata associated with documents or chunks to filter and refine search results. For example, if a user asks a question about a specific product version, we can use metadata to filter results to only include documents relevant to that version.

**Routing:** Directing queries to specific sections or subsets of the knowledge base based on metadata or other criteria. This can improve efficiency and relevance by focusing the search on the most likely sources of information.

**Reranking:** Reordering the retrieved results to prioritize the most relevant items. This involves using additional signals or models to assess the relevance of each retrieved item and adjust its ranking accordingly.

**Embedding Adapter:** A technique introduced by Chroma, a vector database, that allows for adapting embeddings to improve retrieval performance.

  

We'll also have insights from two experts:

**Charles** from [**Weaviate**](https://weaviate.io/developers/weaviate?utm_source=course&utm_medium=course&utm_campaign=rag_course) will dive into production-grade hybrid retrieval systems, combining different retrieval methods for enhanced performance.

**Meor** from [**Cohere**](https://docs.cohere.com/?utm_source=course&utm_medium=course&utm_campaign=rag_course) will discuss building RAG systems that can access external tools like web search engines or SQL databases, expanding the system's knowledge and capabilities.

  

**Revisiting Retrieval:**

Before we dive into advanced techniques, let's quickly recap the fundamentals of retrieval:

- Indexing: During indexing, we use an embedding model to convert our documents or chunks of text into vector representations (embeddings).
- Vector Store: The collection of documents and their corresponding embeddings is called a vector store.
- Query Time Retrieval: When a user submits a query:
    - The query is embedded using the same embedding model.
    - A similarity function (e.g., cosine similarity) is used to find the top-k closest embeddings in the vector store.
    - These top-k embeddings are mapped back to their corresponding text chunks, which are then returned as the retrieved results.


![[2024-12-12 at 08.08.01@2x.png]]


![[2024-12-12 at 08.08.47@2x.png]]

### Limitations

**TLDR:** These limitations highlight the need to move beyond basic retrieval methods in RAG systems, especially for complex applications. Advanced techniques, such as using deep neural network embeddings, addressing query-document misalignment, handling complex queries, and prioritizing relevant chunks, are essential for improving the accuracy, relevance, and efficiency of information retrieval.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

As RAG systems become more sophisticated and handle increasingly complex queries, simple retrieval methods start to show their limitations. Let's explore some key arguments for moving beyond basic retrieval:

**1. Limited Contextual Understanding in Embeddings:**

While methods like TF-IDF and BM25 are effective for basic retrieval, they have a limited capacity to capture the different meanings and contexts of the same word. They primarily rely on word frequencies and co-occurrences without a deeper understanding of semantic relationships.

To address this, we need to use embeddings generated by deep neural networks. These models are trained on vast amounts of text data (billions of tokens) and can learn more nuanced representations of words and their various contexts. They can better capture semantic similarities and relationships between words, improving the accuracy of retrieval.

**2. Misalignment Between Queries and Documents:**

User queries often lack the precise language or structure that aligns perfectly with the wording used in relevant documents. This mismatch can make it difficult for simple retrieval systems to find the best matches.

Example: A user might ask, "How do I track experiments in W&B?" while the relevant document uses the phrase "experiment tracking." A simple keyword-based retrieval system might miss this connection.

**3. Query Complexity:**

Simple queries, like "What is W&B?", are easier to match to a single relevant document or chunk. However, complex queries, which might involve multiple concepts or sub-questions, often require retrieving information from multiple parts of the knowledge base.

Example: A query like "How can I compare different model versions and visualize their performance metrics?" might require retrieving information about model versioning, performance metric logging, and visualization tools within W&B. A simple retrieval system might only find information about one of these aspects.

**4. Position of Relevant Chunks:**

The order in which retrieved results are presented is crucial. The most relevant information should be ranked higher to ensure the user can easily find it. Simple retrieval systems might not adequately prioritize the most relevant chunks.

![[2024-12-12 at 08.09.54@2x.png]]

### Compare evaluations

**TLDR:** This comparison demonstrates the potential benefits of using a dense retriever based on a sophisticated embedding model. Dense retrievers can provide more accurate and relevant retrieval results, especially for complex queries. However, it's essential to evaluate the performance of different retrieval methods in your specific use case, as factors like latency can be influenced by various factors.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

We're comparing the performance of a traditional TF-IDF retriever with a more advanced dense retriever based on the Cohere Embed English V3 embedding model.

**Dense Retriever Implementation:**

- [Cohere Embed English V3](https://docs.cohere.com/docs/cohere-embed?utm_source=course&utm_medium=course&utm_campaign=rag_course): This model generates dense vector representations of text, capturing semantic relationships and context more effectively than sparse methods like TF-IDF.
- [Colab Notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb): The implementation of the dense retriever using Cohere Embed English V3 is available in the Colab Notebook for this chapter, providing a practical example for you to explore.

  

**Evaluation Results:**

We used the Weave evaluation comparison dashboard to analyze the performance of both retrievers. Here are some key observations:

- Better F1 Score (Dense Retriever): The dense retriever achieved a higher F1 score than the TF-IDF retriever, indicating better retrieval accuracy.
- Higher NDCG (Dense Retriever): The dense retriever also showed a higher NDCG score, which is a more reliable ranking-based metric than MRR or hit rate. This suggests that the dense retriever is better at retrieving and ranking the most relevant items.
- Counterintuitive Latency: Surprisingly, the TF-IDF retriever was slower than the dense retriever. This is counterintuitive because TF-IDF is often considered a simpler and faster method. There could be several reasons for this, such as differences in implementation or the specific dataset used. It's worth investigating this further to understand the underlying factors.

  

**Implications:**

These results highlight the advantages of using a dense retriever based on a powerful embedding model like Cohere Embed English V3. Dense retrievers can capture semantic relationships more effectively, leading to improved retrieval accuracy and relevance, as demonstrated by the higher F1 and NDCG scores.

The counterintuitive finding about latency underscores the importance of careful evaluation and profiling. It's crucial to measure the actual performance of different retrieval methods in your specific context, as assumptions about speed might not always hold true.

### Query translation

**TLDR:** Query translation techniques offer powerful strategies for improving retrieval effectiveness in RAG systems, especially for complex queries. By rewriting, decomposing, or abstracting queries, we can enhance the system's ability to find all the relevant information and generate more comprehensive and accurate responses.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

When dealing with complex queries in RAG systems, simply searching for the exact words in the user's query might not be enough to find all the relevant information. Query translation techniques offer strategies for modifying the query to enhance retrieval effectiveness.

The primary goal of query translation is to improve recall – to increase the chances of retrieving all the documents or chunks that are relevant to the user's query, even if they don't contain the exact words used in the query.

Query translation strategies include query rewriting, query rewriting and abstract query generation.

**Query Rewriting (using LLMs)**

We can use an LLM to rewrite the original query into multiple similar queries with slight modifications in wording or phrasing. This can help address the misalignment problem we discussed earlier, where the user's query might not use the same language as the relevant documents.

**Query Decomposition (Subqueries)**

This involves breaking down a complex query into smaller, more manageable sub-queries.

Chapter 4 Example: The QueryEnhancer module we implemented in Chapter 4 used this strategy to generate sub-queries for complex user questions.

This approach is particularly effective for handling complex queries that involve multiple concepts or sub-questions.

**Abstract Query Generation**

This technique involves converting the original query into a more abstract, high-level query.

The system retrieves information for the abstract query, generates an abstract response, and then uses this abstract information along with the retrieved documents to reason about the original query.

This method can be useful when factual accuracy is paramount, as the abstract reasoning step can help ensure the final response is consistent with the retrieved information.

  

**Example of a Query Decomposition (Subqueries)** 

One approach to using sub-queries is sequential retrieval:

1. Identify Sub-Problems: An LLM is used to determine the intermediate sub-problems that need to be solved to answer the main question.
2. Sequential Retrieval and Response Generation: The system retrieves information and generates an answer for one sub-problem at a time.
3. Combining Intermediate Answers: The answers to the sub-problems are then used to construct the final response to the main question.

![[2024-12-12 at 08.11.43@2x.png]]
![[2024-12-12 at 08.12.40@2x.png]]

### Retrieve with CoT

**TLDR:** Retrieval with chain-of-thought reasoning is a powerful technique for handling complex QA tasks in RAG systems. It allows the system to perform step-by-step reasoning, guided by retrieved information, to arrive at a comprehensive and accurate answer. By exploring different variations and levels of complexity, you can tailor this approach to the specific requirements of your RAG application.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

For complex question-answering (QA) tasks, especially those that require multi-step reasoning or involve finding information from multiple sources, combining retrieval with chain-of-thought reasoning can be very effective.

This technique differs from simple query decomposition in that the reasoning steps are not generated upfront. Instead, the system iteratively retrieves information and performs reasoning based on the retrieved context.

Here's a typical process:

- Initial Retrieval: The system first retrieves relevant documents or chunks based on the initial user query.
- CoT Prompting: The LLM is then prompted with the query and the retrieved context, and it's instructed to generate a reasoning sentence (T1) that represents an intermediate step towards finding the answer.
- Retrieval for Reasoning Step: The system retrieves new documents or chunks relevant to the reasoning sentence (T1).
- Loop Continuation: Steps 2 and 3 are repeated, generating new reasoning sentences (T2, T3, etc.) and retrieving corresponding information until a termination condition is met.
- Termination Condition: The loop typically terminates when the system finds the answer to the original query within the retrieved context. This could be determined by checking if the answer is a substring of the retrieved text or by using other criteria.

  

**Example:**

User Query: "What are the advantages of using Weights & Biases for experiment tracking compared to using a spreadsheet?"

Steps:

1. Initial Retrieval: Retrieve documents related to Weights & Biases and experiment tracking.
2. T1 (Reasoning): "Weights & Biases offers automatic logging of experiment data, while spreadsheets require manual entry."
3. Retrieve for T1: Find documents about automatic logging and manual data entry.
4. T2 (Reasoning): "Automatic logging saves time and reduces errors compared to manual entry."
5. Retrieve for T2: Find documents discussing the benefits of automatic logging.
6. Termination: The retrieved documents likely contain information about the advantages of Weights & Biases (e.g., time-saving, error reduction), so the loop terminates.

  

**Complexities and Variations:**

- Number of Reasoning Steps: The complexity can be adjusted by controlling the number of reasoning steps allowed before termination.
- Types of Reasoning: The reasoning steps can involve different types of logic or inference, depending on the task.
- Retrieval Methods: Different retrieval methods (e.g., dense retrieval, keyword-based retrieval) can be used within the loop.
![[2024-12-12 at 08.13.22@2x.png]]

### Metadata filtering

**TLDR:** Metadata filtering is a valuable technique for enhancing retrieval in RAG systems. It allows you to leverage the rich contextual information provided by metadata to refine the retrieval process and ensure that the LLM receives the most relevant information to generate accurate and helpful responses.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb)

Metadata filtering is a powerful technique for enhancing the retrieval process in RAG systems, especially when dealing with queries that have specific contextual requirements.

As discussed in Chapter 3, we can enrich our vector store by not only storing documents and their embeddings but also associating relevant metadata with each document. This metadata can include information like the document's source, topic, date, author, or any other relevant attributes.

Here is what a metadata filtering process looks like.

**1. Metadata Extraction (using LLM):**

We use an LLM to extract relevant metadata from the user's query. To guide the LLM, we provide a predefined metadata schema that specifies the types of metadata we want to extract.

Example: In the provided example, the LLM is instructed to extract the "error" metadata from the query. This might involve identifying error codes, error messages, or other information related to specific errors.

**2. Filtering the Vector Store:**

Once we have the extracted metadata, we use it to filter the vector store. We select only the documents or chunks whose metadata matches the extracted metadata.

**3. Cosine Similarity Search:**

We then perform the usual cosine similarity search, but only on the filtered subset of documents. This ensures that the retrieved context is more focused and relevant to the specific aspects of the query indicated by the metadata.

  

**Example:**

1. User Query: "I'm getting error code 12345 when trying to log in. What does it mean?"

2. Metadata Extraction: The LLM extracts the error code "12345" as the relevant metadata.

3. Filtering: The vector store is filtered to select documents or chunks that mention or are associated with error code 12345.

4. Retrieval: The cosine similarity search is performed on the filtered set, returning documents or chunks that are more likely to contain information about that specific error code.

  

The benefits of metadata filtering are:

- Enhanced Retrieval Relevance: By narrowing down the search space based on metadata, we can significantly improve the relevance of the retrieved information.
- More Accurate Responses: Providing the LLM with a more focused and relevant context leads to more accurate and helpful responses.
- Efficient Retrieval: Filtering the vector store before performing the similarity search can also improve retrieval efficiency.

![[2024-12-12 at 08.14.31@2x.png]]


### Logical routing

**TLDR:** Routing is an essential technique for RAG systems that need to access information from multiple data sources. By leveraging LLMs and employing a clear reasoning process, we can create intelligent routing mechanisms that efficiently direct queries to the most appropriate sources, improving the accuracy, comprehensiveness, and relevance of the retrieved information.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)
- [Let Me Speak Freely? A Study on the Impact of Format Restrictions on Performance of Large Language Models](https://arxiv.org/abs/2408.02442)

  

In many real-world RAG applications, you'll likely have multiple sources of information that could be relevant to a user's query. These sources might include:

- Multiple Vector Stores: You might have separate vector stores for different types of documents (e.g., internal documentation, product specifications, customer reviews).
- SQL Databases: Structured data stored in relational databases can also be valuable for answering certain types of questions.
- Web Search Results: Accessing external knowledge through web search can provide a broader range of information.

Routing is a technique for directing the user's query to the most appropriate data source(s), ensuring we retrieve the most relevant and comprehensive information. We can implement intelligent routing by leveraging the power of LLMs with function-calling capabilities.

1. Query Analysis: The LLM analyzes the user's query to understand its intent and the type of information required.
2. Reasoning Step: Ideally, we use a separate LLM call to generate a reasoning step that explains why a particular data source is chosen.  
    Example: "The query is asking about recent customer reviews, so we should search the customer review database."
3. Function Calling: Another LLM call uses the reasoning step to execute a function that retrieves information from the selected data source(s).

A recent [study](https://arxiv.org/abs/2408.02442) suggests that using separate LLM calls for the reasoning step and the function calling step can lead to better performance and more reliable routing decisions. This separation helps to:

- Improve Clarity and Focus: Each LLM call has a specific and well-defined task.
- Reduce Bias: The reasoning step is less likely to be biased towards a particular data source.
- Enhance Transparency: The reasoning step provides a clear explanation of the routing decision, making it easier to understand and debug the system's behavior.

  

**Example**:

1. User Query: "What are customers saying about the latest version of our product?"
2. Reasoning (LLM Call 1): "The user is asking for opinions and feedback, so we should search the customer review vector store."
3. Function Calling (LLM Call 2): Execute a function to retrieve relevant reviews from the customer review vector store.
![[2024-12-12 at 08.14.55@2x.png]]

![[2024-12-12 at 08.15.24@2x.png]]
### Context stuffing

**TLDR:** The position of relevant context within the retrieved set significantly impacts the LLM's ability to generate accurate and complete responses. Simply relying on cosine similarity ranking might not be enough. We need techniques like reranking to prioritize the most relevant information and mitigate the "lost in the middle" problem, ensuring the LLM has access to the crucial context it needs.

**L****inks:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)
- [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/pdf/2307.03172)

  ![[2024-12-12 at 08.16.46@2x.png]]

The order in which we present retrieved information to the LLM significantly impacts the quality of the generated response. Simply retrieving the top-k most similar documents based on cosine similarity might not be enough, especially if relevant information is buried in lower-ranked results.

While retrieving more documents, by increasing the value of 'k', generally leads to higher recall and a greater chance of including all relevant information, we must consider the limitations of LLMs. LLMs have a finite context window, a maximum amount of text they can process at once. As we increase the number of retrieved documents, the context length grows, potentially exceeding the LLM's capacity.  Therefore, we face a trade-off:  retrieving enough documents to ensure high recall while keeping the context length manageable for the LLM to process effectively. 

  

**The "Lost in the Middle" Problem**

[Research](https://arxiv.org/pdf/2307.03172) has shown that LLMs tend to struggle with accessing relevant information when it's located in the middle of long contexts. This is known as the "lost in the middle" problem.

The "Lost in the Middle" paper demonstrated this phenomenon through a control study. They varied the position of the most relevant document within a set of retrieved results and observed how it affected the LLM's performance. The LLM performed best when the relevant information was placed at the beginning or the end of the context. Performance significantly degraded when the relevant document was in the middle of a long context.

**Implications for RAG Systems:**

In the example provided, even though we retrieved the top 10 documents, two of the relevant pieces of information were located in the middle of the retrieved set. This means the LLM might struggle to access and utilize this crucial information effectively, potentially impacting the quality of the generated response.

**Addressing the "Lost in the Middle" Problem:**

We'll explore techniques for addressing this problem, such as reranking, in the following sections of the chapter. Reranking allows us to reorder the retrieved results based on additional signals or models, ensuring that the most relevant information is presented to the LLM in a more prominent position.

![[2024-12-12 at 08.17.05@2x.png]]

### Cross encoder

**TLDR:** Cross-encoder transformers provide a powerful mechanism for reranking retrieved documents in RAG systems. By learning to score the relevance of query-document pairs, they can prioritize the most relevant information and mitigate the "lost in the middle" problem. However, the computational cost of reranking should be considered when choosing the initial number of documents to retrieve.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

To address the limitations of simple cosine similarity ranking and the "lost in the middle" problem, we can use reranking techniques. One powerful approach to reranking involves using a cross-encoder transformer model.

**Cross-Encoder Transformers for Reranking:**

- Pairwise Comparison: Cross-encoder transformers are specifically designed to compare pairs of text sequences. In the context of reranking, we pass pairs of the user query and each retrieved document to the cross-encoder.
- Training for Relevance: We train the cross-encoder to learn how to assign a relevancy score to each pair. This training often involves using a dataset of query-document pairs labeled with their relevance.
- BERT as a Foundation: Popular transformer models like BERT are often used as the basis for cross-encoders because they are effective at capturing contextual relationships and semantic similarities between text sequences.

**Reranking Process:**

1. Initial Retrieval: We first retrieve a set of documents using a standard retrieval method (e.g., cosine similarity search).
2. Cross-Encoder Scoring: For each retrieved document, we create a pair with the user query and pass this pair through the cross-encoder. The cross-encoder assigns a relevance score to each pair.
3. Reordering: We then reorder the retrieved documents based on their new relevance scores, with the highest-scoring documents ranked first.

**Latency Considerations:**

- Reranking with a cross-encoder can be computationally expensive, especially if we're retrieving a large number of documents initially. Therefore, it's important to be mindful of the initial top-k parameter used in the retrieval step.
- Balancing Recall and Speed: A smaller top-k value will result in faster reranking but might sacrifice recall.
- Optimal top-k: Finding the optimal top-k value often involves balancing the need for high recall with the need for reasonable latency.
![[2024-12-12 at 08.18.13@2x.png]]

### Notebook 5: retrieval and reranking

**TLDR:** Reranking is a valuable technique for enhancing retrieval quality in RAG systems. By using a powerful reranker like the Cohere Reranker, you can improve the ranking of retrieved documents, leading to a better balance between precision and recall and ultimately a more effective RAG application.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

In this hands-on session, we're demonstrating the power of reranking to improve the accuracy and relevance of information retrieval in RAG systems. We've implemented two retrieval systems: a basic dense retriever using Cohere's embedding model and a more advanced system that combines dense retrieval with the Cohere Reranker. Both systems are evaluated using the same set of metrics (Hit Rate, MRR, NDCG, MAP, and F1 score) to provide a direct comparison of their performance. We use Weights & Biases Weave to manage the evaluation process and visualize the results.

The evaluation results clearly show the benefits of incorporating reranking into the retrieval pipeline. The dense retriever with the [Cohere Reranker](https://cohere.com/rerank?utm_source=course&utm_medium=course&utm_campaign=rag_course) consistently outperforms the basic dense retriever across most metrics, particularly in terms of ranking accuracy (Hit Rate and MRR) and the balance between precision and recall (F1 score). This demonstrates that reranking effectively prioritizes the most relevant documents, leading to more accurate and informative responses from the RAG system. The comparison highlights the value of incorporating advanced retrieval techniques like reranking to enhance the performance and effectiveness of RAG applications.


### Reciprocal rank fusion

**TLDR:** Rank fusion is a valuable technique for efficiently combining retrieval results from multiple sources in RAG systems. It offers a faster alternative to reranking while still improving the overall relevance of the retrieved information. This approach helps to enhance recall and provides a more comprehensive set of results for the LLM to process, leading to more accurate and informative responses.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

When retrieving information from multiple sources, reranking all the retrieved chunks using a cross-encoder can add significant latency to the RAG system. Rank fusion provides a simpler and more efficient way to combine results from different sources while still improving the relevance of the retrieved information.

**How Rank Fusion Works:**

1. Retrieve from Multiple Sources: The system performs retrieval from multiple data sources, each potentially using different retrieval methods or focusing on different aspects of the knowledge base.
2. Identify Unique Documents: The retrieved results from all sources are combined, and any duplicate or redundant documents are identified.
3. Aggregate Ranks: For each unique document, the system aggregates its ranks from the different retrieval sources into a unified or fused rank. This aggregation can be done using various methods, such as taking the average rank, the highest rank, or a weighted combination of ranks.
4. Order by Fused Rank: The unique documents are then sorted in descending order based on their fused ranks.
5. Select Top-N: The top-N documents from this sorted list are selected as the final retrieved results.

  

**Benefits of Rank Fusion:**

- Reduced Latency: Rank fusion is generally faster than reranking with a cross-encoder, especially when dealing with a large number of retrieved documents from multiple sources.
- Improved Recall: By considering results from multiple sources, rank fusion can enhance the recall of the system, increasing the chances of finding all relevant information.
- Flexibility: Rank fusion allows for flexibility in how ranks are aggregated, allowing you to prioritize certain sources or retrieval methods based on your specific needs.

![[2024-12-12 at 08.20.53@2x.png]]

### Hybrid retriever

**TLDR:** Hybrid retrieval is a powerful technique for enhancing RAG system performance. It allows you to combine the strengths of different retrieval methods to create a more robust and accurate system. However, the trade-off between performance gains and latency should be carefully considered, especially in applications where response time is critical.

**Links:** 

- Chapter [notebook](https://github.com/wandb/edu/blob/main/rag-advanced/notebooks/Chapter05.ipynb) 
- Weights & Biases Weave [Documentation](https://weave-docs.wandb.ai/?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Wandbot [repo](https://github.com/wandb/wandbot)
- LLM-friendly [resources](https://github.com/wandb/edu/tree/main/rag-advanced/resources)

  

In this hands-on session, we're exploring the power of hybrid retrieval, where we combine multiple retrieval methods to enhance the overall retrieval performance of our RAG system.

**Hybrid Retriever Implementation:**

1. Combining BM25 and Dense Retrieval: The _HybridRetrieverReranker_ class combines both the BM25 retriever (which performs well on keyword matching) and the dense retriever (which captures semantic relationships).
2. Reciprocal Rank Fusion: This specific rank fusion technique is used to aggregate the ranks of documents retrieved by both methods.
3. Cohere Reranker: After rank fusion, the Cohere Reranker is used to reorder the results and select the top-N documents to pass to the LLM.

  

**Evaluation and Comparison:**

We use Weave Evaluation to assess the performance of the hybrid retriever and compare it to the dense retriever (both with and without reranking) using the same set of metrics. The Weave dashboard provides a clear visualization of the performance differences.

  

**Results:**

The evaluation results demonstrate the effectiveness of the hybrid retrieval approach:

- Higher Hit Rate: The hybrid retriever achieved a significantly higher hit rate (60%) compared to both the dense retriever (31%) and the dense retriever with reranking (48%). This indicates that the hybrid approach is much better at finding at least one relevant document for the given queries.
- Improved F1 Score: The hybrid retriever also surpassed both other retrieval systems in terms of F1 score, indicating a better balance between precision and recall.
- Higher Latency: As expected, the hybrid retriever had higher latency due to the additional processing steps involved in combining multiple retrieval methods and reranking.

**Conclusion:**

The hybrid retriever, by combining the strengths of BM25 and dense retrieval with a reranking step, effectively leverages the benefits of each method while mitigating their individual weaknesses. The evaluation results demonstrate that this approach can lead to significant improvements in retrieval accuracy and relevance, albeit at the cost of increased latency.

### Weaviate Vector Database

**TLDR:** Weaviate provides a powerful and scalable platform for building production-ready RAG applications. Its integration with Cohere's APIs, its efficient handling of unstructured data, and the convenience of Weaviate Cloud simplify the development and deployment process, allowing you to focus on building a high-quality RAG experience for your users.

**Links**: 

- Weaviate Cloud [documentation](https://weaviate.io/developers/wcs?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Weaviate quickstart [notebook](https://colab.research.google.com/github/weaviate-tutorials/quickstart/blob/main/quickstart_end_to_end.ipynb)
- Weaviate + Cohere integration [docs](https://weaviate.io/developers/weaviate/model-providers/cohere#integrations-with-cohere)
- Weaviate + Weights & Biases integration [docs](https://weaviate.io/developers/integrations/operations/wandb)

  

Hey, it is [Charles](https://www.linkedin.com/in/charles-pierse/) from [Weaviate](https://weaviate.io/?utm_source=course&utm_medium=course&utm_campaign=rag_course)! I want to introduce you to building production-ready RAG applications using Weaviate, a vector database specifically designed for AI-powered applications.

Weaviate offers several advantages for building production-scale RAG systems:

- Optimized Vector Storage and Querying: Weaviate is optimized for storing and querying large numbers of vector embeddings, enabling fast and efficient retrieval of similar objects.
- Unstructured Data Handling: It excels at handling unstructured data like text, making it well-suited for RAG applications that often deal with large text-based knowledge bases.
- AI-Native Ecosystem: Weaviate provides a rich ecosystem of tools, integrations, and services that support the development of AI-powered applications, particularly those that rely on similarity search.

Using [Weaviate Cloud](https://weaviate.io/developers/wcs?utm_source=course&utm_medium=course&utm_campaign=rag_course) simplifies the setup and deployment process, as it handles hosting and infrastructure management, allowing developers to focus on building the application logic.Weaviate seamlessly integrates with Cohere's APIs.

**Setting Up Weaviate:**

1. Import Libraries: We start by importing the Weaviate Python client and the Weave library.
2. Connect to Weaviate Cloud: We use our Weaviate Cloud URL and API key to connect to the cloud instance.
3. Fetch Data: We retrieve the pre-processed dataset from Weave, which we prepared in previous chapters.
4. Create a Collection: We define a new collection in Weaviate to store our data. We specify the collection name, properties (fields) of the data, their data types, and the configuration for the vectorizer and reranker. In this case, we're using Cohere's embedding model as the vectorizer and Cohere's Reranker for reranking.
5. Import Data: We use Weaviate's optimized batch API to efficiently import the data into the collection. The Cohere vectorizer automatically generates embeddings for the data during the import process.
![[2024-12-12 at 08.22.57@2x.png]]

### Weaviate Hybrid Search

**TLDR:** Hybrid search in Weaviate combines the strengths of semantic and keyword-based retrieval, giving you control over the balance between precision and recall. By incorporating Cohere's Reranker, you can further enhance retrieval accuracy, especially for complex queries, ensuring that your RAG application delivers the most relevant and informative results.

**Links:**

- Weaviate hybrid search [docs](https://weaviate.io/developers/weaviate/search/hybrid)
- Weaviate Cloud [documentation](https://weaviate.io/developers/wcs?utm_source=course&utm_medium=course&utm_campaign=rag_course) 
- Weaviate quickstart [notebook](https://colab.research.google.com/github/weaviate-tutorials/quickstart/blob/main/quickstart_end_to_end.ipynb)
- Weaviate + Cohere integration [docs](https://weaviate.io/developers/weaviate/model-providers/cohere#integrations-with-cohere)
- Weaviate + Weights & Biases integration [docs](https://weaviate.io/developers/integrations/operations/wandb) 

  

Let me show you how powerful hybrid search and reranking can be when building effective RAG applications in Weaviate! I'll explain why pure vector search, while great for capturing semantic meaning, sometimes misses the mark, especially when dealing with very specific domain terms. That's where hybrid search comes in. By combining vector search with traditional keyword search (we use BM25 in Weaviate), we get a much more comprehensive and robust retrieval system. 

[Weaviate's hybrid search](https://weaviate.io/hybrid-search?utm_source=course&utm_medium=course&utm_campaign=rag_course) engine runs both BM25 and vector search in parallel, then cleverly merges the results using a weighted system controlled by what we call the "alpha parameter." I'll show you how adjusting this parameter lets you fine-tune the balance between keyword matching and semantic similarity – giving you the control to prioritize either precision or recall based on your application's needs.

Now, let's talk about reranking. Using Cohere's Reranker, we can significantly improve results, especially for those tricky, complex queries that even a hybrid search might struggle with. I'll use a real example - a question about setting up parallel sweeps with Weights & Biases agents on multiple GPUs. You'll see how the initial hybrid search results aren't quite right. But, with the magic of the Cohere Reranker, we can reorder the results, putting the most relevant document right at the top! This demonstrates how rerankers can understand the nuances of a complex query and re-contextualize the retrieved documents to deliver the most accurate and relevant information. 

With these techniques, you'll be well-equipped to build powerful RAG applications in Weaviate that can handle even the most challenging search requests.

![[2024-12-12 at 08.27.15@2x.png]]
![[2024-12-12 at 08.28.25@2x.png]]

![[2024-12-12 at 08.28.50@2x.png]]

### Conclusion
![[2024-12-12 at 08.32.55@2x.png]]
**Key Takeaways:**

**No One-Size-Fits-All Solution:** There is no single "best" retrieval technique that works for every situation. The optimal approach depends on the specific characteristics of your data, the complexity of your queries, and your performance requirements.

**Experimentation and Evaluation are Crucial:** It's essential to experiment with different retrieval techniques and rigorously evaluate their performance using appropriate metrics.

**Handling Complex Queries:** For complex queries, consider using techniques like:

- Subquery Decomposition: Breaking down the query into smaller, more manageable sub-queries.
- Query Rewriting: Rephrasing the query to improve the chances of finding relevant information (recall).

**Leveraging Metadata:** Metadata filtering can help to:

- Speed up retrieval time by narrowing down the search space.
- Enforce the selection of correct information by filtering based on relevant attributes.

**Multiple Retrieval Sources:** Don't be afraid to use multiple vector databases or different retrieval algorithms to capture a wider range of information.

**Reranking and Rank Fusion:**

- Reranking: You can use a reranker (like Cohere's Reranker) to reorder the retrieved results from multiple sources, prioritizing the most relevant items. However, this can be computationally expensive.
- Reciprocal Rank Fusion: This offers a faster alternative for combining results from multiple retrievers. You can then apply Cohere's Reranker to further refine the fused results.

By experimenting with these techniques, evaluating their performance, and finding the right combination for your RAG system, you can significantly improve the accuracy, relevance, and efficiency of your retrieval process.