# AI Engineer Fundamentals - Interview Questions and Answers

## Overview

This document covers fundamental AI/LLM concepts commonly asked in mid-senior AI Engineer interviews.

Topics:

- LLM fundamentals
- Transformer architecture
- Tokens
- Embeddings
- Context windows
- Inference
- Sampling
- Hallucinations
- Fine-tuning
- Prompt engineering
- RAG basics

---

# 1. What is a Large Language Model (LLM)?

## Short Answer

An LLM is a neural network trained on large amounts of text data to understand and generate human-like language. Modern LLMs are typically based on transformer architectures and learn patterns between tokens to predict the next token.

---

## Detailed Answer

LLMs work by:

1. Converting text into tokens
2. Processing tokens through transformer layers
3. Learning relationships using attention mechanisms
4. Predicting the next most likely token

Example:

Input:

```
"The capital of France is"
```

Model predicts:

```
Paris
```

LLMs do not store facts like a database. They learn statistical patterns from training data.

---

# 2. Explain Transformer Architecture

## Short Answer

Transformers are neural network architectures that use self-attention mechanisms to understand relationships between tokens in a sequence. They enable parallel processing and allow models to capture long-range dependencies.

---

## Detailed Answer

A transformer consists of:

```
Input Tokens

↓

Embedding Layer

↓

Self-Attention

↓

Feed Forward Network

↓

Output Prediction
```

Key components:

- Token embeddings
- Positional encoding
- Multi-head attention
- Feed-forward layers
- Layer normalization

The main innovation is self-attention, which allows each token to consider other relevant tokens.

---

# 3. What is Self-Attention?

## Short Answer

Self-attention allows a model to determine how much importance each word should give to other words when processing a sentence.

---

## Example

Sentence:

```
The animal didn't cross the street because it was tired.
```

The model needs to understand:

```
it = animal
```

Self-attention helps connect related words.

---

## Technical Explanation

Each token is converted into:

- Query (Q)
- Key (K)
- Value (V)

Attention calculation:

```
Attention(Q,K,V)

=

softmax(QKᵀ / √d)V
```

The model calculates relationships between tokens and creates contextual representations.

---

# 4. What are Tokens?

## Short Answer

Tokens are the smallest units of text processed by an LLM. They can represent words, parts of words, or characters depending on the tokenizer.

---

## Example

Text:

```
unbelievable
```

Could become:

```
un
believ
able
```

The model processes:

```
[token1, token2, token3]
```

not raw text.

---

## Why Tokens Matter

Tokens affect:

- Cost
- Context length
- Latency
- Model limits

Example:

More tokens:

```
Higher API cost
More computation
```

---

# 5. What are Embeddings?

## Short Answer

Embeddings are numerical representations of text, images, or other data where similar concepts have similar vector representations.

---

## Example

Text:

```
King
Queen
Man
Woman
```

are converted into vectors:

```
[0.23, 0.45, 0.67...]

[0.21, 0.44, 0.69...]
```

Similar meanings have closer vectors.

---

## Applications

Embeddings are used for:

- Semantic search
- RAG
- Recommendations
- Clustering
- Similarity matching

---

# 6. Token vs Embedding Difference

## Short Answer

Tokens represent pieces of text. Embeddings represent the meaning of text as numerical vectors.

---

## Comparison

| Token | Embedding |
|-|-|
| Text representation | Meaning representation |
| Used by LLM input | Used for similarity search |
| Discrete values | Continuous vectors |

---

Example:

```
Text

↓

Tokens

↓

LLM processing

↓

Embeddings
```

---

# 7. What is a Context Window?

## Short Answer

The context window is the maximum number of tokens a model can process in a single request, including input and output.

---

## Example

If a model has:

```
128K token context window
```

It can process:

```
User prompt

+

Conversation history

+

Retrieved documents

+

Generated response
```

within that limit.

---

## Challenges

Large context windows increase:

- Cost
- Latency
- Memory usage

---

# 8. What Happens During LLM Inference?

## Short Answer

Inference is the process of using a trained model to generate output from input tokens.

---

## Flow

```
User Input

↓

Tokenization

↓

Embedding

↓

Transformer Layers

↓

Next Token Prediction

↓

Generated Response
```

The model generates one token at a time.

---

# 9. Explain Next Token Prediction

## Short Answer

LLMs generate text by predicting the probability distribution of the next token based on previous tokens.

---

Example:

Input:

```
The weather today is
```

Model probabilities:

```
sunny: 60%

cloudy: 25%

rainy: 15%
```

The model selects a token based on sampling strategy.

---

# 10. What is Temperature?

## Short Answer

Temperature controls randomness during text generation.

---

