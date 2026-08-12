# Build a Responsive Grid
Responsive web design used to mean writing dozens of media queries (@media) to snap columns into place at specific viewport widths. If you missed a breakpoint, your layout would break.

Modern CSS Grid changes this paradigm. By using the mathematical formula repeat(auto-fit, minmax(300px, 1fr)), you can build a self-sorting, highly responsive card grid that calculates its own columns based on available space—writing zero media queries in the process.

In this hands-on lab, you will act as a Front-End Engineer building an Interactive Media Gallery Portal that adapts to any screen size instantly.

## Provided Code

<details>
  <summary><b>Click to expand and view the HTML code</b></summary>
  
``` html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta
            name="description"
            content="PUSH Magazine Week 02 — an accessible OKLCH palette and fluid type study."
        >
        <title>Week 02 — Color in Motion</title>
        <link rel="stylesheet" href="./styles.css">
    </head>
    <body>
        <a class="skip-link" href="#main-content">Skip to content</a>

        <header class="site-header">
            <a
                class="wordmark"
                href="../"
                aria-label="Return to PUSH Magazine home"
            >
                PUSH<span>®</span>
            </a>
            <p>Week 02 / Design systems</p>
            <nav class="site-actions" aria-label="Display preferences">
                <button
                    class="theme-toggle"
                    type="button"
                    aria-label="Switch color theme"
                    aria-pressed="false"
                    data-theme-toggle
                >
                    <span class="skateboard" aria-hidden="true">
                        <span class="skateboard__deck"></span>
                        <span class="skateboard__truck skateboard__truck--front"></span>
                        <span class="skateboard__truck skateboard__truck--back"></span>
                    </span>
                </button>
            </nav>
        </header>

        <main id="main-content">
            <section class="hero" aria-labelledby="page-title">
                <p class="eyebrow">Color in motion / 2026</p>
                <h1 id="page-title">Built to<br><em>contrast.</em></h1>
                <div class="hero-meta">
                    <p>
                        A black-led OKLCH palette with red energy, a purple counter-accent,
                        and a title scale that moves from pocket screen to desktop without a
                        breakpoint.
                    </p>
                    <span aria-hidden="true">↘</span>
                </div>
            </section>

            <section class="palette" aria-labelledby="palette-title">
                <div class="section-heading">
                    <p>01 / Designing the palette</p>
                    <h2 id="palette-title">Black leads.<br>Red hits. Purple cuts.</h2>
                </div>

                <div class="swatches">
                    <article class="swatch swatch--light">
                        <div>
                            <p>Light mode</p>
                            <strong>Aa</strong>
                        </div>
                        <dl>
                            <div>
                                <dt>Background</dt>
                                <dd>oklch(96% 0.015 90)</dd>
                            </div>
                            <div>
                                <dt>Text</dt>
                                <dd>oklch(14% 0.025 275)</dd>
                            </div>
                        </dl>
                        <p class="ratio">17.75:1 <span>AAA</span></p>
                    </article>

                    <article class="swatch swatch--dark">
                        <div>
                            <p>Dark mode</p>
                            <strong>Aa</strong>
                        </div>
                        <dl>
                            <div>
                                <dt>Background</dt>
                                <dd>oklch(14% 0.025 275)</dd>
                            </div>
                            <div>
                                <dt>Text</dt>
                                <dd>oklch(96% 0.015 90)</dd>
                            </div>
                        </dl>
                        <p class="ratio">17.75:1 <span>AAA</span></p>
                    </article>
                </div>

                <div class="explanation">
                    <h3>Why these L values?</h3>
                    <div>
                        <p>
                            OKLCH <code>L</code> runs from 0 (black) to 1 (white) and is
                            perceptually uniform, so a large gap is a strong starting point:
                            <strong>0.96 − 0.14 = 0.82</strong> in light mode and
                            <strong>0.96 − 0.14 = 0.82</strong> in dark mode.
                        </p>
                        <p>
                            WCAG does not calculate contrast from that L gap directly. After
                            converting each color to linear sRGB, it uses
                            <code>(Llighter + 0.05) / (Ldarker + 0.05)</code>. These pairs
                            produce 17.75:1 in both modes—well above AA’s 4.5:1 requirement for
                            normal text.
                        </p>
                    </div>
                </div>
            </section>

            <section class="scale" aria-labelledby="scale-title">
                <div class="section-heading">
                    <p>02 / Calculating fluid scales</p>
                    <h2 id="scale-title">Type that finds<br>its own line.</h2>
                </div>

                <div class="scale-demo">
                    <p class="demo-label">Resize the viewport</p>
                    <p class="fluid-title">Streets are the studio.</p>
                    <div class="ruler" aria-hidden="true">
                        <span>375px / 1.75rem</span>
                        <i></i>
                        <span>1440px / 3rem</span>
                    </div>
                </div>

                <div class="formula">
                    <p>Production value</p>
                    <code>--title-size: clamp(1.75rem, 1.3099rem + 1.8779vw, 3rem);</code>
                </div>

                <ol class="math">
                    <li>
                        <span>01</span>
                        <div>
                            <h3>Convert the endpoints</h3>
                            <p>At a 16px root size: 1.75rem = 28px and 3rem = 48px.</p>
                        </div>
                    </li>
                    <li>
                        <span>02</span>
                        <div>
                            <h3>Find the slope</h3>
                            <p>
                                (48 − 28) ÷ (1440 − 375) = 0.018779px per viewport pixel.
                                Multiply by 100 to express it as <strong>1.8779vw</strong>.
                            </p>
                        </div>
                    </li>
                    <li>
                        <span>03</span>
                        <div>
                            <h3>Find the intercept</h3>
                            <p>
                                28 − (0.018779 × 375) = 20.9577px. Divide by 16 to get
                                <strong>1.3099rem</strong>.
                            </p>
                        </div>
                    </li>
                </ol>
            </section>
        </main>

        <footer>
            <a href="../">← Issue index</a>
            <p>PUSH Magazine / Week 02</p>
            <p>Fall down. Get up.</p>
        </footer>
        <script src="../theme-toggle.js"></script>
    </body>
</html>
```

