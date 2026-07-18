---
name: recipe-cards-art-deco-style
description: House style is Art Deco (obsidian/gold) everywhere, including print — an explicit choice
metadata:
  type: project
---

Decision (2026-07-18): the whole site — index AND all recipe cards, **including their printed output** — uses an Art Deco design system: obsidian background (#0A0A0A), near-black card sheets (#101010), charcoal panels (#141414), metallic gold accents (#D4AF37), champagne cream text (#F2F0E4). Nikesh explicitly chose "everything, including print" over keeping print ink-friendly, so cards print dark full-bleed — do not revert print styles to light without being asked. CSS variable names stay the same as the old palette (`--cream`, `--accent-soft`, `--ink`, `--accent`, `--line`) with remapped values. Display type Marcellus (Georgia fallback), body Josefin Sans (Futura/Century Gothic fallback); recipe cards stay self-contained so only the hosted index loads Google Fonts. Ornaments: double-frame sheets, gold corner brackets, diamond bullets, square gold step badges, Roman numerals (marinades are No. I–V, footer count is IX). The skill's template.html was restyled to match and the .skill repackaged. Full token/ornament spec is in CLAUDE.md "Card conventions".

Related: [[recipe-cards-index-categories]], [[recipe-cards-skill-layout]], [[record-build-decisions]]
