# 4.1 Live Demo: Styling Without Classes (index.html, shared styles.css)

Open index.html. Show the HTML: there are NO class attributes anywhere. Open styles.css (the 4.1 section is empty) and add each rule, saving and refreshing after each one.

| Step | CSS | Where to look on index.html | Matches |
|---|---|---|---|
| 2 | `input[required] { border-left: 3px solid coral; }` | Contact & Newsletter form: Name and Email get a coral left edge; Mobile (optional) does not | 2 |
| 3 | `input[type='email'] { background-color: #eef6ff; color: #0b3d91; }` | Only the Email field turns light blue (still keeps coral edge) | 1 |
| 4 | `a[href^='http']:not([href*='yourdomain.com'])::after { content: ' ↗'; }` | "Around the Web" links and the Ride with GPS link get an arrow | 5 |
| 5 | `a[href$='.pdf']::after { content: ' (PDF)'; }` | Care checklist, Trail map and the two Downloads PDFs get "(PDF)" | 4 |
| 6 | Validate CSS at jigsaw.w3.org/css-validator and HTML at validator.w3.org | Confirm zero errors | |

Bonus (already in the file): `a[href='#main-content']` + `:focus` hides the skip link until you press Tab.

## Talking points
- Step 3: use background/color only. A `border` or `border-color` shorthand in the email rule would wipe out the coral left border from step 2, because it comes later with equal specificity.
- Step 4: the site has no absolute link to its own domain, so `:not([href*='yourdomain.com'])` has nothing to exclude. To show it working, add `<a href="https://yourdomain.com/about">Our story</a>` anywhere: it gets NO arrow. (Tested.)
- Mailto, tel, in-page and relative links get no arrow because they do not start with `http`.
- The PDF link text no longer says "(PDF)" in the HTML, so the CSS supplies it (otherwise it shows twice).
- Only one `::after` per element: an external link ending in `.pdf` would match both rules, and specificity (0,2,0 beats 0,1,0) means it shows the arrow, not "(PDF)".
- Other pages share this stylesheet: products.html and about.html also have required inputs, so they pick up the coral edge too. That is the point of attribute selectors.
