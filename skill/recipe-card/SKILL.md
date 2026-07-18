---
name: recipe-card
description: Turn a screenshot or photo of a recipe into a clean, printable recipe card showing the dish title, ingredients, and step-by-step method. Use this whenever the user uploads one or more images of a recipe (a screenshot from a website, Instagram/TikTok, a cookbook photo, a note, etc.) and wants it tidied up, extracted, reformatted, made printable, or turned into a "card", even if they don't say the word "skill". Handles a single recipe split across several screenshots, several recipes in one image set (one card each), ingredient-only posts like marinades, and requests to scale servings. Also trigger on phrases like "make a recipe card", "clean up this recipe", "extract this recipe", "turn this into a printable recipe", or "a card for each".
---

# Recipe Card

Convert a recipe shown in uploaded image(s) into a styled, printable HTML recipe card. Each card has a **dish title**, the **ingredients**, and the **method** (how to cook). Optional extras — servings, prep/cook time, macros — are shown only when the image actually contains them.

## Workflow

1. **Read every image** carefully. Screenshots are visible directly in context, so no OCR tooling is needed.
2. **Stitch and order** the screenshots into one continuous recipe (see below). Work out how many distinct recipes are present.
3. **Extract** title, ingredients, method, and any metadata/macros per recipe, following the fidelity rules.
4. **Choose a layout** (standard, ingredient-only, or multi-page) and fill the card by reproducing the style of `assets/template.html`.
5. **Save** to `/mnt/user-data/outputs/<dish-name>-recipe-card.html` and present it. For several recipes, make one card per recipe — either separate files or one file with each card on its own page.
6. **Tell the user, briefly, about any judgement calls** you made: inferred titles, scaling, flagged glitches, clutter removed, missing methods.
7. **Publish to the user's GitHub recipe directory** (see "Publishing to GitHub" below).

## Reading and stitching multiple screenshots

People often upload a recipe in pieces, scrolled top-to-bottom but **not always in upload order**.

- Order the images by their content, not their filenames. Use overlapping text, running step numbers, and section headings ("Ingredients" → "Method") to find the true sequence.
- Screenshots usually **overlap** at the edges; merge the duplicated text rather than repeating it.
- A single recipe can also include a separate photo of the finished dish or the macros — treat those as part of the same recipe.

## How many recipes?

- One title with one ingredient list and one method = **one card**.
- An image set containing several clearly separate recipes (each with its own name and ingredient list, e.g. "1. Hot Honey Harissa … 2. Cilantro Lime …") = **one card per recipe**. Keep them in the source order.
- When in doubt, prefer the reading that matches how the user phrased the request ("a card for each" → several cards).

## Extraction fidelity — the most important part

The card must faithfully represent the recipe. A missing step or a changed quantity ruins a dish, so accuracy beats polish.

- **Never invent content.** Don't add ingredients, steps, quantities, times, servings, or macros that aren't in the image. Don't "improve" or round the recipe.
- **Preserve quantities and units exactly** ("1½ cups", "200g", "2 tbsp"). If the source gives **two units** (e.g. "2 cups all-purpose flour 260g"), keep both.
- **Keep the original order** of ingredients and steps. Don't merge, split, or reorder.
- **Preserve groupings.** If ingredients sit under sub-headings ("For the sauce", "Marinade", "Salad"), keep them as ingredient groups. For multi-part recipes (cake + frosting + syrup), group both the ingredients and the method by component, numbering each component's steps from 1 as the source does.
- **Ingredients buried in prose:** when a recipe writes quantities inside the method instead of as a list (common on social media), extract them into a proper grouped ingredient list, then keep the method steps too. This is reorganising stated content, not inventing.
- **Metadata and macros are opt-in.** Show a servings/time chip or a macros block only if those figures appear in the image. If no serving count is given, don't invent one — say so in a footnote if useful.
- **Title:** use the dish name shown. If there's none (the post starts mid-recipe), infer a short, plain descriptive name from the components and tell the user you inferred it.
- **Attribute the source** when the screenshot shows it (handle, site, byline) in the footer.

### Obvious typos and OCR/autocorrect glitches

- Fix a glitch **only when the source itself confirms the intended word** (e.g. "monkfrit" on one screen, "monkfruit" on another → use "monkfruit").
- If a word is clearly garbled but the intended meaning **isn't confirmed anywhere** (a classic is autocorrect turning a spice into something nonsensical), **do not guess a replacement** — that's inventing. Keep it verbatim, mark it on the card with an asterisk, and add a short on-card footnote explaining it looks like an autocorrect slip so the reader can substitute. Put the flag on the card itself, not only in chat, because cards get printed and shared without the conversation.

### Scaling to a different quantity

When the user asks to scale (e.g. "use 6 chicken thighs for each"):

- Scale cleanly when the base is a **count** you can divide into (4 thighs → 6 = ×1.5). Apply the same factor to every measured ingredient and add a chip/note saying it was scaled.
- **Flag weight-vs-count mismatches** instead of fabricating a conversion. If a recipe is written by **weight** (e.g. "2 lb chicken") and the user asks in **counts** (6 thighs), don't invent a thigh-to-pound figure. Note the original base, point out that the requested amount is roughly equivalent (or not), and leave the marinade/sauce amounts unchanged unless a clean factor exists.
- Items that don't scale numerically — "a pinch", "a dash", "to taste" — stay as written; note that they should be adjusted to taste.

## Imperfect screenshots and clutter

Screenshots are often cropped, low-resolution, or full of app chrome.

