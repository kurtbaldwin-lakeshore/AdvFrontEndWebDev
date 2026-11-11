MILWAUKEE BREWERS FAN GUIDE - CLASSROOM DEMO

Open index.html in Chrome.

Pages:
- index.html
- history.html
- ballpark.html
- legends.html
- contact.html
- navigation-demo.html

Stylesheet:
- css/styles.css

Images:
- images/*.svg

This project was intentionally written at an introductory HTML/CSS level.

Baseline accessibility/semantic features now included on every page:
- <html lang="en">
- Skip-to-main-content link immediately after <body>
- <header>, <nav>, <main id="main">, and <footer>
- aria-current="page" on the active navigation link

The deliberate validator/Lighthouse issues listed below remain intentionally unchanged.

It includes deliberate minor issues for validator / Lighthouse demonstrations:
1. Duplicate id="feature-card" on history.html.
2. Missing alt attribute on one image on ballpark.html.
3. Unlabeled optional phone input on contact.html.
4. Misspelled CSS property: font-weigth.
5. Invalid CSS float value: float: center.
6. Some secondary text uses relatively low contrast.

The content is educational and unofficial. It is not affiliated with MLB or the Milwaukee Brewers.
Primary factual references are cited in HTML comments, including MLB Brewers history and retired-number pages.


Navigation Demo page:
- Contains a deliberately large nested dropdown navigation menu.
- Uses nested UL elements with basic CSS.
- Designed to demonstrate keyboard tab order and why skip links matter.
- Uses :hover and :focus-within so dropdowns can be explored by mouse or keyboard.
