## RAG Evaluation Program
### Overview
This program evaluates a Retrieval-Augmented Generation (RAG) system by assessing the quality of both the retrieval and generation stages. RAG is an important approach in natural language processing (NLP) where information retrieval techniques are combined with language generation models to produce responses based on external knowledge. This program uses various metrics to evaluate each stage of RAG, providing insights into relevance, factual consistency, fluency, coverage, and retrieval accuracy.

### Evaluation Metrics
This RAG evaluation program uses the following metrics:

**Relevance:** Measures the similarity between the query and the retrieved context. We use cosine similarity between embeddings generated by a SentenceTransformer model to evaluate the degree of relevance of the retrieved documents.

**Factual Consistency:** Ensures the generated response accurately reflects the information within the retrieved context. Using a Natural Language Inference (NLI) model, we calculate the probability that the generated response is logically entailed by the context. Higher entailment probability indicates higher consistency.

**Fluency (Perplexity):** Assesses the linguistic quality of the generated response by measuring how natural or "fluent" the language is. We use a language model (GPT-2) to compute the perplexity of the generated response, where a lower perplexity score implies greater fluency.

**Coverage:** Indicates whether the generated response adequately covers the query's requirements. Coverage is calculated using the NLI model, where the entailment score between the query and response serves as the coverage score. A high entailment score reflects good coverage.

**Retrieval Accuracy:**
Mean Reciprocal Rank (MRR): Measures how well the relevant documents are ranked. This is computed by taking the inverse of the rank of the first relevant document, then averaging over queries. A higher MRR score signifies more accurate retrieval.
Mean Average Precision (MAP): Averages the precision scores at each relevant document's rank. This helps evaluate the spread of relevant documents within the ranked list, with higher MAP values reflecting better distribution.

#### Program Structure
**Context Retrieval:** Using a SentenceTransformer model, the program retrieves relevant documents based on the query. The retrieved documents serve as the "context" for the generation stage.
**Response Generation:** With the retrieved context, the program generates a response using a text-generation model (GPT-2).
**Metric Evaluation:** Each metric is computed based on the query, context, and generated response. For retrieval accuracy metrics (MRR and MAP), the rank positions of relevant documents within the entire knowledge base are analyzed.
#### Requirements
Install the following packages:
   * pip install sentence-transformers transformers sklearn numpy

### How to Use
Define your knowledge base in the format used within the program.
Customize the query variable with the text you want to evaluate.
Run the program to see detailed logging for each metric. The program will output relevance, factual consistency, fluency (perplexity), coverage, and retrieval accuracy scores for the query.
### Code Explanation
Each function in the code performs a specific part of the RAG evaluation:

**retrieve_context(query)**: Retrieves relevant documents based on cosine similarity between query and document embeddings.
**generate_response(query, context)**: Generates a response using the context retrieved for the query.
**evaluate_relevance(query, context)**: Measures relevance using cosine similarity between the query and retrieved contexts.
**evaluate_factual_consistency(response, context)**: Calculates factual consistency using an NLI model to check entailment between response and context.
**evaluate_fluency(response)**: Uses perplexity (from GPT-2) to evaluate response fluency.
**evaluate_coverage(query, response)**: Computes coverage by using NLI entailment scores between the query and response.
**evaluate_retrieval_accuracy(query, context)**: Calculates retrieval accuracy through MRR and MAP scores based on the ranks of retrieved documents.
### Logging
Logging is configured to record and output each metric’s score to assist with tracking performance across multiple queries. Loggers will display values for relevance, factual consistency, fluency, coverage, and retrieval accuracy (MRR and MAP) directly in the console.

Example Output
Below is an example of the logging output for a sample query:


Relevance: 0.6143321990966797
Factual_consistency: 0.024692179635167122
Fluency: 881.6091098568681
Coverage: 0.0027736832853406668
Retrieval_accuracy: {'MRR': 1.0, 'MAP': 1.0}
These scores help provide a detailed overview of the performance of the RAG system on the given query, allowing for a well-rounded evaluation of both retrieval and generation quality.

### Conclusion
This program provides a comprehensive framework for RAG evaluation, with a modular design that allows easy customization of the evaluation metrics, knowledge base, and models. The metrics chosen ensure a balanced assessment across relevance, consistency, fluency, coverage, and retrieval accuracy, which are essential for robust RAG performance.
