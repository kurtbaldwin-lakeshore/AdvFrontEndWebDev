# Checkpoint 2 Sample Build (Wisconsin State Fair)

A finished example that follows the 12-step Checkpoint 2 Build Guide. Each `commitNN/` folder is the project exactly as it should look right AFTER that commit, so you can start anywhere or show a "before and after" by comparing two folders. `finished/` is the same as `commit12/`. `commit_messages.txt` lists the 12 commit messages.

## How to use it live
1. Create a new public GitHub repo, clone it, open it in VS Code.
2. For each step, type the new code from the guide (or copy it from the next folder's `style.css`), save, refresh the browser, then commit with the message from `commit_messages.txt`.
3. Compare your folder with `commitNN/` if the page doesn't look right.

| Commit | Adds | Where to look in the browser |
|---|---|---|
| 01 | HTML skeleton, empty stylesheet, README | Blank page, tab title shows |
| 02 | Semantic HTML (skip link, header, nav, main, section/article, aside, footer) and content | Unstyled page that still reads in order. Tab once: skip link |
| 03 | Custom properties, reset, skip link CSS, focus ring | Tab: skip link appears, then every link gets a ring |
| 04 | Grid with named areas. Mobile areas at base, desktop areas at 900px | Stacked below 900px, sidebar beside main at 900px+ |
| 05 | Flexbox: nav, quick links, footer links, card row | Links in rows, cards reflow without a media query |
| 06 | border-radius, box-shadow, gradients, region colors | Colored regions, rounded corners, shadows |
| 07 | 600px breakpoint | Header becomes a row at 600px, larger text |
| 08 | fadeInUp heading and pulsing first button | Reload: heading slides up, button keeps pulsing |
| 09 | prefers-reduced-motion reset | Turn on reduce (DevTools Rendering panel, then the real OS setting): everything stops |
| 10 | README validation section (no code change if the pages are clean) | Run both W3C validators, record the dates |
| 11 | README accessibility section | Run Lighthouse (Mobile and Desktop), record real scores and a screenshot |
| 12 | README live link | Publish on GitHub Pages, replace the placeholder URL |

## What I tested
- W3C Nu HTML checker: zero errors. axe accessibility scan: zero violations.
- Widths 320, 599, 600, 899, 900, 1200: no horizontal scroll; the sidebar sits beside main only at 900px and up; the header becomes a row at 600px.
- Reduced motion: with "no preference" the button pulses forever (2 running animations); with "reduce" none are running and the heading is fully visible.
- First Tab stop is the skip link.
- NOT run (not reachable from my environment): the W3C CSS validator and Lighthouse. Commits 10 and 11 are for you to run live. The README placeholders ("__", "add the date") are blanks to fill in with real results.

## Images
The three images are original SVG illustrations (so it works offline). Each has an HTML comment showing where a web photo's source URL goes. Swap in real Unsplash, Pexels or Pixabay photos and put the URL in that comment.