Low temperature:

```
0 - 0.3
```

Produces:

- More predictable
- More deterministic answers

---

High temperature:

```
0.7 - 1.0
```

Produces:

- More creative
- More diverse answers

---

# 11. Explain Top-k and Top-p Sampling

## Top-k

Limits token selection to the top K most likely tokens.

Example:

```
Top-k = 10

Only consider top 10 tokens
```

---

## Top-p

Selects tokens whose cumulative probability reaches a threshold.

Example:

```
Top-p = 0.9

Consider tokens covering 90% probability
```

---

# 12. Why Do LLMs Hallucinate?

## Short Answer

LLMs hallucinate because they generate likely text patterns rather than retrieving verified facts.

---

## Causes

- Missing knowledge
- Ambiguous questions
- Poor prompts
- Limited context
- Incorrect retrieval

---

## Reducing Hallucinations

Use:

- RAG
- Better prompts
- Grounding data
- Output validation
- Evaluation systems

---

# 13. What is Prompt Engineering?

## Short Answer

Prompt engineering is the process of designing instructions that guide LLM behavior and improve output quality.

---

## Techniques

### Zero-shot prompting

```
Summarize this article.
```

---

### Few-shot prompting

Provide examples:

```
Example input/output pairs
```

---

### Structured prompting

Define:

- Role
- Context
- Task
- Output format

---

# 14. Fine-Tuning vs Prompt Engineering

## Short Answer

Prompt engineering changes the input instructions. Fine-tuning changes the model weights using additional training data.

---

| Prompt Engineering | Fine-tuning |
|-|-|
| No model changes | Updates model |
| Faster | More expensive |
| Good for behavior changes | Good for specialization |

---

Example:

Prompt:

```
Answer as a financial analyst.
```

Fine-tuning:

```
Train on financial documents.
```

---

# 15. Fine-Tuning vs RAG

## Short Answer

Fine-tuning teaches a model new behavior or style. RAG provides external knowledge dynamically at runtime.

---

Comparison:

| Fine-tuning | RAG |
|-|-|
| Changes model | Keeps model unchanged |
| Training required | Retrieval required |
| Good for behavior | Good for knowledge |

---

# 16. What is RAG?

## Short Answer

Retrieval Augmented Generation combines information retrieval with LLM generation. It retrieves relevant documents and provides them as context to the model.

---

## Architecture

```
User Query

↓

Retriever

↓

Relevant Documents

↓

LLM

↓

Answer
```

---

# 17. Why Use RAG Instead of Fine-Tuning?

## Short Answer

RAG is better when information changes frequently because knowledge can be updated without retraining the model.

---

Examples:

RAG:

```
Company policies
Product documentation
Support articles
```

Fine-tuning:

```
Writing style
Domain behavior
Specific tasks
```

---

# 18. What Are Vector Databases?

## Short Answer

Vector databases store embeddings and allow similarity search based on meaning rather than exact keywords.

---

Examples:

- Pinecone
- Weaviate
- Milvus
- Chroma
- pgvector

---

# 19. What Is a Good LLM Evaluation Strategy?

## Short Answer

LLM evaluation should combine automated metrics, human feedback, and production monitoring.

---

Metrics:

- Accuracy
- Relevance
- Hallucination rate
- Latency
- Cost
- User satisfaction

---

# 20. Explain LLM Application Architecture

## Short Answer

A production LLM application typically contains:

```
User

↓

Application Layer

↓

Prompt Management

↓

Retrieval / Tools

↓

LLM

↓

Validation

↓

Response
```

---

Production components:

- Authentication
- RAG
- Memory
- Guardrails
- Monitoring
- Evaluation

---

# Senior-Level Follow-up Questions

## How would you reduce LLM latency?

Answer:

- Use smaller models
- Cache responses
- Reduce prompt size
- Optimize retrieval
- Use streaming responses
- Use model routing

---

## How would you reduce LLM cost?

Answer:

- Optimize token usage
- Use smaller models where possible
- Cache repeated requests
- Improve prompts
- Route requests intelligently

---

## How do you make an LLM application production-ready?

Answer:

I focus on five areas:

1. Quality - evaluation and grounding
2. Reliability - retries and fallbacks
3. Security - access control and data protection
4. Observability - monitoring and tracing
5. Cost - optimization and model selection

---

# Key Takeaways

- LLMs predict tokens using transformer architectures.
- Attention enables understanding of relationships between tokens.
- Embeddings represent semantic meaning.
- Context windows limit available information.
- RAG improves grounding with external knowledge.
- Fine-tuning changes behavior; RAG changes available knowledge.
- Production AI systems require evaluation, security, monitoring, and cost optimization.
