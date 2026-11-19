# DT 7.3 Bootstrap Customization: demo steps

Start from `after-7.2/`. Finished state: `after-7.3/`.
All edits go in `css/style.css`, which loads after Bootstrap.

**1. Brand color.** Add at the top of `style.css`:
```css
:root {
  --bs-primary: #0f5c4d;
  --bs-primary-rgb: 15, 92, 77;   /* always change both together */
}
```
Reload. Say what changes: `.bg-primary`, `.text-primary`, the badge. Say what does **not**: the buttons are still blue (and later, the progress bar and accordion). Bootstrap 5.3 buttons have their own `--bs-btn-*` variables. Fix:
```css
.btn-primary {
  --bs-btn-bg: var(--bs-primary);
  --bs-btn-border-color: var(--bs-primary);
  --bs-btn-hover-bg: #0a3f35;
  --bs-btn-hover-border-color: #0a3f35;
  --bs-btn-active-bg: #083229;
  --bs-btn-active-border-color: #083229;
  --bs-btn-disabled-bg: var(--bs-primary);
  --bs-btn-disabled-border-color: var(--bs-primary);
  --bs-btn-focus-shadow-rgb: 15, 92, 77;
}
```
Also set the link color (this fixes the breadcrumb/link contrast the 7.1 slide warned about):
```css
:root {
  --bs-link-color: #0f5c4d;
  --bs-link-color-rgb: 15, 92, 77;
  --bs-link-hover-color: #0a3f35;
  --bs-link-hover-color-rgb: 10, 63, 53;
}
```

Bonus: the form focus ring is also hard-coded blue. Click into a contact form field to show it, then fix:
```css
.form-control:focus {
  border-color: var(--bs-primary);
  box-shadow: 0 0 0 0.25rem rgba(var(--bs-primary-rgb), 0.25);
}
```

**2. Font.** In `<head>`, before `css/base.css`:
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible:wght@400;700&display=swap">
```
```css
:root {
  --bs-body-font-family: 'Atkinson Hyperlegible', system-ui, -apple-system, 'Segoe UI', Roboto, sans-serif;
}
```

**3. Corner style.**
```css
:root {
  --bs-border-radius: 0.75rem;
  --bs-border-radius-lg: 1rem;
}
```
Cards, buttons, alerts and form fields all round together. That is the payoff of variables.

**4. Transitions on `.card` and `.btn-primary`** (LP3):
```css
.card { transition: transform 0.2s ease, box-shadow 0.2s ease; }
.btn-primary { transition: background-color 0.2s ease, border-color 0.2s ease, transform 0.2s ease; }
.btn-primary:hover { transform: translateY(-1px); }
```

**5. Shadow on `.card:hover`** (LP2):
```css
.card:hover {
  box-shadow: 0 0.75rem 1.5rem rgba(27, 36, 32, 0.18);
  transform: translateY(-4px);
}
```
Then add the reduced-motion reset so it covers the new transitions:
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
  .card:hover, .btn-primary:hover { transform: none; }
}
```

**6. Reload.** Components reflect the brand.

**7. Compare with `after-7.2/` side by side.** Same HTML, different look. The slide's goal: a reviewer should not immediately recognize it as Bootstrap.

## Accessibility Spotlight: re-test contrast
Open WebAIM Contrast Checker with `#ffffff` on `#0f5c4d` (button text) and `#0f5c4d` on `#f5f6f2` (links). Both pass AA comfortably. Bootstrap's default `#0d6efd` link on the page background `#f5f6f2` is about 4.14:1 and fails, so changing the link color was an accessibility fix, not just style.
