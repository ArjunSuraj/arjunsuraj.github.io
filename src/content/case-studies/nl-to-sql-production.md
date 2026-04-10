---
title: "From Natural Language to SQL: Democratizing Data Access"
description: "Building a production NL-to-SQL system that lets non-technical users query databases using plain English."
date: "2024-03-10"
tags: ["NL-to-SQL", "LLMs", "FastAPI", "Prompt Engineering", "Python"]
company: "Trimble"
role: "Full Stack Software Engineer"
impact: "Self-serve data access for non-technical teams"
featured: true
---

## Context

Data-driven decisions require data access. But at most companies, getting a specific data point means filing a ticket, waiting for an engineer to write the query, and hoping it answers the right question. This cycle repeated dozens of times per week.

## The Challenge

Build a system where business users can ask questions in plain English — "What were the top 5 customers by revenue last quarter?" — and get accurate SQL results back instantly. Without exposing them to SQL, schemas, or database complexity.

## Approach

### Schema Understanding

The hardest part wasn't generating SQL — it was giving the LLM enough context to generate *correct* SQL. I built a schema description layer that provides:

- Table structures with column types and descriptions
- Foreign key relationships between tables
- Business glossary mapping (e.g., "revenue" → `orders.total_amount`)
- Example queries for common patterns

### Safety First

Non-technical users querying production databases is terrifying without guardrails:

- **Read-only enforcement:** SQL parser rejects any INSERT, UPDATE, DELETE, DROP statements
- **LIMIT enforcement:** All queries automatically capped to prevent full-table scans
- **Cost estimation:** Queries estimated to scan more than a threshold of rows are flagged for review
- **Audit logging:** Every generated query logged with the original natural language input

### Prompt Engineering Pipeline

Rather than a single prompt, built a multi-step pipeline:

1. **Intent classification** — Is this a data query, a definition question, or something else?
2. **Schema selection** — Which tables are relevant to this question?
3. **SQL generation** — Generate the query with the selected schema context
4. **Validation** — Parse and validate the generated SQL
5. **Self-correction** — If execution fails, feed the error back for retry (max 2 attempts)

### Few-Shot Examples

Curated 50+ example query-SQL pairs per domain. This was the single biggest accuracy improvement — domain-specific examples beat generic prompt engineering every time.

## Results

- Non-technical users able to self-serve data queries
- Query turnaround dropped from days to seconds
- High accuracy on domain-specific queries through careful prompt tuning

## Key Learnings

- **Few-shot examples are king.** Generic prompts produce generic (wrong) SQL. Domain-specific examples are the difference between a demo and a product.
- **Error recovery matters more than first-try accuracy.** The self-correction loop handles ~15% of queries that fail on first attempt.
- **Schema descriptions are underrated.** Column names like `cust_id` or `amt` are meaningless to an LLM without descriptions. Adding a business glossary improved accuracy significantly.
