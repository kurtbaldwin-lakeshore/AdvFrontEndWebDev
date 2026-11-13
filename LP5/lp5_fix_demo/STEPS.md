# LP5 live demo: Fixed to Responsive (Wisconsin State Fair)

Start from the original starter in `step0/` (exactly the LP5_starter files). Each later folder
(`step1` ... `step10`) is the finished result of that step, so you can type live or jump ahead.
The photos in these folders are color placeholders. Copy the real fair-logo.png, cream-puffs.jpg,
livestock.jpg, and ferris-wheel.jpg into the folder you demo from.

Setup: open index.html in the browser, press F12, turn on the device toolbar (Ctrl+Shift+M),
and start at 375px wide. Drag the width wider as you go.

---------------------------------------------------------------------------
## Step 0: Show the problem (no typing)
- At 375px the page scrolls sideways (the page is 960px wide, images are 600px wide).
- Drag wider: the sidebar sits UNDER the content, even on a big screen, and nothing changes at 600px or 1024px.
- Ask: "What is fixed here?" Answer: `.page` 960px, `.layout` 960px, `.content` 680px, `.sidebar` 240px,
  `.feature-img` 600px, `.logo` 120px, h1 36px, and two `float: left`.

## Step 1: Add the viewport meta tag (index.html)
In `<head>`, right after `<meta charset="UTF-8">`, add:

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

Why: without it, a real phone pretends to be ~980px wide and your media queries never fire.
(You won't see a change in the desktop browser. Say so.)

## Step 2: box-sizing: border-box, globally (style.css)
The starter has no box-sizing rule. Under the top comment, replace lines 3-6:

BEFORE
       Fixed-width starter stylesheet — this is the "before" version.
       Your job: convert this to a fully responsive, mobile-first, Flexbox
       layout. See the LP5 Formative Lab instructions for exact requirements.
       ========================================================================== */

AFTER
       Mobile-first and responsive: base styles are the phone layout.
       min-width media queries at 600px and 1024px add the larger layouts.
       ========================================================================== */

    *, *::before, *::after {
      box-sizing: border-box;
    }

WHAT YOU SEE: the sidebar jumps up beside the content. Before, 680px + 48px of padding plus
240px + 48px of padding was wider than 960px, so the sidebar dropped. Now padding is inside the width.

## Step 3: Make the base layout the phone layout (style.css)
Three edits.

(a) `.page`: delete the comment line above it, and change `width: 960px;` to `max-width: 1200px;`

BEFORE
    /* Fixed pixel width — does not adapt to any screen size. */
    .page {
      width: 960px;
      margin: 0 auto;
      background: #fff;
    }
AFTER
    .page {
      max-width: 1200px;
      margin: 0 auto;
      background: #fff;
    }

(b) Replace the whole "Two fixed-width columns" block (.layout, .content, .sidebar):

BEFORE
    /* Two fixed-width columns using float — not responsive, and not Flexbox. */
    .layout {
      width: 960px;
      overflow: hidden;
    }

    .content {
      width: 680px;
      float: left;
      padding: 24px;
    }

    .sidebar {
      width: 240px;
      float: left;
      padding: 24px;
      background: #f4ede1;
    }
AFTER
    /* Mobile first: one column. .layout is the flex container. */
    .layout {
      display: flex;
      flex-direction: column;
    }

    .content {
      padding: 24px;
    }

    .sidebar {
      padding: 24px;
      background: #f4ede1;
    }

WHAT YOU SEE: the 960px layout is gone, the sidebar stacks under the content, and the page fills
the window. At 375px it STILL scrolls sideways because the 600px images are next. That is step 4.

## Step 4: Responsive images (style.css)
Two edits.

(a) `.logo`: remove the comment and add a global `img` rule above it.

BEFORE
    .logo {
      /* Fixed pixel width on an image — will overflow on small screens. */
      width: 120px;
    }
AFTER
    img {
      max-width: 100%;
      height: auto;
    }

    .logo {
      width: 120px;
    }

(b) `.feature-img`: delete the comment, delete `width: 600px;`, add `display: block;`

BEFORE
    /* Fixed pixel width on content images — will overflow at small
       viewport widths instead of scaling down. */
    .feature-img {
      width: 600px;
      border-radius: 6px;
      margin-top: 8px;
    }
AFTER
    .feature-img {
      display: block;
      border-radius: 6px;
      margin-top: 8px;
    }

WHAT YOU SEE: the sideways scroll is gone at every width. Images now fill their card and scale down.

## Step 5: Flex nav and the first breakpoint (600px)
(a) `.site-nav`: add three lines.

BEFORE
    .site-nav {
      background: #591616;
      padding: 12px 24px;
    }
AFTER
    .site-nav {
      background: #591616;
      padding: 12px 24px;
      display: flex;
      flex-direction: column;     /* phone: links stack */
      gap: 8px;
    }

(b) `.site-nav a`: delete the last line `margin-right: 24px;` (the gap replaces it).

(c) At the very bottom of the file, add the first media query:

    @media (min-width: 600px) {
      .site-nav {
        flex-direction: row;      /* tablet: links sit in a row */
        gap: 24px;
      }
    }

WHAT YOU SEE: the links stack on a phone and sit in a row from 600px up.

## Step 6: Cards in two columns at 600px (inside the 600px query)
Add these after the `.site-nav` rule, inside the same `@media (min-width: 600px) { }`:

    .content {
      display: flex;
      flex-wrap: wrap;          /* cards wrap into rows */
      gap: 16px;
    }

    .content h2 {
      flex: 1 1 100%;           /* heading takes a full row */
      margin: 0;
    }

    .schedule-card {
      flex: 1 1 280px;          /* two per row when there is room */
      margin-bottom: 0;
    }

WHAT YOU SEE: 1 card per row on a phone, 2 per row at 800px, equal heights in each row.
Tie it back to 5.2: `flex: 1 1 280px` = grow 1, shrink 1, start at 280px.

## Step 7: Sidebar beside the content at 1024px
Add a second media query at the very bottom of the file:

    @media (min-width: 1024px) {
      .layout {
        flex-direction: row;      /* desktop: content and sidebar side by side */
      }

      .content {
        flex: 3;
      }

      .sidebar {
        flex: 1;
      }
    }

WHAT YOU SEE: at 1024px and wider, content and sidebar sit side by side (3 : 1). Below 1024 the
sidebar stays underneath.

## Step 8: Fluid heading with clamp()
BEFORE
    .site-header h1 {
      font-size: 36px;
      margin: 8px 0 4px;
    }
AFTER
    .site-header h1 {
      font-size: clamp(1.75rem, 1.25rem + 2vw, 2.5rem);
      margin: 8px 0 4px;
    }

WHAT YOU SEE: the heading is 28px on a phone, grows with the window, and stops at 40px.
Talk through the three values: minimum, preferred (scales with the screen), maximum.

## Step 9: Carry the reduced-motion reset forward (from LP3)
Add at the very bottom of style.css:

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
    }

