# Driftless Cycle Co. - LP4 Live-Code Demo: Instructor Notes

A four-page bicycle shop site for demonstrating Learning Plan 4 live in class. The HTML has **no CSS, no classes, and no inline styles**, which matches the LP4 lab constraint. Everything is selected by structure and attributes. The only ids are the ones needed for label/for, `:target` jumps, and `aria-controls`.

**One shared `styles.css`** is linked from all four pages, with a heading for each lesson. Rules written in 4.1 will also affect the later pages, which is realistic. If you want each lesson isolated, comment out the earlier sections or make a copy of the folder per lesson.

| Lesson | Page | Main idea |
|---|---|---|
| 4.1 | `index.html` | Combinators and attribute selectors |
| 4.2 | `products.html` | Pseudo-classes and pseudo-elements |
| 4.3 | `about.html` | Advanced backgrounds (also has quote/`::before` spots if your 4.3 still covers pseudo-elements) |
| 4.4 | `history.html` | `@font-face` and web typography |

Every count below was measured in a real browser against the finished HTML. The HTML also passes the W3C Nu validator with zero errors and zero warnings.

## DT 4.1 - Combinators & Attribute Selectors  (`index.html`)

| Selector | What it demonstrates | Matches |
|---|---|---|
| **COMBINATORS** | | |
| `nav li` | DESCENDANT: every li anywhere inside nav (top menu AND submenu) | 9 |
| `nav > ul > li` | CHILD: only the five top-level menu items | 5 |
| `nav ul ul` | DESCENDANT: the nested submenu list | 1 |
| `nav > ul > li > a` | CHILD chain: top-level links only (no submenu links) | 5 |
| `header h1 + p` | ADJACENT: the tagline right after the h1 | 1 |
| `#welcome h2 + p` | ADJACENT: only the first paragraph under the h2 | 1 |
| `#welcome h2 ~ p` | GENERAL SIBLING: all three paragraphs after the h2 | 3 |
| `#guide h2 + p` | ADJACENT: only the h2s followed straight by a p (3 of the 5 h2s) | 3 |
| `#guide p + h2` | ADJACENT: only the h2s that come right AFTER a p (2 of the 5) | 2 |
| `#guide h2 ~ p` | GENERAL SIBLING: every paragraph after the first h2, adjacent or not | 5 |
| `#guide h2 + ol` | ADJACENT: the h2 followed by an ordered list (Chain Care) | 1 |
| `#guide h2 + ul` | ADJACENT: the h2 followed by a list (Winter Storage) | 1 |
| `#resources h3 + ul` | ADJACENT: the list straight after each h3 | 2 |
| `#faq h3 + div` | ADJACENT: each answer panel after its question | 3 |
| `#faq h3 > button` | CHILD: the button directly inside each h3 | 3 |
| **ATTRIBUTE SELECTORS - LINKS** | | |
| `a[href^="https"]` | STARTS WITH: secure external links | 4 |
| `a[href^="http:"]` | STARTS WITH: the one insecure link (http, not https) | 1 |
| `a[href^="mailto:"]` | STARTS WITH: email links | 2 |
| `a[href^="tel:"]` | STARTS WITH: phone links | 2 |
| `a[href^="#"]` | STARTS WITH: in-page links (skip link, 'Ask us', back to top) | 3 |
| `a[href$=".pdf"]` | ENDS WITH: PDF files | 4 |
| `a[href$=".gpx"]` | ENDS WITH: GPX route files | 2 |
| `a[href$=".csv"]` | ENDS WITH: CSV file | 1 |
| `a[href$=".zip"]` | ENDS WITH: ZIP file | 1 |
| `a[href$=".html"]` | ENDS WITH: links to other pages on the site | 7 |
| `a[href*="bikefed"]` | CONTAINS: one specific external site | 1 |
| `a[href*="driftless"]` | CONTAINS: the shop's own email address | 2 |
| `a[target="_blank"]` | EXACT: links that open in a new tab | 4 |
| `a[rel~="noopener"]` | WORD MATCH: rel list contains the word noopener | 4 |
| `a[download]` | PRESENCE: links with the download attribute | 4 |
| `a[aria-current="page"]` | ARIA STATE: the current page in the menu | 1 |
| **ATTRIBUTE SELECTORS - FORMS, ARIA, OTHER** | | |
| `input[type="text"]` | EXACT: text input | 1 |
| `input[type="email"]` | EXACT: email input | 1 |
| `input[type="tel"]` | EXACT: telephone input | 1 |
| `input[required]` | PRESENCE: required fields | 2 |
| `label + input` | ADJACENT: input right after its label | 3 |
| `button[aria-expanded="true"]` | ARIA STATE: open FAQ question | 1 |
| `button[aria-expanded="false"]` | ARIA STATE: closed FAQ questions | 2 |
| `[hidden]` | PRESENCE: hidden answer panels | 2 |
| `[aria-controls]` | PRESENCE: buttons that control a panel | 3 |
| `abbr[title]` | PRESENCE: abbreviations with a title tooltip | 5 |

## DT 4.2 - Pseudo-classes & Pseudo-elements  (`products.html`)

