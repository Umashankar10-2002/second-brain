---
title: "llm-wiki"
type: source-summary
source: "raw/processed/llm-wiki.md"
source_url: "https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f"
author: "Andrej Karpathy"
published:
processed: 2026-05-08
tags:
  - llm-wiki
  - knowledge-management
  - source-summary
---

# llm-wiki

## Summary

Karpathy describes a pattern for building a personal knowledge base where an LLM maintains a persistent markdown wiki between the user's raw sources and future questions. The point is to avoid re-deriving knowledge from raw documents every time. Instead, the LLM incrementally extracts, integrates, links, updates, and revises durable wiki pages as new sources arrive.

The architecture has three layers: raw sources, the wiki, and the schema. Raw sources are immutable. The wiki is the LLM-authored synthesis layer. The schema, such as `AGENTS.md`, tells the LLM how to maintain the system.

## Key Points

- The wiki is meant to compound over time.
- The LLM owns the bookkeeping: summaries, cross-references, contradictions, page updates, and logs.
- The human owns source curation, exploration, judgment, and questions.
- `index.md` is the content-oriented catalog of the wiki.
- `log.md` is the chronological record of ingests, queries, and lint passes.
- Useful answers can be saved back into the wiki so questions become part of the knowledge base.
- Periodic linting should find contradictions, stale claims, orphan pages, missing concepts, missing cross-references, and data gaps.

## Why It Matters

This source defines the operating model for this vault. It says the wiki should be a persistent, compounding artifact, not just a folder of clipped notes or a retrieval layer over raw files.

## Source

- [[raw/processed/llm-wiki|Raw source]]
- [Karpathy gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)

## Related

- [[wiki/LLM Wiki Operating Model]]
