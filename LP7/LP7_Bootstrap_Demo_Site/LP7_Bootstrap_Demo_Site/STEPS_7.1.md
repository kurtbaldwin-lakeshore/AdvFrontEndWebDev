# DT 7.1 Introduction to Bootstrap: demo steps

Start from `starter/`. Finished state: `after-7.1/`.
Slide 4 (CDN), slide 5 (grid), slide 6 (utilities), slide 7 (accessibility demo cue).

## Part A: Add Bootstrap (slide 4)
1. Open `starter/index.html`. Point out: no Bootstrap yet, plain Driftless page.
2. In `<head>`, add the CSS link **before** `css/base.css`:
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
      integrity="sha384-T3c6CoIi6uLrA9TneNEoa7RxnatzjcDSCmG1MXxSR1GAsXEV/Dwwykc2MPK8M2HN" crossorigin="anonymous">
```
3. Keep `<link rel="stylesheet" href="css/base.css">` **after** it. Say: Bootstrap first, your CSS second.
4. Add the JS bundle just before `</body>`:
```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-C6RzsynM9kWDrMNeT87bh95OGNyZPhcTNXj1NW7RuBCsyN/o0jlpcV8Qyq46cDfL" crossorigin="anonymous"></script>
```
5. Say what `integrity` and `crossorigin` are: SRI, verifies the CDN file was not changed.
6. Test the connection: change `<main id="main">` to `<main id="main" class="container py-4">`. Content is centered with a max width. Resize the window.
7. Note for the video: the checkpoint `base.css` is trimmed (body font, colour and link rules removed) so Bootstrap's variables can control them in 7.3. Mention it once.

## Part B: 12-column grid (slide 5)
Inside `<main>` add:
```html
<div class="row g-3">
  <div class="col-12 col-md-6 col-lg-4"><div class="bg-primary text-white p-4">Column one</div></div>
  <div class="col-12 col-md-6 col-lg-4"><div class="bg-primary text-white p-4">Column two</div></div>
  <div class="col-12 col-md-6 col-lg-4"><div class="bg-primary text-white p-4">Column three</div></div>
</div>
```
Resize: 1 column below 768px, 2 columns at 768px, 3 columns at 992px. Open DevTools on `.row`: `display: flex` (the LP5 flexbox).

## Part C: Utilities (slide 6)
```html
<div class="d-flex justify-content-between align-items-center mt-4 mb-2 px-3 py-2 bg-light border">
  <span class="fw-bold">Utility classes at work</span>
  <span class="d-none d-md-block">Hidden on phones, shown from 768px</span>
</div>
```
Point out: no custom CSS written. Also mention the trade-off in the slide notes (cluttered HTML).

## Part D: Accessibility Spotlight (slide 7)
1. Open `after-7.1/nav-demo.html`. Two identical-looking bars.
2. DevTools, Accessibility panel (Elements, Accessibility tab): the `<nav>` one has a **navigation** landmark. The `<div class="navbar">` one does not.
3. Plant the seed: "We re-test contrast in 7.3."
