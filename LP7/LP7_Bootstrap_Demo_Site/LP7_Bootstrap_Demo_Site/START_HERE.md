# LP7 Bootstrap Demo: Driftless Cycle Co.

One site, four demos. Each folder is a complete, working site.

| Folder | Use it |
|---|---|
| `starter/` | Start of 7.1. The plain Driftless page, no Bootstrap. |
| `after-7.1/` | What the site looks like at the end of 7.1. Start 7.2 from here. |
| `after-7.2/` | End of 7.2. Start 7.3 from here. |
| `after-7.3/` | End of 7.3. Start 7.4 from here. |
| `finished/` | End of 7.4. Everything on. Your answer key. |

Step guides: `STEPS_7.1.md` to `STEPS_7.4.md`. Each lists the exact LIVE DEMO steps from the slides with the code to type.

## Before you record
- Bootstrap loads from the **CDN** (cdn.jsdelivr.net, version 5.3.2, with the SRI `integrity` hashes), exactly as the 7.1 slide shows. You need an internet connection.
- The 7.3 font (Atkinson Hyperlegible) loads from Google Fonts. Offline, the page falls back to the system font and still works.
- Every page has the skip link in the body and its CSS in `base.css`.
- Use a Live Server or just open the files in Chrome.

## Things to know on camera
1. **Buttons ignore `--bs-primary`.** In Bootstrap 5.3, `.btn-primary` has its own `--bs-btn-*` variables. Changing `--bs-primary` recolors `.bg-primary`, `.text-primary` and the badge (and, with `--bs-link-color`, links), but not the button, the progress bar, the accordion's open state or the form focus ring. Those carry their own hard-coded blues. 7.3 step 1 shows this on purpose and fixes the button and form focus ring. The 7.4 checkpoint fixes the progress bar, accordion and dropdown the same way.
2. **Contrast finding.** After 7.2, the breadcrumb link (Bootstrap blue on the off-white page) is the kind of thing a contrast check flags (4.14:1). 7.3 sets `--bs-link-color` to the brand green. A good moment to run WebAIM again, as the 7.1 and 7.3 slides promise.
3. **Fine to say out loud:** Bootstrap adds `role="dialog"` and `aria-modal` at runtime, but we write them in the HTML anyway, per the slides.
