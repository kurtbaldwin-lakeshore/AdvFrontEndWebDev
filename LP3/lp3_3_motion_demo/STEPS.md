# Reduced-motion demo (DT 3.3)

Open index.html. style.css has NO prefers-reduced-motion rule. You add it live.

## What is on the page
1. Entrance animations (play once on load): h1 slides in, paragraph and three cards fade up with a stagger.
2. Loops that never stop: drifting circles, pulsing yellow button, scrolling banner, and six tiles
   (spin, bounce, pulse, wiggle, slide, blink).
3. Hover and focus changes: a color-swap card, a color + lift card, and a button (hover or Tab to them).

## Demo order
1. Show the page as delivered. Everything moves. Reload to replay the entrance animations.
2. Turn ON Reduce motion in the operating system (Windows 11: Settings > Accessibility > Visual effects >
   Animation effects OFF. Mac: System Settings > Accessibility > Display > Reduce motion).
   Reload. NOTHING changes, because the CSS does not ask the browser about that setting yet.
   This is the key point: the OS setting only works if your CSS listens for it.
3. Add this to the bottom of style.css and reload:

    @media (prefers-reduced-motion: reduce) {
      *,
      *::before,
      *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
      }
    }

   With the OS setting on, the loops stop, the entrance animations just appear, and the banner is still.
4. Show hover and Tab on section 3: the colors still change (and the card still ends up lifted).
   Explain: we removed the motion, not the feedback. Transitions become instant, not gone.
5. Turn the OS setting OFF and reload: the animations are back. Same CSS, different user.
6. Repeat with DevTools instead of the OS setting:
   F12 > Ctrl+Shift+P > type "reduced motion" > "Emulate CSS prefers-reduced-motion: reduce".
   (Rendering tab: "Emulate CSS media feature prefers-reduced-motion".) Reload to replay the load animations.
7. Optional: comment out `animation-iteration-count: 1 !important;` and reload with reduce on.
   The loops keep flickering at 0.01ms. That line is what actually stops them.

## Notes
- All keyframes use only transform and opacity (an LP3 requirement).
- The skip link is the first Tab stop.
- The blink animation is slow (1s) on purpose. Fast flashing can trigger seizures.
