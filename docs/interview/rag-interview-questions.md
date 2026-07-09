# RAG Interview Questions and Answers

## Overview

This document covers Retrieval Augmented Generation (RAG) interview questions for mid-senior AI Engineer roles.

Topics:

- RAG architecture
- Document ingestion
- Chunking
- Embeddings
- Retrieval
- Vector databases
- Re-ranking
- Hybrid search
- Evaluation
- Production challenges
- System design

---

# 1. What is RAG?

## Short Answer

Retrieval Augmented Generation (RAG) is an architecture that combines information retrieval with LLM generation. Instead of relying only on the model's internal knowledge, the system retrieves relevant external information and provides it as context to generate more accurate responses.

---

## Architecture

```
User Query

↓

Query Processing

↓

Retriever

↓

Relevant Documents

↓

Context + Query

↓

LLM

↓

Generated Answer
```

---

## Why Use RAG?

RAG helps with:

- Reducing hallucinations
- Using private enterprise data
- Keeping knowledge up to date
- Providing source grounding

Examples:

- Customer support assistant
- Internal knowledge assistant
- Developer assistant
- Document analysis

---

# 2. Explain a Production RAG Pipeline

## Short Answer

A production RAG system has two major pipelines:

1. Offline ingestion pipeline
2. Online retrieval pipeline

---

## Offline Pipeline

```
Documents

↓

Parsing

↓

Cleaning

↓

Chunking

↓

Embedding Generation

↓

Vector Database
```

---

## Online Pipeline

```
User Query

↓

Query Embedding

↓

Similarity Search

↓

Re-ranking

↓

Context Assembly

↓

LLM Generation

↓

Response
```

---

# 3. Explain the Difference Between Retrieval and Generation

## Short Answer

Retrieval finds relevant information. Generation uses the retrieved information to create a natural language response.

---

Example:

Retrieval:

```
Find customer refund policy document
```

Generation:

```
Explain refund policy to customer
```

---

# 4. How Does Chunking Work in RAG?

## Short Answer

Chunking divides large documents into smaller pieces that can be embedded and retrieved effectively.

---

Example:

Large document:

```
100-page employee handbook
```

After chunking:

```
Chunk 1: Benefits

Chunk 2: Leave policy

Chunk 3: Security policy
```

---

# 5. What Are Common Chunking Strategies?

## Fixed Size Chunking

Example:

```
Every 500 tokens
```

Advantages:

- Simple
- Predictable

Disadvantages:

- May split important information

---

## Recursive Chunking

Splits based on:

- Paragraphs
- Sentences
- Sections

Better for documents.

---

## Semantic Chunking

Uses meaning to determine boundaries.

Advantages:

- Better context preservation

Disadvantages:

- More expensive

---

# 6. How Do You Select Chunk Size?

## Short Answer

Chunk size depends on document structure, retrieval quality, and model context limits.

---

Trade-off:

Small chunks:

Advantages:

- More precise retrieval

Disadvantages:

- Lose context

---

Large chunks:

Advantages:

- Preserve context

Disadvantages:

- More noise

---

Typical approach:

```
300-1000 tokens
```

with overlap.

---

# 7. Why Do We Need Embeddings in RAG?

## Short Answer

Embeddings convert text into numerical vectors that capture semantic meaning, allowing similarity search.

---

Example:

Queries:

```
"How do I reset password?"

"Forgot my login credentials"
```

Different words but similar meaning.

Embeddings identify similarity.

---

# 8. Explain Vector Similarity Search

## Short Answer

Vector similarity search finds documents whose embeddings are closest to the query embedding.

---

Common metrics:

## Cosine Similarity

Measures angle between vectors.

```
similarity = A.B / ||A|| ||B||
```

---

## Euclidean Distance

Measures vector distance.

---

# 9. What Is a Vector Database?

## Short Answer

A vector database stores embeddings and provides efficient similarity search.

---

Examples:

- Pinecone
- Milvus
- Weaviate
- Chroma
- pgvector

---

Features:

- Vector indexing
- Metadata filtering
- Similarity search
- Scalability

---

# 10. Explain Retrieval Strategies

## Dense Retrieval

Uses embeddings.

Example:

```
Query embedding

↓

Vector similarity search
```

Advantages:

- Understands meaning

---

## Sparse Retrieval

Uses keyword matching.

Example:

- BM25

Advantages:

- Good exact matching

---

## Hybrid Retrieval

Combines:

```
Dense Retrieval

+

Keyword Search
```

Often performs better in enterprise systems.

---

# 11. What Is Re-ranking?

## Short Answer

Re-ranking improves retrieval quality by applying a more powerful model after initial retrieval.

---

Flow:

```
Query

↓

Vector Search

↓

Top 50 documents

↓

Re-ranker

↓

Top 5 documents

↓

LLM
```

---

Why?

Vector search is fast but approximate.

Re-ranking improves precision.

---

# 12. How Do You Improve Poor RAG Retrieval?

## Answer

I would investigate multiple areas:

### 1. Document Quality

- Remove duplicate content
- Improve parsing
- Add metadata

---

### 2. Chunking

- Adjust chunk size
- Add overlap
- Use semantic chunking

