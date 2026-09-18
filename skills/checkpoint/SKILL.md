---
name: checkpoint
description: Write or refresh a project folder's .index/, one extremely concise summary per file, on the user's command only. Use when they say checkpoint, or ask to build, refresh or reset the index, or say they've added or changed many files. Never run unasked.
---

# Checkpoint

A checkpoint writes `.index/`: one entry per file in the project, so the `skim` skill can read the entries before it opens files. A model reads each file whole and writes its entry. Nothing outside `.index/` is touched.

## Steps

1. Find the project root: the folder the user names, or the one that holds `.index/`. If more than one is in reach and they name none, ask.
2. List the files with their modified times. Skip hidden folders, `.index/` itself, and anything matched by `.index/ignore` (one glob per line) if it exists.
3. Read the existing `.index/` if there is one. Keep every entry whose modified time still matches its file. Summarize only the files that are new or changed; on a reset, all of them.
4. Read each file to summarize whole and write its entry in the format below. When there are more than a handful, hand them to a subagent in batches, never one subagent per file.
5. Write `.index/README.md`: the build date, one row per folder (folder, number of files, one clause on what the folder holds), then the entries for files at the root. Write `.index/<folder>.md` for each folder that has files, with that folder's entries. Remove index files for folders that no longer exist.
6. Report how many files were summarized, how many kept, and which folders changed.

## The entry

```
## path/from/root.md
- 3,100 words · 2026-09-18
- Generally: what questions the file can answer, at the level of its sections, in one sentence.
- Except: what the file holds that its name wouldn't predict, and what it lacks that its name would predict (a history, a how-to, numbers, code). One clause each, or drop the one that's empty.
```

Describe the file, not its subject. Nothing the filename already says, nothing about style, format or source, no praise. Both lines together under forty words. A reader decides from the entry whether to open the file, so what's missing is as useful as what's there. The entry is a model's words, so it never implies exact wording.
