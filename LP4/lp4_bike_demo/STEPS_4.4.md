# 4.4 Live Demo: @font-face & Web Typography (history.html, shared styles.css)

NOTE: the DT 4.4 deck has no demo slide, so these steps come from its content slides. The font files are already in the `fonts/` folder (Oswald 400/700, Lora 400/400 italic/700, each as .woff2 and .woff; SIL Open Font License). Open the 4.4 section of styles.css (empty). Start by showing history.html in the default Times font.

| Step | CSS | What to show |
|---|---|---|
| 1 | Two `@font-face` rules for Oswald (400 and 700): `font-family: 'Oswald'; src: url('fonts/oswald-latin-700-normal.woff2') format('woff2'), url('fonts/oswald-latin-700-normal.woff') format('woff'); font-weight: 700; font-style: normal; font-display: swap;` | Nothing changes yet: defining a face does not USE it. Good moment to say that |
| 2 | Three `@font-face` rules for Lora: regular, italic (`font-style: italic`) and bold (700) | Still nothing on screen. One rule per weight/style, same family name |
| 3 | `body { font-family: 'Lora', Georgia, serif; line-height: 1.6; }` `h1, h2, h3 { font-family: 'Oswald', 'Arial Narrow', sans-serif; line-height: 1.2; }` | Page switches to Lora body and Oswald headings. Open DevTools > Network > Font: only .woff2 files download |
| 4 | `h1 { font-size: 2.441rem; }` `h2 { font-size: 1.953rem; }` `h3 { font-size: 1.25rem; }` | Type scale, ratio 1.25 (1rem body) |
| 5 | `main p { max-width: 55ch; }` | Paragraphs stop running edge to edge: about 70 characters per line |
| 6 | DevTools > Network > throttle to "Slow 3G" (or Offline), hard refresh | Text is readable immediately in the fallback font, then swaps. Change `font-display: swap` to `block` on one face to show invisible text |
| 7 | Validate CSS | Zero errors (run live at jigsaw.w3.org/css-validator; I could not run it) |

## Talking points
- Format order: woff2 first, woff as fallback. The browser uses the first format it supports; in current browsers only the .woff2 files download (tested).
- The path is `fonts/...` because styles.css sits in the site root. The deck's `../fonts/` is for a css/ subfolder.
- Oswald 400 is defined but never downloads: every heading is bold by default, and the browser only fetches faces the page actually uses. Add `h3 { font-weight: 400; }` to watch it load.
- Italic and bold are separate files. Delete the Lora italic `@font-face` and the browser fakes an italic for `<em>`/`<cite>` (look at "treat every rider like a neighbor"). Delete the 700 rule and `<strong>` is faux bold.
- `ch` is the width of the "0", so `65ch` runs about 85 real characters in Lora. `55ch` lands near the 60 to 80 target (measured: 71 to 72 characters per line).
- Variable fonts (deck slide): one file, any weight. There is no variable font file in this site, so cover it with the slide only.
- The same font-family rules apply to all four pages (shared stylesheet).
