# 6.2 Live Demo: Grid Areas and Named Regions (`products.html`, `css/6-2.css`)

This follows the LIVE DEMO slide ("Building the Complete Page Layout"). Open `starter/products.html` and `css/6-2.css`. The nav links and bike cards already use Flexbox from LP5 (the deck's "Grid for the page, Flexbox inside each region"). The page is one long column and the HTML does not change.

The HTML source order is header, nav, main, sidebar, footer. Say this on camera. It is the reading order and it never changes in this lab.

## Part B: build it (CSS after each step is in `steps/6-2/stepN.css`; the slide's steps 4 to 6 need no code)

| Step | Change in `css/6-2.css` | What you will see (measured) |
|---|---|---|
| 1 | Make `.page` a grid with the mobile map: `display: grid; gap: 1.5rem; grid-template-areas: 'header' 'nav' 'main' 'sidebar' 'footer';` | The page looks almost the same, with the 1.5rem gap added between regions. The map names areas, but no element has been assigned to one yet. Say that out loud |
| 2 | Add `header { grid-area: header; }`, `nav { grid-area: nav; }`, `main { grid-area: main; }`, `.sidebar { grid-area: sidebar; }` and `footer { grid-area: footer; }` | Still one column, now properly mapped. This is the moment to turn on the Grid overlay and show the area names |
| 3 | Add `@media (min-width: 900px) { .page { grid-template-columns: 220px 1fr; grid-template-areas: 'header header' 'nav nav' 'sidebar main' 'footer footer'; } }` | At 1200px: header and nav span the full 1068px, sidebar is 220px on the left, main is 824px on the right, footer spans. Only the map changed. The five `grid-area` lines were not touched |
| 4 | DevTools: turn the Grid overlay on, tick "Display area names" | The names header, nav, sidebar, main and footer appear on the page |
| 5 | Resize to 320px | One column, 288px wide, nothing scrolls sideways, reading order header, nav, main, sidebar, footer |
| 6 | Resize to 900px | Sidebar appears beside main |
| 7 | Add `min-height: 100vh` to `.page`, add `grid-template-rows: auto auto 1fr auto auto` to the mobile rule and `grid-template-rows: auto auto 1fr auto` to the 900px rule | In a 1600px-tall window the footer now ends at the bottom of the window (1600px). Before step 7 the footer ended at 727px with blank space under it. The `1fr` row for main stretches |

Note on the map: the deck's desktop example leaves out the `nav` row. This page has a nav, so the map has `'nav nav'`. See the next section for what happens if you leave it out.

## Broken examples (the deck says to show one; each result below was measured at 1200px)
1. **A missing row.** Delete the `'nav nav'` line from the 900px map. The nav is no longer in the map but still has `grid-area: nav`. It jumps below the footer on the right (about 513px wide, near the bottom of the page) and the header shrinks to about half width. Put the line back.
2. **A ragged map.** Change `'header  header'` to `'header'` in the 900px map (two columns in most rows, one in this row). The whole `grid-template-areas` declaration is thrown away, so the page shows as a single 220px-wide stack. Nothing on the page says why.
3. **Missing quotes.** Remove the quotes from `footer  footer`. Same result as the ragged map: the declaration is dropped and the page falls back to one narrow column.
4. **A `.` empty cell.** Change `'footer  footer'` to `'.       footer'`. The footer now starts under the main column (x = 310px) and the left column stays open beneath the sidebar.

## Optional: sidebar on the right
Change `grid-template-columns: 220px 1fr` to `1fr 220px` and `'sidebar main'` to `'main sidebar'`. Now main (left) comes first both on screen and in the source, so Tab order matches what you see. With the sidebar on the left, main is first in the source but second on screen. Use this to tie back to the 6.1 accessibility demo.

## Talking points
- "The grid-area assignments are written once. Only the map changes per breakpoint." That is the biggest idea of the session.
- Main comes before the sidebar in the source, so on a phone and for a screen reader the main content comes first.
- Why `.sidebar` and not `aside`? The slide uses `.sidebar`. The element is an `<aside>` with an `aria-label`, so it is a landmark.

## Not run
Lighthouse and the W3C CSS validator.