---

### 3. Retrieval

- Improve embeddings
- Add hybrid search
- Add re-ranking

---

### 4. Query Processing

- Query rewriting
- Query expansion

---

# 13. What Is Query Rewriting?

## Short Answer

Query rewriting transforms user queries into better retrieval queries.

---

Example:

User:

```
Why is my payment broken?
```

Rewrite:

```
Find payment failure troubleshooting documentation and error codes.
```

---

Benefits:

- Better retrieval accuracy
- Handles vague questions

---

# 14. How Do You Reduce Hallucination in RAG?

## Answer

I use multiple strategies:

1. Better retrieval
2. Limit model context to retrieved sources
3. Add citations
4. Use confidence thresholds
5. Add guardrails
6. Evaluate answer quality

---

Example instruction:

```
Answer only using provided context.
If information is missing, say you don't know.
```

---

# 15. How Do You Evaluate RAG Systems?

## Short Answer

RAG evaluation requires measuring both retrieval quality and generation quality.

---

## Retrieval Metrics

### Recall

Did we retrieve the correct documents?

---

### Precision

Were retrieved documents relevant?

---

## Generation Metrics

Measure:

- Answer correctness
- Faithfulness
- Relevance
- Completeness

---

## Production Metrics

- Latency
- Cost
- User satisfaction

---

# 16. What Is RAGAS?

## Short Answer

RAGAS is a framework for evaluating RAG pipelines using metrics such as:

- Faithfulness
- Answer relevance
- Context precision
- Context recall

---

# 17. RAG vs Fine-Tuning

## Short Answer

RAG provides external knowledge at runtime. Fine-tuning changes the model behavior through additional training.

---

| RAG | Fine-tuning |
|-|-|
| External knowledge | Model behavior |
| No retraining | Requires training |
| Easy updates | Expensive updates |
| Dynamic data | Stable patterns |

---

Example:

Company policies:

```
RAG
```

Writing style:

```
Fine-tuning
```

---

# 18. When Would You Not Use RAG?

## Answer

I would avoid RAG when:

- Information is already captured by the model
- Task requires reasoning only
- Dataset is too small
- Retrieval does not improve quality

Examples:

- Simple summarization
- Creative writing
- General knowledge questions

---

# 19. How Would You Design Enterprise RAG?

## Architecture

```
                    User

                      |

                 API Gateway

                      |

                Query Service

                      |

        +-------------+-------------+

        |                           |

    Retriever                 User Context

        |

        v

 Vector Database

        |

        v

    Re-ranking

        |

        v

        LLM

        |

   Guardrails

        |

     Response
```

---

Components:

- Document ingestion
- Embedding pipeline
- Vector storage
- Retrieval service
- LLM gateway
- Monitoring
- Evaluation

---

# 20. How Do You Handle Access Control in RAG?

## Short Answer

Security must be applied during retrieval, not after generation.

---

Example:

Bad:

```
Retrieve everything

↓

Filter response
```

---

Good:

```
User permissions

↓

Filtered retrieval

↓

LLM
```

---

Techniques:

- Metadata filtering
- Document permissions
- Tenant isolation
- Audit logging

---

# 21. How Do You Scale RAG?

## Answer

Scaling strategies:

### Retrieval

- Vector indexing
- Sharding
- Caching

### LLM

- Model routing
- Batch processing
- Streaming

### Infrastructure

- Async pipelines
- Load balancing
- Horizontal scaling

---

# 22. RAG Failure Modes

## Poor Retrieval

Cause:

- Bad embeddings
- Wrong chunks

Solution:

- Improve indexing

---

## Hallucination

Cause:

- Missing context

Solution:

- Ground responses

---

## High Latency

Cause:

- Too many retrieval steps

Solution:

- Cache
- Optimize pipeline

---

## High Cost

Cause:

- Large prompts

Solution:

- Reduce context
- Use smaller models

---

# 23. Senior-Level Interview Question

## Design a ChatGPT-like Enterprise Knowledge Assistant

## Answer Framework

Requirements:

```
Users need accurate answers from internal documents.
```

Architecture:

```
Documents

↓

Ingestion Pipeline

↓

Chunking

↓

Embeddings

↓

Vector Database

↓

Retriever

↓

Reranker

↓

LLM

↓

Response
```

Production considerations:

- Authentication
- Permissions
- Evaluation
- Monitoring
- Cost optimization
- Guardrails

---

# 24. Common Follow-up Questions

## Why not store documents directly in the prompt?

Because:

- Context limits
- Higher cost
- More latency

---

## Why use embeddings instead of keyword search?

Because embeddings understand semantic similarity.

---

## Why add re-ranking?

Because first-stage retrieval optimizes speed; re-ranking optimizes accuracy.

---

## How do you know your RAG improved?

Compare:

Before vs After:

- Accuracy
- Retrieval metrics
- User feedback
- Hallucination rate

---

# Key Takeaways

- RAG combines retrieval and generation.
- Chunking and embeddings strongly impact quality.
- Retrieval quality determines answer quality.
- Re-ranking improves precision.
- Evaluation must measure both retrieval and generation.
- Production RAG requires security, monitoring, and cost optimization.
