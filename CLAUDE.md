# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

`ember-memory` is **not application code** — it's a content/spec repository for a personal emotional-memory
system shared by two "subjects," 渡渡 (Dodo) and 初尘 (Chuchen). It holds:

- The design rationale for that memory system (`FOUNDATIONS.md`).
- Versioned, dated snapshots of a Claude Code **Skill** (`memory-hygiene`) that performs the actual
  curation/cleanup of the memory store described in the foundations.

There is no build, lint, test, or package tooling here (no `package.json`, no CI config, no Cursor/Copilot
rules) — every file is Markdown. "Development" in this repo means editing or versioning these Markdown
documents, not writing or running code.

## Repository layout

```
README.md                          one-line project description
FOUNDATIONS.md                     the six design pillars (see below) — the source of truth for *why*
                                    the memory system and its skill behave the way they do
memory-hygiene/                    ARCHIVED history of the memory-hygiene skill, v2.2.0 → v2.5.0,
                                    migrated in from a different repo ("dodo-when"). Treat as frozen
                                    historical record — don't retroactively edit these.
skills/memory-hygiene/             ACTIVE/current location for the skill going forward, v2.5.0 → v2.6.0+
```

Each version lives in its own dated folder: `<repo-root>/.../<name>/YYYY-MM-DD_vX.Y.Z/SKILL.md`. New
revisions are added as a **new folder**, never by editing a previous version's `SKILL.md` in place — this
is consistent across the whole git history (see the `重组` ("reorganize") commits that moved loose dated
files into folders).

### Known inconsistency to be aware of

`memory-hygiene/2026-06-15_v2.5.0/SKILL.md` and `skills/memory-hygiene/2026-06-15_v2.5.0/SKILL.md` are
**two different lineages** of the same version number with materially different content (the root copy is
the longer, more elaborate "migrated" version; the `skills/` copy is the shorter rewrite that v2.6.0
continues from). When asked about "the current skill," use the `skills/memory-hygiene/` lineage, not the
root `memory-hygiene/` one.

Also note that later version files document **deltas, not full snapshots**: `skills/memory-hygiene/2026-06-21_v2.6.0/SKILL.md`
is only ~28 lines and contains just the `vX.Y.Z新增` ("new in this version") section plus a restated
title/philosophy — it does not repeat unchanged sections like 五步流程 (five-step process) or 白名单
(whitelist) from v2.5.0. To understand the *complete* current behavior of the skill, read the latest full
version together with any subsequent delta-only versions, not just the newest file alone.

## SKILL.md conventions

Every `SKILL.md` uses Claude Code's skill frontmatter:

```yaml
---
name: memory-hygiene-skill
description: >-
  <what it does, in Chinese> Triggers: <comma-separated natural-language trigger phrases>
license: MIT
metadata:
  author: 渡渡
  version: X.Y.Z
---
```

The `description` field embeds a `Triggers:` line listing the phrases (in Chinese) that should cause this
skill to be invoked in conversation — this is functional, not decorative. Keep it when editing.

## Core design vocabulary (from FOUNDATIONS.md)

All memory content and skill logic in this repo is built on six pillars defined in `FOUNDATIONS.md`. Skill
behavior should stay consistent with these when modified:

1. **双主体标记 (dual-subject tagging)** — every memory entry is tagged `subject: chuchen | dodo | us`; the
   same event can have separate entries per subject.
2. **事件关联网络 (event relation graph)** — memories link to each other (`link_memories`) rather than
   existing as isolated records.
3. **热度浮现权重 (heat/salience weighting)** — surfacing is driven by non-linear "heat" (how often a memory
   is revisited/discussed), not linear time decay.
4. **可沉降/基石分类 (sedimentable vs. protected)** — most memories can decay ("sink") over time;
   a fixed set of foundational memories never decay.
5. **双向批注 (bidirectional annotation)** — both subjects can annotate/reply on the same diary entry.
6. **手动热度调节 (manual heat override)** — either subject can manually override decay/heat at any time;
   automated decay never has unilateral authority.

The `memory-hygiene` skill is the operational implementation of pillars 3–4 (and parts of 6): it defines how
to write new memories, deduplicate, classify into 精档/沉降 (precious/sedimentable), and decay them over time.

## Conventions when editing this repo

- **Language**: content is written primarily in Simplified Chinese, with English used only for YAML keys,
  skill/file names, and a few borrowed terms (`precious`). Preserve this — don't translate memory or skill
  content to English.
- **Terminology is load-bearing**: terms like 热度 (heat), 沉降 (sedimentation/decay), 白名单 (whitelist),
  precious, 三分类 (the three memory facets: 事件/进度, 操作经验, 情绪与感受) recur across versions with
  specific meanings defined in `FOUNDATIONS.md` and the `SKILL.md` files — don't redefine them casually when
  drafting a new version.
- **Versioning, not in-place edits**: when changing skill behavior, add a new `YYYY-MM-DD_vX.Y.Z/SKILL.md`
  folder (bump the `metadata.version` and the date) rather than mutating an existing version's file.
- **Commit messages** in this repo's history are short, prefixed, and largely in Chinese
  (`feat:`, `migrate:`, `重组:`, `chore:`, or a bare `vX.Y.0: <summary>`) — follow that style for skill
  version bumps and reorganizations.
