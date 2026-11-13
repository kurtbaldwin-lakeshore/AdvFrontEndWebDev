# LP5 Responsive Lab (Driftless Cycle Co.)

One multi-page site, one page per discussion topic, laid out like the LP4 bike shop: `index.html` is 5.1, `products.html` is 5.2 and `about.html` is 5.3, all linked by the shop's own nav. Every page starts BROKEN on purpose and you fix it live.

| Page | Topic | What is broken | What you do |
|---|---|---|---|
| `index.html` (Home) | DT 5.1 Mobile-first and media queries | No viewport tag, fixed 960px widths, floats, fixed nav and hero | Add the viewport tag, go fluid, write the mobile base, then min-width queries at 600px and 1024px, then test at 320px |
| `products.html` (Products) | DT 5.2 Flexbox fundamentals | Floated, fixed-width cards | `flex-wrap` card grid with `flex: 1 0 280px`, hover and focus, plus `align-self` and `order` |
| `about.html` (About Us) | DT 5.3 Flex items and responsive patterns | Inline-block nav, floated main and sidebar | Column-to-row nav, flex main and sidebar, `clamp()`, centering |

Why three pages and not separate mobile and Flexbox pages: 5.1 is only about media queries and mobile-first thinking, 5.2 is Flexbox on its own (it needs no media query at all), and 5.3 combines the two. That is the order the decks teach them, and each page ends with something that really works.

## Folders
- `starter/` is the site to open in VS Code and fix. Each page has its own stylesheet, because each page starts broken in a different way: `css/5-1.css` for index.html, `css/5-2.css` for products.html and `css/5-3.css` for about.html. `css/base.css` is shared and already finished. The nav on each page is part of that page's own lesson: 5.1 and 5.3 break and fix it, and the 5.2 nav already works.
- `finished/` is the same site, fully fixed.
- `steps/5-1`, `steps/5-2`, `steps/5-3` hold the CSS after each step (`step3.css` is the whole `5-x.css` file as it should look after step 3). Use them to jump ahead or recover.
- `STEPS_5.1.md`, `STEPS_5.2.md`, `STEPS_5.3.md` are the live-demo guides. They follow the demo steps on each deck's slides.

## Standing rules I followed
- Skip link in the body and its CSS on every page.
- Mobile first: base CSS for the smallest screen, `min-width` queries only.
- No reduced-motion CSS in this lab. The only motion is the 5.2 card hover transition. Add the 3.3 reset there if you want it.

## What I tested (all in a real browser)
- Nu HTML checker: zero errors on every page, starter and finished. CSS parsed with zero errors in all 29 CSS files. axe: zero violations on every finished page at 320px and 1024px. The first Tab stop is the skip link.
- Starter pages overflow at 320px (all three). Finished pages do not overflow at 320, 600, 1024 or 1440px.
- NOT run (I cannot reach them from here): the W3C CSS validator and Lighthouse. Run them live. The 5.3 deck ends with "Lighthouse 90+".
