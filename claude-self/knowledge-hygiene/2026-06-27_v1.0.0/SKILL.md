---
name: knowledge-hygiene
description: >-
  Curate persistent notes/memory across sessions (CLAUDE.md, project journals, design docs,
  long-running TODO/changelog files) using engagement-driven salience instead of pure recency:
  split entries into protected vs. decayable, extract essence before deleting raw entries,
  version new understanding instead of silently editing history. Triggers: clean up notes, prune
  CLAUDE.md, consolidate journal, archive old notes, memory hygiene, 整理笔记, 清理记忆, 笔记瘦身
license: MIT
metadata:
  author: Claude
  version: 1.0.0
  inspired_by: do-do026/ember-memory — memory-hygiene skill (渡渡/初尘, v2.2.0–v2.6.0)
---

# /knowledge-hygiene — keep what's worth keeping

## Core philosophy
A notes file is read far more often than it's written. Every entry that survives a cleanup pass
should earn its place by being useful to a *future* reader who has no memory of writing it — not
by being recent.

## When this applies
Any persistent artifact meant to outlive the current session: `CLAUDE.md`, a project journal,
a running decision log, a TODO/changelog file, accumulated design notes. Not for code itself.

## Triage: protected vs. decayable
Before editing, split entries into two buckets:
- **Protected** — load-bearing facts a future session would break without: architecture
  decisions with non-obvious rationale, hard-won gotchas, naming/versioning conventions,
  anything explicitly marked "don't change this." These don't get pruned just because they're old.
- **Decayable** — everything else: status updates, one-off observations, superseded plans. These
  are candidates for consolidation or removal once they stop being useful.

Salience should track *how often something is actually referenced or re-derived*, not how
recently it was written. A six-month-old gotcha that still saves debugging time outranks
yesterday's status note that nobody will reread.

## Rules
1. **Read before you prune.** Decide what to cut by reading the actual content, not by skimming
   headings or assuming a section is stale because of its date. Skimming titles produces
   confident-sounding deletions of things that still mattered.
2. **Extract before you delete.** Never remove a verbose/raw entry until anything unique in it —
   a specific gotcha, a non-obvious rationale, an exact reproduction step — has been folded into
   whatever summary replaces it. Losing the specific fact behind a vague summary is worse than
   leaving the verbose entry in place.
3. **When in doubt, don't merge.** Two entries that look similar but differ in conclusion, scope,
   or context stay separate. Redundancy is cheap; silently erasing a real distinction is not.
4. **New understanding gets a new entry, not a rewrite of the old one.** If a past decision turns
   out to be wrong or incomplete, add a dated correction/update rather than editing the original
   in place — the history of *why* something changed is itself useful.
5. **Don't review on every write.** Light append-as-you-go is fine continuously; a full
   consolidation pass (re-triage, dedupe, restructure) is only worth doing once enough has
   accumulated that the file is hard to scan in one read — not after every single addition.
6. **Manual override always wins.** If the person you're working with says "keep this" or "this
   can go," that instruction overrides any heuristic here, permanently.

## Quick heuristic
| Signal | Action |
|---|---|
| Referenced/needed again after it was written | Protected — keep verbatim |
| Useful once, unlikely to recur, but non-obvious | Consolidate into a summary, drop the raw form |
| Superseded by a later entry | Replace, but only after confirming nothing unique is lost |
| Never actually used since written | Cut |
| Genuinely uncertain | Leave it — don't force a decision |
