# 5.1 Live Demo: Mobile-First and Media Queries (`index.html`, `css/5-1.css`)

The deck's demo is the Chrome DevTools device toolbar. This page makes it real: it is broken in five ways, and you fix it with the mobile-first pattern from the slides. Open `starter/index.html` and `css/5-1.css`.

## Part A: see the problems (the slide's DevTools steps)
1. Press F12, then the phone/tablet icon (or Ctrl+Shift+M).
2. Pick "iPhone SE" (375px). The page is tiny and zoomed out. The starter has NO viewport meta tag, so the phone pretends to be 980px wide (measured: layout width 980 without the tag, 375 with it).
3. Switch to Responsive and drag to **320px**. Sideways scroll appears (every starter page overflows at 320).
4. Look at 600px and 1024px. It still scrolls sideways at both (the page is a fixed 960px). Only at 1440px does it look fine.

## Part B: fix it (CSS after each step is in `steps/5-1/stepN.css`)

| Step | Change | What you will see |
|---|---|---|
| 1 | HTML only. In the `<head>`, add `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | On the phone emulation the page now lays out at 375px instead of 980px. It still scrolls sideways, because the CSS is fixed width |
| 2 | `.container`: change `width: 960px` to `max-width: 960px`. Add `img { max-width: 100%; height: auto; display: block; }` | The trail-map image stops overflowing. The page STILL scrolls at 320 and 700px: the nav, the cards and the text block are still 960px |
| 3 | The mobile BASE, using only what is already covered. Nav: remove the fixed widths and the `li` inline-block, so the links stack as normal block boxes. `.hero` goes from `height: 480px` to `min-height: 50vh`. Cards: delete the floats and the fixed widths; plain block boxes already stack, so add only `margin-bottom: 1rem`. Delete the fixed width on `.article-body` | One column everywhere, no sideways scroll at 320 or 700 |
| 4 | Add `@media (min-width: 600px) { .nav li { display: inline-block; vertical-align: top; } .card-grid { column-count: 2; column-gap: 1rem; } .card { break-inside: avoid; } }` | At 600px and up the nav is a row and the cards are two across |
| 5 | Add `@media (min-width: 1024px) { .card-grid { column-count: 3; } .hero { min-height: 80vh; } }` | Three cards across and a taller hero at 1024px and up |
| 6 | Inside the 600px query add `.article-body { column-count: 2; column-gap: 2rem; }` | The story text flows into two newspaper columns from 600px |
| 7 | Test: 320, 600, 1024, 1440 in the device toolbar. Turn on touch simulation | No horizontal scroll at any size (this is the WCAG 1.4.10 Reflow check from the deck) |

## Talking points
- Mobile first means the base rules are for the smallest screen and each `min-width` query only adds. Show that the step 3 base has no media query and still works at 320px. Then contrast with desktop-first (the starter), where everything is overridden downward.
- Order matters: base first, then 600px, then 1024px, smallest to largest. If you put the 600px query above the base, the base wins and nothing changes.
- No flex or grid on this page on purpose: they are not taught until 5.2 and the grid unit. Block boxes stack by themselves (that is the mobile base), `inline-block` puts the nav in a row, and `column-count` makes the card columns. Say that 5.2 rebuilds a card grid properly with flexbox, so students see why it is better. Column cards read top to bottom inside each column, which is a limit of this shortcut.
- Why step 2 does not finish the job: one fix removes one cause. Reflow bugs usually have several.
- The tablet nav row fits at 600px (five short links). If a student has longer links, they need a bigger breakpoint, so the breakpoint comes from the content, not from a device.
- Measured results for the finished page: nav column at 320, row at 600+; cards 1 / 2 / 3 columns at 320 / 600 / 1024; hero 450px (50vh) then 720px (80vh) in a 900px-tall window; article text 2 columns at 600+.

## Not run
Lighthouse and the W3C CSS validator (I cannot reach them from here).
