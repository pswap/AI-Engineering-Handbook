# Agent Interview Questions and Answers

## Overview

This document covers AI Agent interview questions for mid-senior AI Engineer roles.

Topics:

- AI Agent fundamentals
- ReAct
- Planning
- Tool calling
- Memory
- Reflection
- LangGraph
- Multi-agent systems
- MCP
- Agent evaluation
- Production challenges

---

# 1. What is an AI Agent?

## Short Answer

An AI agent is an LLM-powered system that can reason about a goal, make decisions, use tools, maintain state, and execute actions to complete tasks.

Unlike a chatbot that only generates responses, an agent can take actions and interact with external systems.

---

## Traditional LLM Application

```
User

↓

Prompt

↓

LLM

↓

Response
```

---

## Agent System

```
User Goal

↓

Agent

↓

Reason

↓

Plan

↓

Use Tools

↓

Observe Results

↓

Complete Task
```

---

# 2. What Are the Main Components of an AI Agent?

## Answer

A production agent typically contains:

```
Agent

├── LLM Reasoning Engine
├── Planning Module
├── Tool Layer
├── Memory
├── State Management
├── Guardrails
└── Evaluation
```

---

## Components

### LLM

Responsible for:

- Reasoning
- Decision making
- Natural language understanding

---

### Planning

Breaks complex goals into smaller steps.

Example:

```
Build travel itinerary

1. Find flights
2. Find hotels
3. Create schedule
```

---

### Tools

Allow agents to interact with external systems.

Examples:

- APIs
- Databases
- Search
- Code execution

---

### Memory

Stores information across interactions.

Examples:

- Conversation history
- User preferences
- Previous tasks

---

# 3. What Is the ReAct Pattern?

## Short Answer

ReAct (Reasoning + Acting) is an agent pattern where the model alternates between reasoning about a task and taking actions using tools.

---

## Flow

```
Question

↓

Reason

↓

Action

↓

Observation

↓

Reason

↓

Final Answer
```

---

Example:

User:

```
What is the weather in Seattle?
```

Agent:

```
Thought:
Need current weather.

Action:
Call weather API.

Observation:
Temperature is 65F.

Answer:
Seattle is 65F.
```

---

# 4. Why Use ReAct Instead of Direct Prompting?

## Answer

Direct prompting works for simple tasks.

ReAct is useful when tasks require:

- External information
- Multiple steps
- Tool usage
- Dynamic decisions

---

Example:

Simple:

```
Summarize this text
```

Agent:

```
Research topic

↓

Collect information

↓

Analyze

↓

Generate report
```

---

# 5. Explain Tool Calling

## Short Answer

Tool calling allows an LLM to invoke external functions or APIs to perform actions or retrieve information.

---

Architecture:

```
User

↓

Agent

↓

LLM

↓

Tool Selection

↓

External API

↓

Result

↓

LLM Response
```

---

Example:

```
get_customer_order(customer_id)
```

The model decides when and how to call the tool.

---

# 6. How Does an Agent Decide Which Tool to Use?

## Answer

The LLM evaluates:

- User intent
- Available tools
- Tool descriptions
- Current context

Example:

User:

```
Find my recent transactions
```

Agent chooses:

```
Banking API Tool
```

not:

```
Web Search Tool
```

---

# 7. Function Calling vs MCP

## Short Answer

Function calling connects an LLM to application-specific functions. MCP provides a standardized protocol for agents to discover and use external tools and resources.

---

Comparison:

| Function Calling | MCP |
|-|-|
| Application-specific | Standard protocol |
| Functions defined by app | Tools exposed by servers |
| Tight coupling | Loose coupling |

---

# 8. Explain MCP in Agent Architecture

## Short Answer

MCP allows agents to connect with external systems through a standardized interface.

---

Architecture:

```
Agent

↓

MCP Client

↓

MCP Server

↓

Tools / Resources

↓

External Systems
```

---

Examples:

- GitHub MCP Server
- Jira MCP Server
- Database MCP Server

---

# 9. What Is Agent Memory?

## Short Answer

Agent memory allows an AI system to retain information across interactions and use previous context when making decisions.

---

Types:

```
Short-Term Memory

Long-Term Memory

Vector Memory
```

---

# 10. Short-Term vs Long-Term Memory

## Short-Term Memory

Stores current conversation state.

Example:

```
Current conversation history
```

---

## Long-Term Memory

Stores information across sessions.

Example:

```
User prefers detailed explanations
```

---

# 11. How Does Vector Memory Work?

## Short Answer

Vector memory stores information as embeddings and retrieves relevant memories using similarity search.

---

Flow:

```
Experience

↓

Embedding

↓

Vector Database

↓

Similarity Search

↓

Relevant Memory
```

---

Example:

User:

```
Recommend a vacation
```

Agent retrieves:

```
User prefers beaches
```

---

# 12. Explain Planning in Agents

## Short Answer

Planning allows an agent to decompose a complex goal into smaller executable steps.

---

Example:

Goal:

```
Create market research report
```

Plan:

```
1. Collect data

2. Analyze competitors

3. Generate report

4. Review output
```

---

# 13. Plan-and-Execute vs ReAct

