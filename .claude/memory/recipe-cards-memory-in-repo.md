---
name: recipe-cards-memory-in-repo
description: Memory files live in the repo at .claude/memory/, symlinked from the harness path, so they sync across laptops
metadata:
  type: project
---

Decision (2026-07-18): Claude Code's per-project memory for recipe-cards lives **in the repo** at `.claude/memory/` so it's versioned on GitHub and shared across Nikesh's machines. The harness location `~/.claude/projects/-Users-nikesh-Code-recipe-cards/memory` is a symlink to the repo folder. On a new machine, clone the repo and recreate the symlink (setup snippet in CLAUDE.md under "Working on a new machine"). Memory files are public (public repo) — keep anything sensitive out of them. Commit and push memory changes like any other file.

Related: [[record-build-decisions]], [[recipe-cards-hosting]]
