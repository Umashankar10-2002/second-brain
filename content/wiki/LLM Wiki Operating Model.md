---
title: "LLM Wiki Operating Model"
type: synthesis
created: 2026-05-09
updated: 2026-05-09
sources:
  - "wiki/llm-wiki.md"
  - "AGENTS.md"
tags:
  - llm-wiki
  - knowledge-management
  - operations
---

# LLM Wiki Operating Model

## Thesis

The vault should compound by turning raw sources, questions, journal reflections, and CRM updates into durable markdown pages. The important shift is from one-off chat answers to maintained knowledge artifacts.

## Operating Loop

1. Raw sources remain preserved in `raw/processed/`.
2. The wiki stores source summaries, entity pages, and synthesis pages.
3. `index.md` helps both user and LLM locate knowledge.
4. `log.md` records operations chronologically.
5. `AGENTS.md` evolves as the operating schema.

## What Changed In This Reprocess

- Source summaries now point to `raw/processed/` source files.
- Cross-source synthesis pages were added for creator packaging, trading psychology, algorithmic trading, and the wiki operating model.
- Root raw files are moved to `raw/processed/` after processing.

## Related

- [[wiki/llm-wiki]]
- [[AGENTS]]
- [[index]]
- [[log]]

