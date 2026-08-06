# The Verification (Human Audit)
AI assistants are incredibly helpful, but they frequently inject legacy fallback rules (like floats or unnecessary @media hacks) when designing responsive layouts. You must audit the generated stylesheet to verify it meets these strict requirements:

No Media Query Layout Rules: Search your CSS file for the @media keyword. There should be no media queries adjusting columns or resizing the .grid-container.

The Math of auto-fit vs. auto-fill: Verify the difference between these keywords. If you only have 2 cards on a wide screen, auto-fit will stretch them to fill the remaining space, whereas auto-fill would leave empty columns. Ensure the AI used auto-fit to keep your columns stretched proportionally.

Logical Gaps: Confirm that card separation is controlled entirely by gap on the parent grid, rather than margins on individual cards.