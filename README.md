# Recipe Cards

Recipe screenshots turned into clean, printable HTML cards by the `recipe-card` Claude skill.

- `index.html` — directory page listing every recipe (works as a GitHub Pages site)
- `recipes/` — one self-contained HTML card per recipe (open in a browser; print to save as PDF)
- `skill/recipe-card/` — the source of the `recipe-card` skill that generates these cards (`SKILL.md` + `assets/template.html`)
- `skill/recipe-card.skill` — the packaged skill (a ZIP of `skill/recipe-card/`), regenerated after any source edit

## Hosting with GitHub Pages

1. Push this repository to GitHub.
2. In the repo: **Settings → Pages → Source: Deploy from a branch**, branch `main`, folder `/ (root)`.
3. The directory will be live at `https://<username>.github.io/<repo>/`.

## Adding a new recipe

1. Drop the new card into `recipes/`.
2. Add a card block for it near the top of the grid in `index.html` (there's a comment in the file showing the pattern) and bump the recipe count in the footer.
3. Commit and push.

The recipe-card skill includes this as its final publishing step, so when a GitHub connection is available in the Claude conversation it happens automatically; otherwise the card is delivered in-chat and flagged as not yet uploaded.
