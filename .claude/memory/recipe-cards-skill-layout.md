---
name: recipe-cards-skill-layout
description: Skill source of truth lives unpacked at skill/recipe-card/; the .skill zip is a regenerated artifact
metadata: 
  node_type: memory
  type: project
  originSessionId: 7eaf0074-07c0-4833-9b55-3997460716d6
---

Decision (2026-07-18): the `recipe-card` skill's editable source lives at `skill/recipe-card/` (SKILL.md + assets/template.html), following the anthropics skill-creator anatomy. `skill/recipe-card.skill` is a packaged ZIP build artifact — never hand-edited, always regenerated from the source folder after edits (`zip -rFS` one-liner in CLAUDE.md, or skill-creator's `package_skill.py` which also validates frontmatter). The old root-level `recipe-card.skill` was removed when this structure landed.

The skill is also available locally as `/recipe-card` via a symlink `~/.claude/skills/recipe-card` → `/Users/nikesh/Code/recipe-cards/skill/recipe-card` (added 2026-07-18). Edits to the repo source are live immediately for local Claude Code use — but the `.skill` zip must still be regenerated for distribution/upload elsewhere.

Related: [[recipe-cards-hosting]], [[record-build-decisions]]
