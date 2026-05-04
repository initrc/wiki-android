# Android LLM Wiki Schema

This repository is an LLM-maintained wiki about Android development.

The user curates sources and asks questions. The agent maintains the wiki: it ingests sources, writes and updates markdown pages, preserves citations, cross-links related concepts, flags contradictions, and keeps indexes/logs current.

This wiki follows the LLM Wiki pattern: raw sources are immutable, wiki pages are synthesized and maintained over time, and this `AGENTS.md` file is the operating schema for future agent sessions.

## Scope

The wiki covers Android development, including:

- Android framework APIs and Jetpack libraries
- Kotlin and Java patterns used in Android apps
- App architecture, lifecycle, UI, data, background work, performance, security, accessibility, testing, release, and tooling
- Android Studio, Gradle, emulator, adb, Play Console, and CI/CD workflows
- Practical troubleshooting and migration notes

## Source Types

Expected source inputs:

- Official Android documentation web pages
- Web articles and blog posts
- YouTube video links
- User-authored markdown notes

Treat official Android documentation as the highest-authority source. Treat reputable articles and videos as secondary sources. Treat user notes as local context and preference unless they explicitly cite external facts.

## Directory Layout

Use this structure as the wiki grows:

```text
raw/
  official-docs/
  articles/
  youtube/
  notes/
  assets/
wiki/
  index.md
  log.md
  overview.md
  glossary.md
  topics/
  apis/
  libraries/
  tools/
  patterns/
  troubleshooting/
  sources/
  questions/
```

Raw sources are the source of truth and should not be modified except to add metadata or local copies when the user asks. Wiki pages are agent-maintained synthesized markdown.

## File Naming

Use lowercase kebab-case filenames:

- `wiki/topics/activity-lifecycle.md`
- `wiki/apis/workmanager.md`
- `wiki/tools/adb.md`
- `wiki/sources/android-docs-workmanager.md`

Prefer stable concept names over source-specific names for topic pages. Source pages may include publisher/source names.

## Page Frontmatter

Every wiki page should begin with YAML frontmatter:

```yaml
---
title: "Page Title"
kind: topic
status: draft
last_updated: YYYY-MM-DD
sources:
  - source-id
tags:
  - android
---
```

Allowed `kind` values:

- `overview`
- `topic`
- `api`
- `library`
- `tool`
- `pattern`
- `troubleshooting`
- `source`
- `question`
- `glossary`

Allowed `status` values:

- `draft`
- `active`
- `needs-review`
- `superseded`

## Source Records

For every ingested source, create or update a page in `wiki/sources/` with this structure:

```markdown
---
title: "Source Title"
kind: source
status: active
last_updated: YYYY-MM-DD
source_id: short-stable-id
source_type: official-doc | article | youtube | user-note
authority: primary | secondary | local
url: "https://example.com"
captured_at: YYYY-MM-DD
tags:
  - android
---

# Source Title

## Bibliographic Metadata

- Publisher:
- Author:
- Published:
- Updated:
- Captured:
- URL:

## Summary

## Key Claims

## Concepts Touched

## Follow-Up Questions
```

If a source is a YouTube link, capture the title, channel, URL, date, and transcript source when available. If no transcript is available, state that the summary is based only on available metadata or user-provided notes.

## Ingest Workflow

When the user provides a new source:

1. Identify source type, authority level, title, URL/path, author or publisher, and capture date.
2. Read the source content. For web sources, preserve the URL. For user notes, preserve the original markdown path.
3. Create or update the relevant `wiki/sources/` page.
4. Extract key claims, definitions, APIs, workflows, caveats, version constraints, and examples.
5. Update existing concept pages rather than duplicating knowledge across new pages.
6. Create new topic, API, tool, pattern, or troubleshooting pages only when the concept is likely to recur.
7. Add bidirectional links between related pages using Obsidian-style links, for example `[[activity-lifecycle]]`.
8. Update `wiki/index.md`.
9. Append an entry to `wiki/log.md`.

Prefer ingesting sources one at a time unless the user explicitly asks for batch ingestion.

## Query Workflow

When answering a question about the wiki:

1. Read `wiki/index.md` first if it exists.
2. Search relevant wiki pages and source pages.
3. Prefer synthesized wiki pages, then verify important claims against source pages or raw sources.
4. Answer with citations to wiki pages and source URLs/paths.
5. If the answer creates reusable synthesis, ask whether to file it, or file it directly when the user asks to update the wiki.

## Maintenance Workflow

Periodically lint the wiki for:

- Contradictions between official docs, secondary sources, and older wiki pages
- Stale claims caused by Android API, Gradle, Kotlin, Jetpack, or Android Studio changes
- Missing citations
- Orphan pages
- Important concepts without dedicated pages
- Duplicate pages covering the same concept
- Broken or missing source links
- Pages marked `needs-review`

Official Android docs can change over time. When a claim depends on current platform behavior, library versions, API levels, Gradle behavior, Play policy, or Android Studio behavior, verify against current official documentation before treating it as authoritative.

## Citation Rules

- Every nontrivial factual claim should be traceable to at least one source.
- Prefer primary sources for API behavior, platform requirements, policies, and tooling instructions.
- Secondary sources may be used for interpretation, examples, history, or tradeoffs.
- User notes may capture preferences, project-specific decisions, and hypotheses.
- If sources conflict, do not hide the conflict. Create a "Contradictions / Open Questions" section on the relevant page.

## Index Format

Maintain `wiki/index.md` as the content map:

```markdown
# Android LLM Wiki Index

## Overview

- [[overview]] - One-page synthesis of the wiki.

## Topics

- [[activity-lifecycle]] - Lifecycle states and practical implications.

## APIs

## Libraries

## Tools

## Patterns

## Troubleshooting

## Sources

## Questions
```

Update the index on every ingest or substantial wiki edit.

## Log Format

Maintain `wiki/log.md` as an append-only chronological record. Use this heading format:

```markdown
## [YYYY-MM-DD] ingest | Source Title

- Source:
- Pages created:
- Pages updated:
- Key changes:
- Open questions:
```

Other allowed log entry types:

- `query`
- `synthesis`
- `lint`
- `maintenance`

## Android Taxonomy

Use these recurring tags where appropriate:

- `android`
- `kotlin`
- `java`
- `jetpack`
- `compose`
- `views`
- `lifecycle`
- `navigation`
- `architecture`
- `data`
- `networking`
- `storage`
- `background-work`
- `performance`
- `security`
- `privacy`
- `accessibility`
- `testing`
- `build`
- `gradle`
- `adb`
- `emulator`
- `release`
- `play-console`
- `troubleshooting`

## Writing Style

- Write concise, practical engineering notes.
- Prefer current Android recommendations over historical patterns, but preserve migration context when useful.
- Include code snippets only when they clarify a concept or workflow.
- Mark uncertain claims explicitly.
- Avoid marketing language.
- Keep pages useful for a developer trying to make implementation decisions.

## Agent Operating Rules

- Do not overwrite raw sources.
- Do not delete wiki pages unless the user explicitly approves.
- When updating a page, preserve useful existing synthesis and integrate new information into it.
- Prefer small, focused pages with strong cross-links over large monolithic notes.
- Always update `wiki/index.md` and `wiki/log.md` after ingesting sources.
- Use `rg` for local search when available.
- When checking current Android facts, use official Android documentation first.
