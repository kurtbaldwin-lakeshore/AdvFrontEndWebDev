# 4.3 Live Demo: Building LP4 Design Details (about.html, shared styles.css)

Steps are the six on the DT 4.3 slide. The slide uses `.section-title` and `.gradient-heading` classes, but this HTML has no classes, so the same patterns are applied with element/ID selectors. Open the 4.3 section of styles.css (empty).

| Step | CSS | What to show on about.html |
|---|---|---|
| 1 | `main h2 { position: relative; padding-top: 1rem; }` `main h2::before { content: ''; position: absolute; top: 0; left: 0; width: 3rem; height: 4px; background: linear-gradient(90deg, #0d7a8a, #c04020); border-radius: 2px; }` | Teal-to-rust accent bar above all 7 section titles (the other pages share the stylesheet, so their h2s get it too) |
| 2 | `blockquote::before { content: '\201C'; display: block; font-size: 5rem; line-height: 0.6; height: 2.5rem; color: #0d7a8a; }` | Big opening quote above the mission quote |
| 3 | `header h1 { background: linear-gradient(135deg, #0d7a8a, #c04020); -webkit-background-clip: text; background-clip: text; color: transparent; }` | Gradient page heading. Contrast on white: teal 5.04:1, rust 5.26:1, so both ends pass (3:1 needed for large text) |
| 4 | `#banner { background-image: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.3)), url('images/workshop-banner.svg'); background-size: cover; background-position: center; color: #fff; padding: 3rem 1.5rem; }` | "Built in the Driftless" band: photo with dark overlay, white text. Swap the two layers to show the first one paints on top |
| 5 | `#team article { position: relative; padding-top: 1rem; }` `#team article::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 6px; background: linear-gradient(90deg, #0d7a8a, #c04020); }` | Gradient bar across the top of each team card |
| 6 | Validate at jigsaw.w3.org/css-validator | Confirm zero errors (run live; I could not run it) |

## Talking points
- Step 4 is the "hero". I used the full-width `#banner` band rather than the `<header>`, because step 3 puts gradient text on the header's h1. Dark photo behind gradient text would fail contrast.
- Step 3: the `-webkit-` prefix is still needed for `background-clip: text` (the slide says so). Use only for large decorative headings.
- Step 1 and 5 both use `position: relative` on the parent so the absolutely positioned `::before` stays inside it.
- Step 2: `content: '\201C'` may be read by some screen readers (slide: accessibility spotlight). `content: ''` is silent.
- Extra material from the slides if you have time: `background-size: contain` and `border-image` (the site has `images/logo-mark.svg` and `images/border-frame.svg` for these).
