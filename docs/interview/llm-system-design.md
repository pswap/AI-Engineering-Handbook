# LLM System Design Interview Questions and Answers

## Overview

This document covers LLM system design questions commonly asked in mid-senior AI Engineer interviews.

Topics:

- AI chatbot design
- Enterprise RAG systems
- AI agents
- Coding assistants
- Customer support systems
- Multi-agent platforms
- Scaling
- Reliability
- Security
- Evaluation

---

# System Design Framework for LLM Applications

When designing an LLM system, discuss:

```
1. Requirements

2. High-level architecture

3. Data flow

4. LLM selection

5. Retrieval/tools

6. Storage

7. Evaluation

8. Security

9. Scaling

10. Cost optimization
```

---

# 1. Design an Enterprise AI Chatbot

## Requirements

Build an AI assistant that answers employee questions.

Examples:

- HR policies
- Engineering documentation
- Product information

Requirements:

Functional:

- Answer questions
- Provide citations
- Maintain conversation context

Non-functional:

- Low latency
- Secure access
- High availability

---

# High-Level Architecture

```
                 User

                  |

                  v

            API Gateway

                  |

                  v

          Conversation Service

                  |

        +---------+----------+

        |                    |

        v                    v

    Memory              RAG Pipeline

                             |

                             v

                     Vector Database

                             |

                             v

                           LLM

                             |

                             v

                        Guardrails

                             |

                             v

                         Response
```

---

# Components

## 1. Conversation Service

Responsibilities:

- Manage sessions
- Authentication
- Request routing

---

## 2. Memory Layer

Stores:

- Conversation history
- User preferences
- Previous interactions

---

## 3. RAG Pipeline

Flow:

```
Question

↓

Embedding

↓

Vector Search

↓

Relevant Documents

↓

LLM Context

↓

Answer
```

---

## 4. LLM Layer

Responsibilities:

- Reasoning
- Response generation

Consider:

- Model quality
- Latency
- Cost

---

# Production Considerations

## Security

Implement:

- Authentication
- Authorization
- Document-level permissions
- Data filtering

---

## Evaluation

Measure:

- Answer accuracy
- Retrieval quality
- User satisfaction
- Hallucination rate

---

# 2. Design a RAG-Based Knowledge Assistant

## Problem

Design a system that answers questions from millions of enterprise documents.

---

# Architecture

```
Documents

↓

Ingestion Pipeline

↓

Document Parser

↓

Chunking

↓

Embedding Service

↓

Vector Database


-------------------


User Query

↓

Query Processing

↓

Retriever

↓

Re-ranker

↓

LLM

↓

Answer
```

---

# Ingestion Pipeline

Components:

## Document Processing

Handles:

- PDF
- HTML
- Word documents
- Code repositories

---

## Chunking

Strategies:

- Fixed size
- Recursive
- Semantic

---

## Embedding Service

Converts text:

```
Text

↓

Vector Representation
```

---

# Retrieval Layer

Steps:

```
Query

↓

Embedding

↓

Similarity Search

↓

Top K Results

↓

Re-ranking

↓

Final Context
```

---

# Scaling Considerations

For millions of documents:

Use:

- Distributed vector database
- Metadata filtering
- Index optimization
- Async ingestion

---

# 3. Design an AI Customer Support System

## Requirements

Build an AI system that handles customer issues.

Capabilities:

- Answer questions
- Check order status
- Process requests
- Escalate to humans

---

# Architecture

```
Customer

↓

Chat Interface

↓

Intent Classifier

↓

Supervisor Agent

       |

+------+-------+

|              |

FAQ Agent   Action Agent

               |

               v

          Business APIs

               |

               v

          Customer System
```

---

# Agent Design

## FAQ Agent

Uses:

- RAG
- Documentation

---

## Action Agent

Uses:

- APIs
- Tools

Example:

```
Check order status

↓

Order API
```

---

## Human Escalation

Trigger when:

- Low confidence
- Sensitive issue
- Customer request

---

# 4. Design an AI Coding Assistant

## Requirements

Build an assistant that helps developers write and debug code.

---

# Architecture

```
Developer

↓

IDE Plugin

↓

AI Assistant Service

       |

+------+-------+

|              |

Code RAG    Agent

|              |

Repository   Tools

               |

               v

          Build/Test Systems
```

---

# Components

## Code Retrieval

Indexes:

- Source code
- Documentation
- APIs