## ReAct

```
Think

↓

Act

↓

Observe

↓

Repeat
```

Good for:

- Dynamic tasks

---

## Plan-and-Execute

```
Create complete plan

↓

Execute steps
```

Good for:

- Predictable workflows

---

# 14. What Is Reflection in Agents?

## Short Answer

Reflection allows an agent to evaluate its own output and improve it.

---

Flow:

```
Generate Answer

↓

Review Answer

↓

Identify Issues

↓

Improve
```

---

Example:

Coding agent:

```
Generate code

↓

Run tests

↓

Fix errors
```

---

# 15. What Is a Multi-Agent System?

## Short Answer

A multi-agent system uses multiple specialized agents coordinated to solve complex problems.

---

Example:

```
Supervisor Agent

       |

+------+------+------+

Research  Coding  Review
Agent     Agent   Agent
```

---

# 16. Why Use Multiple Agents?

## Advantages

- Specialization
- Better modularity
- Easier maintenance
- Parallel execution

---

Challenges:

- Coordination complexity
- Higher cost
- Debugging difficulty

---

# 17. Explain Supervisor Agent Pattern

## Short Answer

A supervisor agent coordinates specialist agents by deciding which agent should handle each task.

---

Example:

```
User

↓

Supervisor

↓

Research Agent

Coding Agent

Writing Agent
```

---

# 18. LangGraph Agent Architecture

## Short Answer

LangGraph represents agents as stateful workflows where nodes represent agents or actions and edges define execution flow.

---

Architecture:

```
        START

          |

     Supervisor

     /    |    \

Research Tool Review

     \    |    /

          END
```

---

Components:

- Nodes
- Edges
- State
- Checkpoints

---

# 19. How Do You Make Agents Reliable?

## Answer

I focus on:

### 1. Control

- Limit tools
- Add approvals

### 2. Reliability

- Retries
- Timeouts
- Fallbacks

### 3. Observability

Track:

- Decisions
- Tool calls
- Failures

### 4. Evaluation

Measure:

- Task completion
- Accuracy
- Cost

---

# 20. How Do You Prevent Unsafe Agent Actions?

## Answer

Use:

- Tool permissions
- Human approval
- Input validation
- Output validation
- Guardrails
- Audit logging

---

Example:

Before:

```
Delete production database
```

Require:

```
Human approval
```

---

# 21. How Do You Evaluate an Agent?

## Short Answer

Agent evaluation should measure both final output quality and execution behavior.

---

Metrics:

## Task Metrics

- Completion rate
- Accuracy

---

## Agent Behavior

- Planning quality
- Tool selection accuracy
- Number of steps

---

## System Metrics

- Latency
- Cost
- Failures

---

# 22. Agent vs Workflow Automation

## Agent

Dynamic decision making:

```
Decides next action
```

---

## Workflow

Fixed steps:

```
Step 1 → Step 2 → Step 3
```

---

Use agents when:

- Problems are uncertain
- Decisions are required

Use workflows when:

- Process is predictable

---

# 23. How Would You Design an AI Research Agent?

## Architecture

```
User

↓

Supervisor Agent

↓

Research Agent

↓

Search Tool

↓

RAG System

↓

Analysis Agent

↓

Writing Agent

↓

Final Response
```

---

Components:

- Planning
- Tools
- Memory
- Retrieval
- Evaluation

---

# 24. How Do You Reduce Agent Cost?

## Answer

Strategies:

- Reduce unnecessary tool calls
- Use smaller models for simple tasks
- Cache results
- Limit reasoning steps
- Use model routing
- Optimize prompts

---

# 25. Common Agent Failure Modes

## Infinite Loops

Cause:

Agent keeps retrying.

Solution:

- Maximum iterations
- State tracking

---

## Wrong Tool Usage

Cause:

Poor tool descriptions.

Solution:

- Better schemas
- Validation

---

## Hallucinated Actions

Cause:

Agent assumes tool results.

Solution:

- Verify outputs
- Require evidence

---

## Excessive Cost

Cause:

Too many LLM calls.

Solution:

- Optimize workflow

---

# Senior-Level Design Question

## Design an Enterprise AI Agent Platform

## Answer Framework

Requirements:

```
Users need AI assistants that can access company systems.
```

Architecture:

```
User

↓

API Gateway

↓

Agent Orchestrator

↓

Supervisor Agent

↓

Specialist Agents

↓

Tools + MCP Servers

↓

RAG + Memory

↓

LLM

↓

Guardrails

↓

Response
```

Production concerns:

- Security
- Evaluation
- Observability
- Cost
- Reliability

---

# Interview Summary

A production AI agent is not just an LLM with a prompt. It is a system combining reasoning, planning, tools, memory, orchestration, evaluation, and safety controls. The key engineering challenge is balancing autonomy with reliability, security, and cost.

---

# Key Takeaways

- Agents combine LLM reasoning with actions.
- ReAct enables reasoning and tool usage.
- Planning breaks complex goals into steps.
- Memory enables personalization.
- MCP standardizes tool integration.
- Multi-agent systems provide specialization.
- Production agents require evaluation, security, and observability.
