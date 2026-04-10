---
title: "Natural Language to SQL"
description: "A production API that translates natural language questions into SQL queries, empowering non-technical users to query databases directly."
tags: ["Python", "FastAPI", "LLMs", "Azure OpenAI", "SQL", "Prompt Engineering"]
featured: true
order: 2
---

## Overview

Built a production-ready API that converts natural language questions into SQL queries, allowing non-technical stakeholders to extract insights from databases without writing code.

## The Problem

Business analysts and product managers needed data insights but depended on engineering teams to write SQL queries. This created bottlenecks — simple data requests could take days to fulfill, slowing down decision-making.

## The Solution

Developed an intelligent NL-to-SQL system that:

- **Understands schema context** — automatically maps database schemas, table relationships, and column semantics
- **Generates safe SQL** — produces read-only queries with built-in guardrails to prevent destructive operations
- **Handles ambiguity** — asks clarifying questions when a natural language query maps to multiple possible interpretations
- **Validates before executing** — runs generated SQL through a validation layer before execution

## Technical Approach

- **Schema representation:** Built a schema description layer that provides the LLM with table structures, foreign keys, and column descriptions
- **Few-shot prompting:** Curated example query-SQL pairs for each domain to improve accuracy
- **Query validation:** Implemented SQL parsing to reject mutations, enforce LIMIT clauses, and prevent expensive full-table scans
- **Error recovery:** When queries fail, the system feeds errors back to the LLM for self-correction

## Stack

- Python + FastAPI
- Azure OpenAI (GPT-4 for query generation)
- Custom prompt engineering pipeline
- MySQL / PostgreSQL compatible

## Impact

- Empowered non-technical users to self-serve data queries
- Reduced data request turnaround from days to seconds
- Achieved high accuracy on domain-specific queries through careful prompt tuning