(This page has no animation. The assignment still requires the reset in the file.)

## Step 10: Skip link (index.html and style.css)
index.html: first line inside `<body>`:

    <a class="skip-link" href="#main-content">Skip to main content</a>

and add an id to the main element:

    <main class="content" id="main-content">

style.css: add above the `.page` rule:

    /* Skip link: hidden until it gets keyboard focus */
    .skip-link {
      position: absolute;
      left: -999px;
      top: 0;
      z-index: 10;
      padding: 8px 16px;
      background: #000;
      color: #fff;
    }

    .skip-link:focus {
      left: 0;
    }

Press Tab once to show it appear.

## Step 11: Validate (do this live)
1. W3C CSS validator: https://jigsaw.w3.org/css-validator/ (paste style.css). Expect zero errors.
   Also run index.html through https://validator.w3.org/nu/
2. Lighthouse: DevTools > Lighthouse > Accessibility only > Analyze. Expect 90 or higher.
3. Check the rubric: no `float` anywhere in the CSS (search the file for the word), min-width queries
   at 600px and 1024px only, max-width: 100% on every image, clamp() on the h1, border-box, reduced-motion.

---------------------------------------------------------------------------
Rubric map: viewport + steps 3, 5, 6, 7 = Mobile-First & Breakpoints. Steps 2, 3, 5, 6, 7 = Flexbox.
Steps 4 and 8 = Images & Typography. Steps 9 and 11 = Validation & Accessibility.
