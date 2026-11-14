# LP6 Grid Demo: Driftless Cycle Co. (video recording version)

One site, one page per discussion topic, the same layout as the LP4 and LP5 demos. Every page starts incomplete or flawed on purpose, and you build or fix it live while recording.

| Page | Topic | What the starter looks like | What you build or fix |
|---|---|---|---|
| `index.html` (Home) | DT 6.1 CSS Grid fundamentals | One long column. The markup is finished, there is no grid | Three-column grid, `gap`, `grid-column: 1 / -1`, `grid-row: span 2`, `repeat()`, `auto-fill` then `auto-fit`, a collapse query |
| `products.html` (Products) | DT 6.2 Grid areas and named regions | One long column | `grid-template-areas` map, `grid-area` per element, a different map at 900px, `min-height: 100vh` |
| `about.html` (About Us) | DT 6.3 Checkpoint 2 build session | A Checkpoint 2 style page with eight planted problems | The six-step audit: find each problem and fix it |

## Folders
- `starter/` is the site to open in VS Code and work on. Each page has its own stylesheet (`css/6-1.css`, `6-2.css`, `6-3.css`). `css/base.css` is shared and already finished.
- `finished/` is the same site with everything done. Use it to check your work or as a fallback if a take goes wrong.
- `steps/6-1/`, `steps/6-2/`, `steps/6-3/` hold the stylesheet as it should look after each step (`step3.css` = the file after step 3). Copy one over `css/6-x.css` to jump to that point.
- `STEPS_6.1.md`, `STEPS_6.2.md`, `STEPS_6.3.md` are the recording guides. Each follows the LIVE DEMO steps on that deck.

## Same rules as the earlier demos
- Every page has the skip link in the body and its CSS in `base.css`.
- Every page has the viewport meta tag, because this lesson is not about that.
- No fonts are needed. The site uses the system font stack.
- The reduced-motion reset appears only in `6-3.css`, as one of the planted problems (DT 3.3 and later).
- The nav is the shop's own nav: Home, Products, About Us go to the three pages.

## How this builds on LP5
Grid is new here. The flexbox you already taught (LP5) appears inside the grid regions: the nav links and the bike cards in `products.html`, and the crew cards in `about.html`. That is the DT 6.3 pattern: Grid for the page, Flexbox inside each region.

## What I checked, and what I did not
Checked: all six HTML files pass the Nu validator with no errors; every CSS file parses and its declarations are valid (css-tree); axe-core is clean on the finished pages at 320px and 1200px, and finds only the planted contrast problem on the `about.html` starter; every layout number quoted in the guides was measured in Chromium at the stated width.

Not run: the W3C CSS validator and Lighthouse (I cannot reach them from here), and the real OS Reduce Motion setting (I used browser emulation only). Run those live. DT 6.3 says the Reduce Motion test must use the actual OS setting, and that matters on camera.
