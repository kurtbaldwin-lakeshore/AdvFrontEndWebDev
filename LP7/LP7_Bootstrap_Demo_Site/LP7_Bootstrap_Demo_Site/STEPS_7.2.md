# DT 7.2 Bootstrap Grid and Components: demo steps

Start from `after-7.1/` (copy it). Finished state: `after-7.2/`.
Follows the 7 LIVE DEMO steps on the slide.

**1. CDN before your stylesheet.** Already in place from 7.1. Confirm the order: bootstrap.min.css, then `css/base.css`. Now add a new file `css/style.css` and link it **last**:
```html
<link rel="stylesheet" href="css/style.css">
```

**2. Navbar with full ARIA.** Replace the plain `<nav class="plain-nav">` with:
```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark" aria-label="Main">
  <div class="container">
    <a class="navbar-brand" href="index.html">Driftless Cycle Co.</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#mainNav"
            aria-controls="mainNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="mainNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link active" aria-current="page" href="index.html">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="contact.html">Contact</a></li>
      </ul>
    </div>
  </div>
</nav>
```
Narrow the window below 768px, click the toggler. In DevTools watch `aria-expanded` flip `false` to `true`.

**3. Three cards, `col-12 col-md-4`.** Replace the three demo columns with:
```html
<div class="row g-4">
  <div class="col-12 col-md-4">
    <div class="card h-100">
      <img src="images/bike-road.svg" class="card-img-top" alt="Road bike illustration">
      <div class="card-body d-flex flex-column">
        <h3 class="card-title h5">Road bike</h3>
        <p class="card-text">Light aluminium frame for fast pavement rides.</p>
        <div class="mt-auto d-flex gap-2">
          <!-- step 4 goes here -->
        </div>
      </div>
    </div>
  </div>
  <!-- repeat for bike-gravel.svg and bike-ebike.svg -->
</div>
```

**4. Buttons in each card.**
```html
<a href="#" class="btn btn-primary">View bike</a>
<a href="#" class="btn btn-outline-secondary">Compare</a>
```

**5. Inspect in DevTools.** Click `.row`, `.col-md-4`, `.card`, and `.card-body`: all `display: flex`. Bootstrap's grid is the LP5 flexbox.

**6. Custom class on one card.** On the middle card add `card-featured`. In `css/style.css`:
```css
.card-featured {
  background-color: #fffaf0;
  border: 2px solid #9a4a00;
}
```

**7. Verify the load order (the memorable part).** In DevTools drag `style.css`'s `<link>` above Bootstrap's in the Elements panel (or reorder in the file and reload). The card goes back to white: Bootstrap now wins. Put it back, the override works.

## Extras in the finished 7.2 page (use as time allows)
- Dismissible `alert` with `role="alert"` at the top of `<main>`.
- Modal: "Book a bike fitting" button, `role="dialog"`, `aria-modal="true"`, `aria-labelledby` pointing at the real title id. Tab around: focus stays inside. Escape closes and focus returns to the button.
- `contact.html`: floating-label form. Floating labels only work if each input has a `placeholder` attribute.
