# LLM Wiki Schema

This vault follows Karpathy's LLM Wiki pattern:

https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

The structure has three layers:

- `raw/` - raw sources. These are immutable source documents. Read them, but do not modify them.
- `wiki/` - the LLM-maintained wiki. Create and update markdown pages here.
- `AGENTS.md` - the schema. This file defines the conventions and workflows for maintaining the wiki.

## Required Files

- `index.md` - content-oriented catalog of wiki pages.
- `log.md` - chronological append-only record of ingests, queries, and lint passes.

## Operations

Log entries should use this format:

```md
## [YYYY-MM-DD] ingest | Source Title
## [YYYY-MM-DD] query | Question or Topic
## [YYYY-MM-DD] journal | Journal Entry Title
## [YYYY-MM-DD] crm | Person Name
## [YYYY-MM-DD] lint | Scope
```

### Ingest

When the user adds a source and asks the LLM to process it:

1. Read the source from `raw/` or from the provided URL/path.
2. Create or update wiki pages in `wiki/`.
3. Update relevant entity, concept, topic, overview, synthesis, or comparison pages.
4. Cross-link any wiki page generated or updated to the original source page.
5. Update `index.md`.
6. Append an entry to `log.md`.
7. Move the source file from the root `raw/` directory to `raw/processed/`.

Prefer ingesting sources one at a time unless the user asks for batch ingestion.

For YouTube videos clipped with Obsidian Web Clipper, also open or inspect the YouTube source URL and add the channel name to the generated source summary frontmatter:

```yaml
channel: Channel Name
```

If the channel name cannot be determined from the clipped file alone, fetch it from YouTube before finishing the ingest.

### Journal

When the user starts a chat with `Journal:`:

1. Treat the entire user journal text and the subsequent conversation as one journal entry.
2. Create a `journal/` folder if it does not exist.
3. Create `journal/index.md` if it does not exist. The journal index should be similar to `index.md`, with a table that lists date, title, summary, and a link to each journal entry.
4. Decide on a short, descriptive title for the journal entry based on its contents.
5. Save the entry as a new markdown file in `journal/` using this filename format: `YYYY-MM-DD - Short Title.md`.
6. Include the original journal text, important follow-up conversation, and any useful advice or insights generated during the exchange.
7. Add the date, title, short summary, and link to `journal/index.md`.
8. If the conversation produces a reusable idea, framework, tactic, or durable insight, create or update a synthesis page in `wiki/` and link it from the journal entry.
9. If a synthesis page is created or updated, update `index.md`.
10. Append an entry to `log.md` with the journal title and a short summary.

Journal responses should be grounded in:

- relevant pages from `wiki/`
- past entries from `journal/`
- available CRM notes or files, if a CRM exists in the vault or connected workspace
- the LLM's general knowledge, clearly separated from vault-grounded claims when needed

When responding to journal entries, provide useful advice, insights, guidance, tactics, and ideas. Prefer practical, specific recommendations over generic encouragement.

### CRM

When the user says they are giving information for the CRM:

1. Create a `crm/` folder if it does not exist.
2. Create `crm/index.md` if it does not exist.
3. Identify the person the user is describing.
4. If the person already has a CRM file, update that file.
5. If the person does not already have a CRM file, create one.
6. CRM person files should always be named with the person's name: `crm/Person Name.md`.
7. Add whatever details the user provides, including name, contact details, where or how the user met them, things the user knows about them, relationship context, follow-up ideas, and relevant dates.
8. Update `crm/index.md` with the person's name, a link to their CRM file, and a short bio or summary of what is known about them.
9. Keep `crm/index.md` sorted alphabetically by person name.
10. Append an entry to `log.md` with the person's name and a short summary of what changed.

CRM files should use a practical structure:

```md
# Person Name

## Contact

## How We Met

## Known Details

## Relationship Context

## Follow-Ups

## Notes
```

When answering questions about contacts, read `crm/index.md` first, then read the relevant person files. Use CRM information carefully and do not invent personal facts that are not present in the CRM or supplied by the user.

### Query

When the user asks a question:

1. Read `index.md`.
2. Search relevant pages in `wiki/`.
3. Read the most relevant source summaries and raw sources when needed.
4. Synthesize an answer with links to the wiki pages or raw sources used.
5. If the answer is reusable, save it as a new or updated wiki page.
6. If a wiki page is created or updated, update `index.md`.
7. If a wiki page is created or updated, append an entry to `log.md`.

### Lint

When the user asks for a wiki health check:

1. Read `index.md`.
2. Scan `wiki/` for contradictions between pages.
3. Find stale claims that newer sources may have superseded.
4. Find orphan pages with no inbound links.
5. Find important concepts mentioned repeatedly but missing their own page.
6. Find missing cross-references between related pages.
7. Find data gaps that could be filled with new sources or web research.
8. Fix straightforward issues when the requested scope allows it.
9. Update `index.md` if pages are created, renamed, or materially changed.
10. Append a lint entry to `log.md`.

Prefer concrete fixes over abstract advice, but do not invent unsupported claims.
