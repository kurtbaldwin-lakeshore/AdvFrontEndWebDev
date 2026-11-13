# 5.3 Live Demo: A Complete Responsive Page with Flexbox (`about.html`, `css/5-3.css`)

These follow the 8 steps on the DT 5.3 slide, with two extra steps for the problems you meet when you test. The HTML does not change. Open `starter/about.html` and `css/5-3.css`. CSS after each step: `steps/5-3/stepN.css` (steps 0 to 6 and 8; step 7 is Lighthouse).

## What is broken in the starter
The Home, Products and About Us nav links are fixed-width inline blocks, and the page is a floated 960px layout (680px main, 250px sidebar). It scrolls sideways at 320, 600 and 700px and is fine at 1024px and up. The headline is a fixed 56px.

| Step | Change | What you will see |
|---|---|---|
| 1 | Nav: BASE `.site-nav ul { display: flex; flex-direction: column; list-style: none; margin: 0; padding: 0; gap: 0.25rem; }`, links `min-height: 44px`. Then `@media (min-width: 600px) { .site-nav ul { flex-direction: row; justify-content: flex-end; } }` | Stacked buttons on a phone, a right-aligned row at 600px and up |

| 2 | Delete the floats and widths. Add `.layout { display: flex; gap: 2rem; }` | Side by side, but sized by content (at 1024px the sidebar is 190px and main 746px). At 320px the sidebar shrinks to 138px, main is 634px wide and the page scrolls sideways |

| 3 | `.sidebar { flex: 0 0 250px; }` and `.main { flex: 1; }` | Sidebar fixed at 250px, main fills the rest. Nice at 1024px. Still broken on a phone |

| 4 | Make it mobile first. BASE: `.layout { display: flex; flex-direction: column; gap: 2rem; }`. Then `@media (min-width: 600px) { .layout { flex-direction: row; } .sidebar { flex: 0 0 250px; } .main { flex: 1; } }` (move the flex sizing INSIDE the query) | Stacked below 600px, side by side at 600px and up |

| 5 | Test at 320px (no code needed to see it): it still scrolls sideways. Find why (see the console trick below), then add `img { max-width: 100%; height: auto; display: block; }` and `.site-header h1 { font-size: clamp(1.5rem, 4vw, 3rem); }` | The map image fits. The headline scales from 24px to 48px. It STILL scrolls at 320px, and at 600 to 640px |

| 6 | Add `code { overflow-wrap: anywhere; }` and, inside the 600px query, `.main { flex: 1; min-width: 0; }` | The long file name now wraps, and main can shrink. No overflow at any width (checked every 20px from 320 to 1080) |

| 7 | Run Lighthouse (the deck's target is 90+) | Not run by me, so do it live |

| 8 | Bonus: center the dashed box. `.center-demo { display: flex; justify-content: center; align-items: center; }` | Text centered both ways |

## Console trick for step 5 and 6 (paste into the DevTools Console)
```js
[...document.querySelectorAll('body *')].filter(e => e.getBoundingClientRect().right > document.documentElement.clientWidth).map(e => e.tagName.toLowerCase() + (e.className ? '.' + e.className : ''))
```
At 320px after step 4 it lists `img` and `code`. After the image fix it lists only `code`. After step 6 it is empty.

## Talking points
- Keep sizing in the query. In a COLUMN, `flex-basis` is a height, so a base `.sidebar { flex: 0 0 250px }` sets the stacked sidebar's height. I measured it: with `flex: 0 0 400px` outside the query the stacked sidebar is 400px tall instead of its natural 268px. With 250px you will not see it here, because the content is already taller, which is exactly why students miss it.
- Step 6 is the classic Flexbox gotcha. A flex item will not shrink below its content (`min-width: auto`). A long unbroken string (a file name or URL) holds `main` wide and pushes the sidebar off the screen. `min-width: 0` lets the item shrink, and `overflow-wrap: anywhere` lets the text wrap. The file name uses underscores on purpose, because the browser will break a hyphenated name on its own.
- Step 5: `clamp(1.5rem, 4vw, 3rem)` is the minimum, preferred and maximum. The deck says the minimum never goes below 1.5rem, which is what keeps Reflow working at 320px.
- Accessibility (deck): stacked nav is easiest to tap and use (44px targets). The sidebar comes after main in the HTML, so keyboard and screen reader order is the order you want, and no `order` property is needed.
- The deck's agenda also mentions the "holy grail" layout. That is not built here. Use this page's layout as the starting point and add a header and footer if you want to show it.

## Not run
Lighthouse and the W3C CSS validator.