---

## Agent

Capabilities:

- Understand code
- Modify files
- Run tests

---

## Tools

Examples:

- GitHub
- Build system
- Testing framework

---

# Challenges

## Context Management

Codebases are large.

Solutions:

- Code chunking
- Semantic retrieval
- Context ranking

---

# 5. Design a Multi-Agent Research Assistant

## Requirements

Build an AI assistant that researches topics and creates reports.

---

# Architecture

```
User

↓

Supervisor Agent

        |

+-------+-------+-------+

|       |       |       |

Search  Data  Analysis  Writer

Agent   Agent Agent     Agent

        |

        v

      Final Report
```

---

# Agent Responsibilities

## Supervisor

- Planning
- Routing
- Coordination

---

## Search Agent

Uses:

- Web search
- RAG

---

## Analysis Agent

Uses:

- Data processing
- Reasoning

---

## Writer Agent

Creates:

- Final report
- Summary

---

# 6. Design an AI Travel Assistant

## Requirements

User wants:

- Flights
- Hotels
- Itinerary

---

# Architecture

```
User

↓

Travel Supervisor Agent

        |

+-------+-------+-------+

|       |       |       |

Flight Hotel  Activity

Agent  Agent  Agent

        |

        v

External APIs

        |

        v

Final Itinerary
```

---

# Agent Flow

Example:

User:

```
Plan a trip to Japan
```

Supervisor:

```
1. Find flights

2. Find hotels

3. Create itinerary

4. Optimize schedule
```

---

# 7. Design an Enterprise AI Agent Platform

## Requirements

Create a platform where teams can build AI agents.

---

# Architecture

```
                    Users

                      |

                API Gateway

                      |

              Agent Platform

                      |

          +-----------+-----------+

          |                       |

          v                       v

   Agent Runtime             Model Gateway


          |

          v

   Tools / MCP / APIs


          |

          v

     Data Sources
```

---

# Platform Components

## Agent Runtime

Handles:

- Execution
- State management
- Workflows

---

## Model Gateway

Provides:

- Model routing
- Rate limits
- Cost control

---

## Tool Layer

Supports:

- APIs
- MCP servers
- Databases

---

## Observability

Tracks:

- Prompts
- Responses
- Tool calls
- Latency
- Cost

---

# 8. How Do You Handle LLM Scaling?

## Answer

Key strategies:

## Application Layer

- Load balancing
- Async processing
- Request batching

---

## Model Layer

- Model routing
- Smaller models
- Quantization

---

## Data Layer

- Caching
- Efficient retrieval
- Index optimization

---

# 9. How Do You Reduce LLM Latency?

## Answer

Strategies:

- Stream responses
- Reduce prompt size
- Cache responses
- Use smaller models
- Optimize retrieval
- Parallelize tool calls

---

# 10. How Do You Reduce LLM Cost?

## Answer

Strategies:

- Token optimization
- Prompt compression
- Model selection
- Response caching
- Batch processing
- Avoid unnecessary agent steps

---

# 11. How Do You Make LLM Systems Reliable?

## Answer

Use:

## Reliability

- Retries
- Timeouts
- Fallback models

## Quality

- Evaluation pipelines
- Guardrails

## Operations

- Monitoring
- Logging
- Alerting

---

# 12. How Do You Secure LLM Applications?

## Answer

Security areas:

## Data Security

- Encryption
- Access control
- PII protection

---

## Prompt Security

Protect against:

- Prompt injection
- Data leakage

---

## Tool Security

Use:

- Least privilege
- Approval workflows
- Audit logs

---

# 13. How Do You Evaluate an LLM System?

## Answer

Evaluation should include:

## Offline

- Accuracy
- Retrieval metrics
- Benchmark datasets

---

## Online

- User feedback
- Success rate
- Latency

---

## Production

- Cost
- Errors
- Hallucination rate

---

# Senior Interview Closing Answer

> When designing LLM systems, I focus on separating intelligence from infrastructure. The LLM provides reasoning capabilities, while retrieval, tools, memory, evaluation, security, and observability make the system reliable in production. The key engineering challenge is balancing quality, latency, cost, and safety.

---

# Key Takeaways

- LLM applications require more than just calling a model API.
- Production systems combine RAG, agents, tools, memory, and guardrails.
- System design discussions should cover architecture, scaling, security, evaluation, and cost.
- Senior AI engineers should think about the entire AI lifecycle.
