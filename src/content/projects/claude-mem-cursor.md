---
title: "Claude Brain — Persistent Memory for Claude Code"
description: "A plugin that gives Claude Code photographic memory across sessions. One file, zero cloud dependencies, sub-millisecond search."
tags: ["JavaScript", "AI", "Claude Code", "Developer Tools", "Plugins"]
github: "https://github.com/ArjunSuraj/claude-mem-cursor"
featured: true
order: 2
---

## Overview

Claude Code has a 200K context window but zero memory between sessions. Claude Brain fixes that — it captures session context, decisions, bugs, and solutions into a single local file that gets auto-injected at session start.

## The Problem

```
You: "Remember that auth bug we fixed?"
Claude: "I don't have memory of previous conversations."
You: "We spent 3 hours on it yesterday"
Claude: "I'd be happy to help debug from scratch!"
```

Every session starts from zero. All the context from previous conversations — architecture decisions, debugging sessions, codebase-specific knowledge — is lost.

## The Solution

A single `.mv2` file in your project that acts as Claude's persistent brain:

```
your-project/
└── .claude/
    └── mind.mv2   # Claude's brain
```

- **No database.** No cloud. No API keys.
- **Auto-captures** session context, decisions, bugs, and solutions
- **Auto-injected** at session start — Claude picks up where it left off
- **Searchable** anytime via natural language or commands
- **Git-friendly** — `git commit` your Claude's brain for version control

## Commands

```bash
/mind stats                       # memory statistics
/mind search "authentication"     # find past context
/mind ask "why did we choose X?"  # ask your memory
/mind recent                      # what happened lately
```

## Performance

- Empty file: ~70KB
- Growth: ~1KB per memory
- A year of use stays under 5MB
- Search: <1ms across 10K+ memories (native Rust core)

## Installation

```bash
/plugin add marketplace memvid/claude-brain
```

Built on [memvid](https://github.com/memvid/memvid) — the single-file memory engine.
