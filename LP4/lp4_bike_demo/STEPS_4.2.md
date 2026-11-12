# 4.2 Live Demo: Pseudo-classes & Pseudo-elements (products.html, shared styles.css)

NOTE: the DT 4.2 deck has no demo slide, so these steps are built from its content slides (structural, :target / ::placeholder, ::before / ::after, form pseudo-classes, :focus-visible). Open the 4.2 section of styles.css (empty), add each rule, save, refresh.

| Step | CSS | What to show on products.html | Matches |
|---|---|---|---|
| 1 | `article:first-child { background-color: yellow; }` | NOTHING happens. The h2 is child #1, so no article is a first child. Fix: `:first-of-type` | 0 |
| 2 | `article li:first-child { font-weight: bold; }` `article li:last-child { color: #0b6b2d; }` | First spec bold, Price line green in each card | 4 + 4 |
| 3 | `tbody tr:nth-child(even) { background-color: #f2f2f2; }` | Zebra stripes in the price table | 4 |
| 4 | `article:target { background-color: #fff8dc; outline: 3px solid coral; scroll-margin-top: 2rem; }` | Click Products > Gravel Bikes in the nav, or a View link in the table | 1 at a time |
| 5 | `article:target h3::before { content: '\2192  '; }` | Arrow before the targeted card's heading only | 1 at a time |
| 6 | `::placeholder { color: #777; font-style: italic; }` | Reserve form placeholders turn grey italic | 3 |
| 7 | `input:required { border-top: 2px solid coral; }` `input:invalid:not(:placeholder-shown) { outline: 2px solid #c62828; }` `input:valid:not(:placeholder-shown) { outline: 2px solid #2e7d32; }` | Nothing is red at load. Type a name: green. Type "bad" in Email: red. Fix it to a real address: green | 2 required |
| 8 | `label:has(+ input:required)::after { content: ' *'; color: #c62828; }` | Red asterisk on Full name and Email labels | 2 |
| 9 | `a:focus-visible, button:focus-visible, input:focus-visible, select:focus-visible, textarea:focus-visible { outline: 3px solid #1d4ed8; outline-offset: 2px; }` | Press Tab: blue ring. Mouse-click a button: no ring | |

## Talking points
- Step 7 is the deck's "problem / solution": plain `input:invalid` is red before the user touches the field. Adding `:not(:placeholder-shown)` waits until they type. (It only works on fields that HAVE a placeholder.) Radios, checkboxes and the date field have none, so they never get the outline.
- Step 7 uses `border-top` and an outline, not a background, so the 4.1 email tint survives (same-specificity rules later in the file would override it).
- `::before`/`::after` need `content` and cannot go on `<input>`, so step 8 hangs the asterisk on the label.
- Text fields and textareas always show `:focus-visible` (even on click) because you type in them; buttons and links only on keyboard.
- Pseudo-CLASS = state (one colon). Pseudo-ELEMENT = part (two colons). Steps 5, 6, 8 mix both.
- Accessibility (deck): CSS-generated content is read by some screen readers and ignored by others. Decorative = `content: ''`; informative text needs testing.
- Validate at the end (W3C CSS validator: run live).