| Selector | What it demonstrates | Matches |
|---|---|---|
| **STRUCTURAL PSEUDO-CLASSES** | | |
| `article:nth-child(even)` | GOTCHA: cards 1 and 3, because the h2 is child #1 so the articles are children 2-5 | 2 |
| `article:nth-of-type(even)` | FIX: cards 2 and 4 (counts only article siblings) | 2 |
| `article:first-child` | GOTCHA: matches NOTHING, the h2 is the first child | 0 |
| `article:first-of-type` | first article (Road) | 1 |
| `article:last-child` | GOTCHA: matches NOTHING, the closing paragraph is the last child | 0 |
| `article:last-of-type` | last article (Kids) | 1 |
| `article li:first-child` | first spec in each card | 4 |
| `article li:last-child` | the Price line in each card | 4 |
| `article li:nth-child(odd)` | alternate spec lines | 8 |
| `tbody tr:nth-child(even)` | ZEBRA: even table rows | 4 |
| `tbody tr:nth-child(odd)` | ZEBRA: odd table rows | 4 |
| `tbody tr:last-child` | last table row | 1 |
| `tbody td:first-child` | first column | 8 |
| `tbody td:last-child` | last column (the View links) | 8 |
| `th:first-child` | first header cell | 1 |
| **USER-ACTION / STATE PSEUDO-CLASSES** | | |
| `article button` | targets for :hover / :focus / :focus-visible / :active | 4 |
| `button:disabled` | the Sold Out button | 1 |
| `input:disabled` | the Member ID field | 1 |
| `input:checked` | pre-checked radio and checkbox | 2 |
| `input:required` | required fields | 2 |
| `input:invalid` | required fields still empty | 2 |
| `input:checked + label` | label next to a checked control | 2 |
| `input[type='radio'] + label` | radio labels | 3 |
| `input[type='checkbox'] + label` | checkbox labels | 3 |
| `input[placeholder], textarea[placeholder]` | elements with ::placeholder text | 4 |
| **PSEUDO-ELEMENT HOOKS** | | |
| `article h3` | ::before / ::after badge or icon | 4 |
| `a[href$='.pdf']` | PDF links: add an icon with ::after | 4 |
| `article p:first-of-type` | ::first-letter / ::first-line | 4 |
| `li` | ::marker / ::before on list items (menu items + spec lines) | 25 |
| `nav ul ul a` | submenu links that jump to the cards (watch :target) | 4 |

## DT 4.3 - Advanced Backgrounds  (`about.html`)

| Selector | What it demonstrates | Matches |
|---|---|---|
| `header` | hero: cover + multiple backgrounds + gradient overlay | 1 |
| `#banner` | full-width band: cover / position / attachment / overlay | 1 |
| `#numbers li strong` | background-clip: text (gradient numbers) | 3 |
| `#mission blockquote` | border-image | 1 |
| `#team article` | tile pattern, contain logo, two layered backgrounds | 3 |
| `#team img` | portraits | 3 |
| `aside` | multiple backgrounds on a sidebar | 1 |
| `main > section` | the four bands | 5 |

## DT 4.4 - @font-face & Web Typography  (`history.html`)

| Selector | What it demonstrates | Matches |
|---|---|---|
| `h1` | page title (Oswald 700) | 1 |
| `h2` | section headings | 4 |
| `h3` | specimen subheadings | 4 |
| `p` | body text (Lora 400), whole page including tagline and footer | 12 |
| `em` | needs the Lora ITALIC file | 3 |
| `strong` | needs the 700 file | 8 |
| `cite` | italic attribution (Walt Hollander) | 1 |
| `blockquote` | quote styling | 1 |
| `time` | timeline years | 6 |
| `ol li` | timeline entries | 6 |
| `small` | fine print | 1 |

## Teaching moments built into the HTML

1. **`h2 + p` vs `p + h2` vs `h2 ~ p`** (index, `#guide`): five `h2`s in one section. Only some follow a paragraph, only some are followed by one, and `~` matches every later paragraph.
2. **`nav li` vs `nav > ul > li`** (index): the nested submenu makes descendant and child give different counts (9 vs 5).
3. **`nth-child` vs `nth-of-type`** (products, `#lineup`): the `h2` is child #1, so `article:nth-child(even)` picks cards 1 and 3. `nth-of-type(even)` picks 2 and 4. `article:first-child` matches nothing.
4. **`:target`** (products): the Products submenu links to `#road`, `#gravel`, `#ebike`, and `#kids`. Click one and the card becomes `:target`.
5. **Disabled and checked states** (products): the Sold Out button, the Member ID field, and one pre-checked radio and checkbox.
6. **`a[href$=".pdf"]::after`** (products): an attribute selector and a pseudo-element together, for a file-type icon.
7. **`background-clip: text`** (about, `#numbers li strong`): needs `color: transparent` plus the `-webkit-` prefix.
8. **`border-image`** (about, `#mission blockquote`): `images/border-frame.svg` is a 90px 3x3 image, so use slice `30`.
9. **Two font files per family** (history): `em` needs the Lora italic file. `strong` and headings need the 700 files. Show what happens without each one.
10. **`font-display: swap`**: throttle the network in DevTools to watch the fallback font swap.

## Note on the `aria-expanded` buttons

The FAQ buttons carry `aria-expanded` and `aria-controls`, but there is no JavaScript in this course, so they will not toggle. They are there as selector targets: `button[aria-expanded="true"]`, `button[aria-expanded="false"]`, and `[hidden]`.

## Files

- `images/`: 4 bike illustrations, `hero-hills.svg` (cover), `workshop-banner.svg` (cover/overlay), `tread-pattern.svg` (48px tile), `logo-mark.svg` (contain), `border-frame.svg` (border-image), `team-1..3.svg`
- `downloads/`: 6 PDFs, 1 GPX, 1 CSV, 1 ZIP (real files, so the file links and the `download` attribute work)
- `fonts/`: Oswald 400/700 and Lora 400/400-italic/700, each as `.woff2` and `.woff`, with their SIL Open Font License files
- All links to external sites use real domains. `example.com` and `.example` addresses are used for the fake legacy link and the shop's emails.
- The business, people, prices, and phone number are fictional.