</details>

## AI Generation Tools
### Requirements
1.**Initialize Box Model & Core Reset:**
Instruct the AI to reset margins and paddings globally and set up a basic, fluid design theme with relative typography units.

2.**Define the Auto-Fit Grid Formula:**
Prompt the AI to style .grid-container using display: grid. It must explicitly declare its columns using grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)). Set a flexible spacing gutter using the gap property.

3.**Style Card Layout & Proportions:**
Format the .media-card components. Use CSS Flexbox inside each card to ensure the card's text body sits nicely beneath the image, and that all cards in the grid stretch to match each other's height automatically.

### Prompt Blueprint for Your AI Peer
"I need to write a modern, highly responsive CSS file for this gallery page [paste HTML]. The .grid-container must layout its child cards using CSS Grid. You must use the formula repeat(auto-fit, minmax(300px, 1fr)) for grid-template-columns. I want the layout to handle responsiveness entirely on its own—the use of @media screen breakpoints for sizing columns is strictly forbidden. Please use relative spacing properties (like em/rem/%) and explain how the browser decides when to wrap cards using auto-fit and minmax()."

#### Generated Explanation
How auto-fit + minmax() decides wrapping
Each grid track is constrained to minmax(300px, 1fr): 300px is the floor, and 1fr is the ceiling (an equal share of remaining space). The browser's grid algorithm:

Calculates how many 300px tracks can fit in the container's content-box width (dividing available width by 300px, rounding down).
auto-fit collapses any leftover empty tracks to 0px (as opposed to auto-fill, which would leave them as empty gaps), so the tracks that do have content stretch via 1fr to consume all remaining space evenly.
As the viewport shrinks, the browser continuously recomputes that count — the moment there isn't room for another full 300px column plus the required gap, it drops a column and redistributes width to the rest. Below 300px + padding, only one column fits and cards stack vertically.
This happens on every resize/reflow — it's the browser's layout engine doing per-frame track-fitting math, not a fixed set of breakpoints, which is why it can respond to any container width (even inside a resizable panel or sidebar), not just the viewport sizes you'd normally hardcode into @media queries.

## Verification (Human Audit)
AI assistants are incredibly helpful, but they frequently inject legacy fallback rules (like floats or unnecessary @media hacks) when designing responsive layouts. You must audit the generated stylesheet to verify it meets these strict requirements:

**No Media Query Layout Rules:** Search your CSS file for the @media keyword. There should be no media queries adjusting columns or resizing the .grid-container.

**The Math of auto-fit vs. auto-fill:** Verify the difference between these keywords. If you only have 2 cards on a wide screen, auto-fit will stretch them to fill the remaining space, whereas auto-fill would leave empty columns. Ensure the AI used auto-fit to keep your columns stretched proportionally.

**Logical Gaps:** Confirm that card separation is controlled entirely by gap on the parent grid, rather than margins on individual cards.

## Linting

Install the development dependencies once:

```sh
npm install
```

Run HTML Validate and Stylelint together:

```sh
npm run lint
```

The individual checks are available as `npm run lint:html` and `npm run lint:css`.
Stylelint can automatically fix supported CSS issues with `npm run lint:css:fix`.
