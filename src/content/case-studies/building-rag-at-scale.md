---
title: "Building a RAG System That 10,000+ Engineers Actually Use"
description: "How I designed, built, and shipped a Retrieval-Augmented Generation chatbot that became the go-to knowledge tool across Trimble."
date: "2024-06-15"
tags: ["RAG", "LangChain", "Qdrant", "Azure OpenAI", "FastAPI"]
company: "Trimble"
role: "Full Stack Software Engineer"
impact: "Company-wide adoption"
featured: true
---

## Context

Trimble is a large technology company with thousands of engineers across multiple product lines. Documentation was scattered across Confluence, SharePoint, internal wikis, and Slack channels. New engineers spent their first weeks just learning where to find things.

## The Challenge

Build a system that could:
1. Ingest documentation from multiple sources with different formats
2. Return accurate, sourced answers in under 3 seconds
3. Handle domain-specific terminology (forestry, construction, geospatial)
4. Scale to thousands of daily queries without degradation

## Approach

### Document Ingestion Pipeline

Built an automated pipeline that crawls documentation sources on a schedule, chunks documents intelligently (respecting headers and code blocks), and upserts embeddings into Qdrant.

Key decisions:
- **Chunk size:** 512 tokens with 50-token overlap — empirically tested against 256 and 1024
- **Embedding model:** Azure OpenAI `text-embedding-ada-002` for cost-performance balance
- **Metadata:** Preserved source URL, team ownership, last-modified date for filtering and attribution

### Retrieval Strategy

Implemented hybrid retrieval combining:
- **Semantic search** via Qdrant for meaning-based retrieval
- **Metadata filtering** so users could scope queries to their product area
- **Re-ranking** to improve precision on the top-k results

### Generation with Guardrails

- System prompt that enforces sourced answers — the model must cite which documents it drew from
- Temperature set to 0.1 for consistency
- Conversation memory with a sliding window to handle follow-up questions without context explosion

### Frontend Integration

Built the chat interface as an Angular component that could be embedded in any internal tool. Added features like:
- Source document links alongside each answer
- Thumbs up/down feedback collection
- Conversation history with search

## Results

- Adopted across multiple departments within 3 months of launch
- Became the default first-stop for engineering questions
- Received internal recognition for driving AI adoption

## What I'd Do Differently

- **Start with evaluation first.** I built the system before establishing proper evaluation metrics. In hindsight, creating a test set of question-answer pairs upfront would have accelerated iteration.
- **Invest more in chunking.** The biggest retrieval quality gains came from better chunking strategies, not model upgrades.
- **User feedback loop sooner.** The thumbs up/down data became the most valuable signal for improving the system — wish I'd added it from day one.
