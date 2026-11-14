# 6.1 Live Demo: CSS Grid Fundamentals (`index.html`, `css/6-1.css`)

This follows the LIVE DEMO slide ("Building a Grid Layout — Live"), with the `repeat()`, `minmax()`, `auto-fit`/`auto-fill` and span material from the earlier slides added as steps. Open `starter/index.html` and `css/6-1.css`. The HTML already has the header, nav, main, aside, a service band and the footer (slide step 3), so you do not need to type any markup. Say so on camera.

The starter is one long column. Nothing is broken, it is just not a layout yet.

## Part A: the starter
1. Open `starter/index.html` in Chrome. Everything stacks: header, nav, cards, hours box, service boxes, footer.
2. Open DevTools, Elements. Find `.page-grid`. There is no grid badge next to it, because it is not a grid yet.

## Part B: build it (CSS after each step is in `steps/6-1/stepN.css`)

| Step | Add to `css/6-1.css` | What you will see (measured at a 1200px window) |
|---|---|---|
| 1 | In `.page-grid`: `display: grid; grid-template-columns: 200px 1fr 200px;` | The page falls apart on purpose. The grid places items into cells in source order, so the header lands in the 200px cell, the nav in the middle cell, and `main` in the other 200px cell. Say: "I never told the header to span, so it took one cell." |
| 2 | In `.page-grid`: `gap: 2rem;` | Gutters appear. Columns are 200px, 604px, 200px with 32px between them |
| 3 | Add `.site-header { grid-column: 1 / -1; }`, `.site-footer { grid-column: 1 / -1; }` and `.services { grid-column: 1 / -1; }` | Header, service band and footer now run the full 1068px width. Nav, main and aside sit side by side in one row. The browser placed them automatically, in source order. Explain `1 / -1`: first line to last line, so it works for any number of columns |

| 4 | Add `.card-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1rem; }` and `.featured { grid-row: span 2; }` | A grid inside a grid cell. The gravel bike card is 294px wide and about 396px tall, spanning two rows. The other two cards stack beside it. Point out `repeat(2, 1fr)` is the same as `1fr 1fr` |
| 5 | Add `.service-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 1rem; }` | Three boxes in a row. At a 1440px window the grid has six 165px columns, so three boxes sit in the first three and three tracks are empty. Drag the window narrower and watch columns come and go with no media query. At 900px there are five 161px tracks |
| 6 | Change `auto-fill` to `auto-fit` | The empty tracks collapse to 0px and the three boxes stretch: 345px each at 1440px, 279px each at 900px. This is the deck's demo cue |
| 7 | Add `@media (max-width: 899px) { .page-grid { grid-template-columns: 1fr; } .card-grid { grid-template-columns: 1fr; } .featured { grid-row: auto; } }` | Below 900px everything is one 288px column at 320px. No sideways scroll at 320, 899, 900 or 1440 |

Turn on the Grid overlay (the `grid` badge next to `.page-grid`, and again next to `.card-grid` and `.service-grid`) after steps 2, 3 and 6. Have students click the badge themselves at least once, as the deck asks.

## Accessibility demo: visual order versus Tab order (deck slide, DemoCue)
After step 7, add at the bottom:
```css
@media (min-width: 900px) {
  nav   { grid-column: 3; grid-row: 2; }
  aside { grid-column: 1; grid-row: 2; }
}
```
The nav jumps to the right and the hours box to the left. Now press Tab. Measured order: skip link, then the five nav links (on the right), then the card links in the middle, then the group ride link in the hours box (on the left). Keyboard users go right, middle, left while sighted users read left to right. That is WCAG 1.3.2. Delete the two rules to restore the page.

## Talking points
- `fr` means "one share of the space left after fixed tracks". Show `200px 1fr 200px`: the middle column is whatever is left (604px at 1200, 404px at 900).
- `repeat(3, 1fr)` is only a shorthand for `1fr 1fr 1fr`. `minmax()` inside `repeat()` is where the responsiveness comes from.
- This slide's demo uses a `max-width` query to collapse. The earlier LP5 lessons were mobile first. Both work. Say which one you used and why. This page uses `899px` so the 6.2 page (which uses `min-width: 900px`) switches at the same width.
- Why not the deck's 600px? Measured: with `max-width: 600px`, at 601px the three columns need about 724px, so the page scrolls sideways. At 800px it fits. The breakpoint comes from where the content breaks, not from a device.
- Common mistake from the deck: pixel widths from habit instead of `fr`.
- `grid-column: 1 / 4` works only for three columns. `1 / -1` always spans all of them.
- Extra to mention: `.featured { grid-area: 1 / 1 / 3 / 3 }` is the long shorthand (row-start / column-start / row-end / column-end). It is on the slide but not needed here.

## Not run
Lighthouse and the W3C CSS validator.