- **Ignore non-recipe clutter:** ads (e.g. travel/shopping banners, Amazon/sponsored boxes), "jump to recipe" buttons, like/save counts, reader-mode banners ("1 item hidden"), navigation, ratings, author bios, and comment threads. Extract only the recipe.
- **If part of the recipe is cut off or unreadable**, transcribe what you can, mark the gap on the card (e.g. "[unreadable]"), and tell the user what was missing so they can re-upload.
- **If there's no recipe at all**, don't fabricate one — say what you see and ask for a recipe image.
- **Blog "tips" sections** aren't core recipe steps. You may include them as a short, clearly-labelled "Tips" section at the end if they're present and useful, but never let them crowd out the ingredients and method.

## Recipes with no method (marinades, spice blends, ingredient lists)

Some posts list only ingredients. Don't fabricate cooking steps.

- Make an ingredients-led card and add a brief, clearly-generic "How to use" note (for a marinade: combine, coat, marinate, then cook through to a safe temperature). The only specific figure you may add is a food-safety cooking temperature, presented as general guidance.
- State on the card that the method is general because the source listed ingredients only.

## Output format and layouts

Default output is a **single self-contained HTML file** (inline styles, no external assets) so it renders in-app, prints cleanly, and saves to PDF from the browser's print dialog. Reproduce the look of `assets/template.html`; the colour palette and components there are the house style. Pick the layout that fits:

- **Standard card** (most recipes): header with title and optional chips, ingredients in a tinted sidebar (grouped if needed), method as numbered steps beside it. Keep it to one page; tighten spacing before spilling over.
- **Ingredient-only card** (marinades etc.): make ingredients the hero, often in two columns, with the short "How to use" note below.
- **Multi-page document** (large multi-component recipes): it's fine to run to several pages. Use a continuous sheet, group by component, and add print rules so a step or ingredient group isn't split across a page break (`break-inside: avoid`). Only go multi-page when the recipe genuinely needs it or the user says it's fine.

### Keeping everything on the page (this is mandatory, not optional)

The single most common defect is content — usually the ingredient checklist or the second column — running off the right edge on a narrow screen. It happens when the card is sized for a fixed A4 width while being viewed on a phone. Avoid it with these rules, all of which are already wired into `assets/template.html`:

- **Fluid on screen, fixed only in print.** Give the page `width: 100%; max-width: 210mm` (never a bare fixed `width` like `210mm`). Lock the exact A4 sheet (`width: 210mm; min-height: 297mm`) **only inside `@media print`**.
- **Every column must be allowed to shrink.** Grid/flex children default to `min-width: auto`, which refuses to shrink and forces overflow. Use `minmax(0, …)` for every grid track and set `min-width: 0` on the column elements. A fixed-width sidebar (e.g. `66mm`) paired with a `1fr` method column **must** use `minmax(0, 1fr)` for the method, or one long line pushes the page sideways.
- **Stack on narrow screens.** Add a media query (around `max-width: 560px`) that collapses the two-column body to a single column, then restore two columns in `@media print`. This is what guarantees nothing spills off a phone screen while the printout stays two-column.
- **Let text wrap.** Put `overflow-wrap: anywhere` on titles, ingredient items, and method items so a long unbroken token can't widen a column.
- **Responsive multi-column ingredient lists.** For the ingredient-only/marinade layout, do **not** rely on a bare `column-count: 2` (its columns don't collapse and can sit off-screen). Use a self-collapsing grid instead, e.g. `display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 190px), 1fr)); gap: …;` with `break-inside: avoid` on each group, so it shows two columns when wide and one when narrow.
- **Responsive padding and title.** Use `clamp()` for page padding and the `h1` size so margins don't swallow a small screen and the title never overflows.

Before finishing, sanity-check the card at a narrow width: the checklist and method should wrap and stack, with nothing clipped or scrolled off to the right.

Produce a different file format only if asked: **PDF** (render the HTML to PDF) or **Word/.docx** (use the docx skill with the same title/ingredients/method structure).

For several recipes, default to **one file with each card on its own printable page** (page break between), and offer to split into separate files.

## Template usage

`assets/template.html` is a complete worked example, not a fill-in form. Replicate its layout and CSS, then adapt: duplicate `<li>`s freely, add `.ingredient-group` headings only when there are sub-sections, show macro chips only when macros are given, delete the meta row if there's no metadata, and use the footnote component for any flagged glitch. The muted unit style (`.g`) is for second units like gram weights.

## Quick examples

- **One blog recipe, several screenshots, lots of ads** → stitch in reading order, strip the ad boxes, one standard card; if it's a big layered bake with sub-recipes, group by component and let it run to two pages.
- **A post listing five marinades** → five ingredient-only cards (one per marinade), original order; scale only where the chicken base is a clean count, flag weight-vs-count cases, generic "How to use".
- **A reel where quantities are written into the steps** → pull them into a grouped ingredient list, keep the steps as the method, infer a title and say so.

## Publishing to GitHub

The user keeps their recipe cards in a GitHub repository (default name: `recipe-cards`, cards in `recipes/`). They maintain the directory/index page themselves — do not edit it. After presenting a finished card:

1. **Check for GitHub access** (a GitHub tool/connector in the conversation, or network + credentials in the code environment). If none is available, **do not skip silently**: tell the user the card was delivered but NOT uploaded to their recipe repo, so they can add it themselves.
2. **Upload the card** to `recipes/<dish-name>-recipe-card.html` with a sensible commit message like "Add <dish name> recipe card", and remind the user to add it to their directory page.
3. **Confirm** what was pushed, with the repo path.

Never fabricate an upload: if any step fails, say exactly what was and wasn't pushed.
