---
title: "Trimble AI Assistant"
description: "A RAG-powered chatbot trained on internal documentation, adopted company-wide across Trimble for instant knowledge retrieval."
tags: ["RAG", "LangChain", "Python", "FastAPI", "Qdrant", "Azure OpenAI"]
featured: true
order: 3
---

## Overview

Built a production-ready Retrieval-Augmented Generation (RAG) chatbot that enables employees across Trimble to get instant answers from internal documentation, wikis, and knowledge bases.

## The Problem

Engineers and support teams spent significant time searching through scattered documentation across multiple platforms. Finding the right answer often meant digging through Confluence pages, Slack threads, and internal wikis — slowing down onboarding and day-to-day work.

## The Solution

Designed and implemented an AI assistant that:

- **Ingests documents** from multiple sources (Confluence, SharePoint, internal wikis) into a vector database
- **Retrieves relevant context** using semantic search with Qdrant as the vector store
- **Generates accurate answers** using Azure OpenAI with retrieved context, reducing hallucination through careful prompt engineering
- **Handles follow-ups** with conversation memory and context windowing

## Architecture

- **Backend:** Python + FastAPI for the API layer
- **Embeddings:** Azure OpenAI embedding models for document vectorization
- **Vector Store:** Qdrant for fast similarity search
- **Orchestration:** LangChain for the RAG pipeline
- **Frontend:** Angular-based chat interface embedded in internal tools

## Impact

- Adopted company-wide across multiple departments
- Significantly reduced time-to-answer for common engineering questions
- Recognized internally for driving AI adoption at Trimble

## Lessons Learned

- Chunk size and overlap strategy dramatically affect retrieval quality — spent significant time tuning these parameters
- Metadata filtering (by team, product, date) was crucial for relevance in a large document corpus
- Building trust required transparency: showing source documents alongside generated answers
