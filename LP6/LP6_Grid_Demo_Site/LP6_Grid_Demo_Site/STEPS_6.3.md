# 6.3 Live Demo: Checkpoint 2 Build Session and Audit (`about.html`, `css/6-3.css`)

DT 6.3 has no build steps of its own. Its demos are the Flexbox-or-Grid exercise (slide 3), the six-step audit (slide 5), the "most common failures" list (slide 6) and the submission walkthrough (slide 7). This page turns those into one recording. `about.html` is a Checkpoint 2 style page with eight planted problems, one for each failure in the deck. You audit it, find each one, and fix it. Open `starter/about.html` and `css/6-3.css`.

## Part A: Flexbox or Grid? (slide 3 demo cue)
Open `finished/about.html` (or the starter after fix 1). Point at each region and ask the class. Answers:

| Point at | Answer | Why |
|---|---|---|
| The whole page: header, nav, sidebar, main, footer | Grid | Rows and columns at once. `grid-template-areas` names the neighborhoods |
| The row of nav links | Flexbox | One axis, a row that wraps |
| The row of crew cards in main | Flexbox | One axis, wrapping with `flex: 1 1 200px` |
| The service boxes on `index.html` (from 6.1) | Either | We used Grid there to teach `auto-fit` and `minmax()` |

Say the deck's line: "Grid decides where the neighborhoods are. Flexbox decides how the furniture is arranged inside each room."

## Part B: the six-step audit on the starter (slide 5)
Narrate each step as a speed audit. What each step finds on this page:

| Audit step | What happens on the starter |
|---|---|
| 1. W3C HTML validate | Passes. The Nu validator found no errors in the starter. Valid HTML is not the same as good HTML: the flaws below are all valid |
| 2. W3C CSS validate | Passes. Run it live at jigsaw.w3.org (I could not run it here). The CSS parses and every declaration is valid |
| 3. Contrast check | Fails. The role lines (`.meta`) are `#8a8a8a` on white, about 3.5 to 1. AA needs 4.5 to 1. axe-core finds three nodes. Paste the colors into WebAIM to show it |
| 4. Lighthouse on the live URL | Run it on GitHub Pages, not localhost. Expect it to flag the same contrast problem. I could not run Lighthouse here, so I cannot tell you the score |
| 5. Keyboard test | Mouse down. Tab to a crew card link: no focus ring at all (measured: `outline: none`). Cards also do not lift on keyboard focus, only on hover. In the nav, About Us has no current-page marker |
| 6. Reduce Motion test | Turn on Reduce Motion in the OS and reload. The cards still fade in over 0.6s and the hover lift still takes 0.3s. With the reset in place (measured with browser emulation) both drop to 0.01ms |

Also look at it at 320px: the sidebar takes 220px and main is squeezed to about 123px wide, and the page scrolls sideways. At 900px and 1440px it looks fine. This is why you test at 320px.

## Part C: fix it (the CSS after each fix is in `steps/6-3/stepN.css`)

| # | Failure from slide 6 | How you find it | Fix | File |
|---|---|---|---|---|
| 1 | Grid with only `grid-template-columns` and no template areas, no mobile layout | Read the CSS. `grid-column: 2; grid-row: 3`: line numbers, no map. Test at 320px | Replace with the mobile-first `grid-template-areas` map, five `grid-area` lines and a `min-width: 900px` map, exactly as in 6.2 (`step1.css`) | `css/6-3.css` |
| 2 | `transition: all` | Read the CSS. Computed `transition-property` is `all`, and it would animate the focus ring | `transition: transform 0.25s ease-out, box-shadow 0.25s ease-out;` (`step2.css`) | `css/6-3.css` |
| 3 | Missing `:focus-visible` on one element type | Keyboard test: no focus ring on the card links, and cards only react to hover | Delete the `.card a:focus { outline: none; }` rule and change `.card:hover` to `.card:hover, .card:has(:focus-visible)` (`step3.css`) | `css/6-3.css` |
| 4 | Contrast | Contrast check and axe | `.meta { color: var(--muted); }`, about 7.7 to 1 (`step4.css`) | `css/6-3.css` |
| 5 | `prefers-reduced-motion` not in the stylesheet | Reduce Motion test | Add the global reset at the end (`step5.css`) | `css/6-3.css` |
| 6 | Image without meaningful alt text | By eye. `alt="image123.jpg"` | `alt="The Driftless Cycle Co. shop on Main Street in Viroqua, with a green sign and two bikes parked out front"` | `about.html` |
| 7 | Vague link text | By eye. `click here` | Change it to `Browse this season's bikes` | `about.html` |
| 8 | `aria-current` not set on this page | Inspect the nav | Add `aria-current="page"` to the About Us link | `about.html` |

After each CSS fix, save and reload. At the end, run the audit again quickly: contrast clean, keyboard focus ring visible on the card links, Reduce Motion instant, 320px one column.

## Part D: what Lighthouse cannot catch (slide 8 honest framing)
Fixes 6, 7 and 8 are the point. After you fix only the CSS, run axe or Lighthouse's accessibility audit and see the contrast problem go away. The alt text `image123.jpg`, the link text `click here`, the missing `aria-current` and the removed focus outline were never flagged: axe-core, which Lighthouse's accessibility checks are built on, reported only the contrast problem on the starter. A score of 90 or above is necessary, not sufficient. The keyboard test and your own eyes catch the rest.

## Part E: the submission walkthrough (slide 7, a live demo with no starter code)
1. `git add .`, then `git commit -m "Checkpoint 2 final — all requirements complete"`, then `git push`.
2. Wait 2 to 3 minutes for GitHub Pages to redeploy.
3. Run Lighthouse on the live GitHub Pages URL, not localhost. Screenshot the result.
4. Blackboard: Checkpoint 2 Project, open the text entry field.
5. Paste the live site URL (`username.github.io/repo-name`).
6. Paste the repository URL (`github.com/username/repo-name`). Both URLs are required, because the repository shows the commit history, which is graded.
7. Add the Code Journal (three questions) and the Lighthouse screenshot.
8. Submit and confirm the receipt.

## Not run
Lighthouse, the W3C CSS validator, and the real OS Reduce Motion setting (I used browser emulation).
