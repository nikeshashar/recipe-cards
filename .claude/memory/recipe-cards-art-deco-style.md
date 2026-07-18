---
name: recipe-cards-art-deco-style
description: House style is Art Deco (obsidian/gold) everywhere, including print — an explicit choice
metadata:
  type: project
---

Decision (2026-07-18): the whole site — index AND all recipe cards, **including their printed output** — uses an Art Deco design system: obsidian background (#0A0A0A), near-black card sheets (#101010), charcoal panels (#141414), metallic gold accents (#D4AF37), champagne cream text (#F2F0E4). Nikesh explicitly chose "everything, including print" over keeping print ink-friendly, so cards print dark full-bleed — do not revert print styles to light without being asked. CSS variable names stay the same as the old palette (`--cream`, `--accent-soft`, `--ink`, `--accent`, `--line`) with remapped values. Display type Marcellus (Georgia fallback), body Josefin Sans (Futura/Century Gothic fallback); recipe cards stay self-contained so only the hosted index loads Google Fonts. Ornaments: double-frame sheets, gold corner brackets, diamond bullets, square gold step badges, Roman numerals (marinades are No. I–V, footer count is IX). The skill's template.html was restyled to match and the .skill repackaged. Full token/ornament spec is in CLAUDE.md "Card conventions".

Update (2026-07-18, later): every page also has a **light Art Deco variant** (ivory #EDE7D8, sheet #FAF7EE, antique gold #8C6D1F) as a `:root[data-theme="light"]` override block, toggled by a fixed `.theme-toggle` button; persisted in localStorage key `recipe-cards-theme`, shared across index and cards on the same origin. Dark stays the default everywhere; light applies to print too (ink-friendly when chosen). Template/skill updated so generated cards include the toggle.

Related: [[recipe-cards-index-categories]], [[recipe-cards-skill-layout]], [[record-build-decisions]]
