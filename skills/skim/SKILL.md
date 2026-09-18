---
name: skim
description: Read a project's .index/ before its files. Use whenever a task will read files in a folder that has .index/README.md, whether notes, documents or code, even if the user doesn't mention the index. Not for folders without .index/.
---

# Skim

A folder with `.index/README.md` has an index written by the `checkpoint` skill: one extremely concise summary per file, what it's generally about and the exceptions. Skim means reading the entries before the files, and opening a file only when it seems relevant. It is similar to other ideas involving progressive disclosure.

## The rule

1. Read `.index/README.md` first: the folder table and the build date.
2. Read the index files for the folders the task needs, all in one command. The cost of deciding is turns, not the size of the index, since every call re-sends the whole context.
3. Open a file when its entry seems relevant, and open the chosen files in one command. When one line is needed, grep for it instead.
4. Once the files that matter are named, grep the folder for their names. A file that mentions them can bear on the task when its own entry doesn't show it.
5. The entries are a model's summaries. When a question turns on a file's exact wording or numbers, open the file.
6. Files the task names, or that another skill says to read whole, are read whole. Skim governs the rest.
7. Never write to `.index/`. If a file is newer than its entry, say so and suggest a checkpoint.

## Reporting

End the task with one line: index files read, files opened whole, tool calls. That line is how the user measures the saving.
