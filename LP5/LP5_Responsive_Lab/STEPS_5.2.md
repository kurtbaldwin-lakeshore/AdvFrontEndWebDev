# 5.2 Live Demo: Flexbox Card Grid (`products.html`, `css/5-2.css`)

These are the seven steps on the DT 5.2 slide. The page starts with floated, fixed-width cards. The HTML does not change. Open `starter/products.html` and `css/5-2.css`. CSS after each step: `steps/5-2/stepN.css` (steps 0, 1, 2, 3, 6, 7 have files; steps 4 and 5 are tests).

## What is broken in the starter
Six cards float left at 300px wide. They do not stretch to equal heights, the yellow "New rider? Start here" box slides up behind them with its text wrapping around the floats, and 300px plus margins cannot fit a 320px screen (it scrolls sideways at 320).

| Step | Change | What you will see |
|---|---|---|
| 1 | Delete the float rule. Add `.card-grid { display: flex; flex-wrap: wrap; gap: 1.5rem; }` | Cards sit in the flex container, but each is sized by its own text: at 1000px the widths are 968, 348, 968, 968, 968 and 151px. Long cards take a whole row and short ones are narrow, so the grid is ragged |
| 2 | Add `.card { flex: 1 0 280px; max-width: 400px; }` | Every card becomes the same width (307px each at 1000px), three per row. They grow to fill each row, never shrink below 280px, and stop at 400px |
| 3 | Style the card content: padding, radius, shadow, heading margin, and a green button (the heading, description and button are already in the HTML) | A finished-looking card |
| 4 | Resize the browser (no code) | 1 column at 320 to about 600px, 2 columns at 800, 3 columns at 1000 and 1440 |
| 5 | Test at 320px (no code) | Each card is full width (288px) and there is no sideways scroll |
| 6 | Add `.card { transition: transform 0.25s ease-out, box-shadow 0.25s ease-out; }` | Nothing yet. There is no hover state |
| 7 | Add `.card:hover, .card:has(:focus-visible) { transform: translateY(-4px); box-shadow: 0 8px 20px rgba(0,0,0,0.2); }` | Hover lifts a card. Tab to a button and the whole card lifts too (the card itself is not focusable, so `:has()` lifts it when its button is focused) |

## Talking points
- No media query anywhere. The cards go 3 to 2 to 1 because `flex-wrap` lets them wrap and `flex-basis: 280px` decides when they no longer fit. At 600px you will see one card 400px wide, not full width: two 280px cards plus the gap are 584px, which does not fit in 568px, and `max-width: 400px` stops the single card at 400px. Good moment to ask "is that what we want?"
- `flex: 1 0 280px` means grow 1, shrink 0, basis 280px. Without `shrink 0` the cards would squash below 280px instead of wrapping.
- `gap` replaces the margin hacks from the floated version.
- The bigger point: this is what "intrinsic" responsive means. The layout follows the space, so 320px works without a 320px query.

## Extras (they are commented out at the bottom of `5-2.css`; uncomment one at a time)
- **`align-self`**: `.card.featured { align-self: flex-start; }`. Cards normally stretch to the same height (the tallest is about 295px). The Fall Swap Meet card keeps its natural 171px.
- **`order` and keyboard order (accessibility caution)**: `.content { display: flex; flex-direction: column; } .promo { order: -1; }`. The yellow promo box jumps ABOVE the cards, but press Tab: focus visits all the card buttons first and the promo link last (measured). Sighted keyboard users see focus jump from the top of the page to the bottom. Fix it by putting the promo first in the HTML instead of using `order`.

## Not run
Lighthouse and the W3C CSS validator.
