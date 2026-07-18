---
name: recipe-cards-index-categories
description: Index has recipe-type filter chips; marinades split into per-recipe cards shown only under the Marinades filter
metadata: 
  node_type: memory
  type: project
  originSessionId: 7eaf0074-07c0-4833-9b55-3997460716d6
---

Decision (2026-07-18): `index.html` has filter chips (All / Chicken / Bowls / Marinades / Desserts) driven by `data-tags` on each card, with vanilla inline JS and `#<tag>` hash deep-links; chips are hidden in print. The five chicken marinades were split into individual self-contained cards in `recipes/` (built to the current fluid/print layout rules, content copied verbatim). They carry `data-sub="marinades"`, so they appear only when the Marinades chip is selected; the combined five-page file (`chicken-marinades-recipe-cards.html`) stays as the single "All"-view entry and the print-all-five option. Footer counts recipes, not files (9 recipes). New type = new chip + tags; convention documented in CLAUDE.md and an index.html comment.

Related: [[recipe-cards-hosting]], [[record-build-decisions]]
