# DT 7.4 Bootstrap Components Deep Dive: demo steps

Start from `after-7.3/`. Finished state: `finished/`.
Follows the 7 LIVE DEMO steps on the slide. For each component, open the docs page, copy the Example, then fix the accessibility details.

**1. Confirm the CDN.** Bootstrap CSS, then base.css, then style.css; JS bundle before `</body>`. Nothing to add.

**2. Accordion (new `faq.html`), wrap each button in `<h3>`.** Docs: getbootstrap.com/docs/5.3/components/accordion/
```html
<div class="accordion" id="faqList">
  <div class="accordion-item">
    <h3 class="accordion-header">
      <button class="accordion-button" type="button" data-bs-toggle="collapse"
              data-bs-target="#faq0" aria-expanded="true" aria-controls="faq0">How long does a repair take?</button>
    </h3>
    <div id="faq0" class="accordion-collapse collapse show" data-bs-parent="#faqList">
      <div class="accordion-body">Most tune-ups are done in two days.</div>
    </div>
  </div>
  <!-- more items: collapsed button class, aria-expanded="false", no "show" -->
</div>
```
Page needs an `<h2>` above the `<h3>`s so the heading order makes sense. Optional: breadcrumb `<nav aria-label="breadcrumb">` with `aria-current="page"` on the last item.

**3. Carousel on `index.html`, add `aria-label` to every indicator.** Docs: .../components/carousel/
```html
<div id="gallery" class="carousel slide" data-bs-ride="false" role="region" aria-label="Shop photo gallery">
  <div class="carousel-indicators">
    <button type="button" data-bs-target="#gallery" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1: The shop on Main Street"></button>
    <button type="button" data-bs-target="#gallery" data-bs-slide-to="1" aria-label="Slide 2: Road bikes"></button>
    <button type="button" data-bs-target="#gallery" data-bs-slide-to="2" aria-label="Slide 3: Gravel bikes"></button>
  </div>
  <div class="carousel-inner">
    <div class="carousel-item active"><img src="images/shop.svg" class="d-block w-100" alt="Driftless Cycle Co. storefront with green sign"></div>
    <!-- two more .carousel-item -->
  </div>
  <button class="carousel-control-prev" type="button" data-bs-target="#gallery" data-bs-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span><span class="visually-hidden">Previous slide</span>
  </button>
  <button class="carousel-control-next" type="button" data-bs-target="#gallery" data-bs-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span><span class="visually-hidden">Next slide</span>
  </button>
</div>
```

**4. `data-bs-ride="false"`** is already in the code above. Say why: auto-moving content fails WCAG 2.2.2 Pause, Stop, Hide. Wait 10 seconds on camera: nothing moves.

**5. Dropdown in the navbar.** Docs: .../components/dropdowns/. In `<ul class="navbar-nav">`, before FAQ:
```html
<li class="nav-item dropdown">
  <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">Group Rides</a>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#">Saturday gravel loop</a></li>
    <li><a class="dropdown-item" href="#">Tuesday road night</a></li>
    <li><hr class="dropdown-divider"></li>
    <li><a class="dropdown-item" href="#">Ride safety</a></li>
  </ul>
</li>
```
Also add a FAQ link to the nav.

**6. Keyboard test.**
- Tab to the accordion button: Enter opens it.
- Tab to the carousel: nothing auto-plays. Tab to the arrows, Enter advances.
- Tab to Group Rides: Enter opens, Arrow keys move, Escape closes and focus returns to the toggle.

**7. DevTools.** Elements, click an accordion button. Click the header and watch `aria-expanded` flip `false` to `true` live. Say: Bootstrap's JS updates it, you only write the starting value.

## Brand the new components (same lesson as 7.3)
After adding the accordion and progress bar, they show Bootstrap blue even though `--bs-primary` is green. Add to `css/style.css`:
```css
.progress { --bs-progress-bar-bg: var(--bs-primary); }
.accordion {
  --bs-accordion-active-color: #0a3f35;
  --bs-accordion-active-bg: #e3efec;
  --bs-accordion-btn-focus-border-color: var(--bs-primary);
  --bs-accordion-btn-focus-box-shadow: 0 0 0 0.25rem rgba(15, 92, 77, 0.25);
}
.dropdown-menu { --bs-dropdown-link-active-bg: var(--bs-primary); }
```
(The finished `style.css` also swaps the accordion's open chevron color; copy it from there if you want it.) The rule of thumb: after adding any component, look for leftover Bootstrap blue.

## Extras in the finished page
Badge with hidden text (`New<span class="visually-hidden"> this season</span>`), progress bar with `role="progressbar"`, `aria-labelledby`, `aria-valuenow/min/max`.

## Docs-reading workflow (slide 10)
Live demo with a component you have not covered: getbootstrap.com/docs/5.3/components/offcanvas/. Find the Example, copy the HTML, find the JS section, read the Accessibility section, then keyboard test.
