# LP6 Formative Lab: Live Demo Guide (Wisconsin State Fair Homepage)

Build the whole homepage live, in 10 steps. Each `stepNN/` folder is the finished state AFTER that step, so you can jump in if you get lost or want to show the "before". `finished/` = step 10. The HTML is the same in every step; only `style.css` grows. Following the assignment wording, each layout redefines `grid-template-areas` inside its own media query: mobile in `@media (max-width: 899px)`, desktop in `@media (min-width: 900px)`. No overrides.

Lab requirements covered: named grid areas (header, nav, main, sidebar, footer), two columns at 900px, single column stack on mobile, Flexbox inside at least two regions (this demo uses three), semantic landmarks, validation.

| # | Say / do | CSS you type |
|---|---|---|
| 1 | Open `index.html` with empty CSS. Point out the five landmarks: `header`, `nav`, `main`, `aside`, `footer`, all direct children of `<div class="page">`. No `div` soup. Show the skip link and `id="main-content"` | none |
| 2 | Reset + skip link (hidden until focus). Press Tab once to prove it | `box-sizing: border-box`, `body` font, `img { max-width: 100% }`, `.skip-link` + `.skip-link:focus` |
| 3 | The grid container. Give each region its `grid-area`. Then write the MOBILE layout inside `@media (max-width: 899px)`: one column and five quoted strings, one name per row. **Open DevTools responsive mode and keep the window under 900px for steps 3 and 4.** At 900px or wider the regions pile on top of each other until step 5, which makes a good "why do we need the desktop query" moment | `.page { display: grid; gap: 1rem; ... }` then `.site-header { grid-area: header; }` etc. then `@media (max-width: 899px) { .page { grid-template-columns: minmax(0, 1fr); grid-template-areas: "header" "nav" "main" "sidebar" "footer"; } }` |
| 4 | Color-code the regions so students can SEE the areas | background + padding per region |
| 5 | Desktop. A second media query with its own `grid-template-areas`: two columns, main beside sidebar. Widen the window past 900 and watch it snap into place | `@media (min-width: 900px) { .page { grid-template-columns: minmax(0, 1fr) 18rem; grid-template-areas: "header header" "nav nav" "main sidebar" "footer footer"; } }` |
| 6 | Flexbox in region 1 (header quick links) and region 2 (nav) | `display: flex; flex-wrap: wrap; gap: ...` on `.quick-links` and `.site-nav ul` |
| 7 | Flexbox in region 3 (card row in main) | `.cards { display: flex; flex-wrap: wrap; gap: 1rem; }` `.card { flex: 1 1 220px; }` |
| 8 | Images: hero crops cleanly at every width | `aspect-ratio: 16 / 9; object-fit: cover;` |
| 9 | Hover and `:focus-visible` states. Tab through the page | `a:focus-visible { outline: 3px solid #ffbf47; outline-offset: 3px; }` |
| 10 | Validate HTML and CSS (zero errors), resize 320 to 1200, Tab through | none |

## Talking points (the "why")
- **Grid on the wrapper, not on `body`.** The five regions must be DIRECT children of the grid container. That is why `.page` wraps them. The skip link sits outside it.
- **Names are the layout.** Each string in `grid-template-areas` is one row, and every row needs the same number of names. Repeating a name ("header header") makes it span columns. Typing `sidebar` where the CSS says `side` quietly breaks the layout.
- **Each layout is its own map, inside its own media query.** Same five names, different map: mobile stacks them, desktop puts main beside the sidebar. No `grid-column` overrides fighting each other. Show this by changing only the strings.
- **`minmax(0, 1fr)` instead of plain `1fr`.** `1fr` really means `minmax(auto, 1fr)`, so a column can refuse to shrink below its widest unbreakable content (a long word, a wide table) and push the page sideways at 320px. `minmax(0, 1fr)` lets it shrink. I did not test a broken version of this page, so if you demo removing it, try it first.
- **Grid for the page, Flexbox inside the regions.** Grid = two-dimensional page structure. Flexbox = a row of things (buttons, links, cards). Ask the class which one they would use for each.
- **`.card { flex: 1 1 220px }`**: cards reflow 3 to 2 to 1 with no media query. At 1000px two cards sit on row one and the third wraps (that's flex-wrap doing its job).
- **Landmarks survive Grid.** Grid rearranges visually; the DOM order (header, nav, main, aside, footer) is what screen readers get. Don't use `grid-template-areas` to move things in a way that makes the tab order jump around.

## What I tested (all pass)
- Nu HTML validator: zero errors. CSS parser: zero errors. axe: zero violations.
- Widths 320, 600, 899: single column, no horizontal scroll. 900 and 1200: two columns, sidebar beside main. (Steps 3 and 4 on their own only work under 900px, since the desktop query doesn't exist until step 5.)
- First Tab stop is the skip link.
- NOT run (I can't reach them from here): the W3C CSS validator at jigsaw.w3.org and Lighthouse. Do those live in step 10.

## Grading tips for student submissions
- **Grid Template Areas (10):** check that all five names exist, and that each element has a matching `grid-area`. Common bugs: name typos, rows with different column counts, `grid-area` missing on one region (it then auto-places).
- **Responsive (8):** mobile stacks in a single column and desktop is two columns at 900px, each defined with `grid-template-areas` inside a media query (this demo: `max-width: 899px` and `min-width: 900px`). Watch for desktop rules that get fixed with `grid-column` or `order` overrides instead of a redefined area map. A mobile-first student (stacked areas at base, desktop in `min-width: 900px`) is a judgment call under your wording, since the mobile areas are not in a media query.
- **Flexbox (7):** need `display: flex` on a container inside two regions, with real flex children (an `<li>` row, a card row).
- **Semantic HTML (5):** `header`, `nav`, `main`, `aside`, `footer`. One `main` only. No `div` standing in for a region.

## Images
The three images are original SVG illustrations so the demo runs offline. The lab asks for royalty-free photos (Unsplash, Pexels, Pixabay) and, for web images, the website in an HTML comment. Each `<img>` already has a comment above it in `index.html` showing the pattern: replace the example with the real page URL and photographer. Swap the files into `images/` and keep `width`/`height` attributes and alt text.
