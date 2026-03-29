# 03 — Build the Arena & Snake

Open **Copilot Chat** (`Ctrl+Shift+I`) with `game.js` active.

Use the prompts below one at a time. After each, paste the output into the correct file and save.

---

## Prompt A — HTML Shell

Paste into Copilot Chat with `index.html` open:

> *"Create a professional three-column dashboard layout for a cybersecurity game called CyberDefender. Include a top navigation bar showing 'CyberDefender [v1.0.4]' on the left, a green '● CONNECTION: STABLE' badge, and session telemetry on the right. The layout should have a 200px left sidebar for the 'OPERATOR CONSOLE' with level clearance headers and difficulty selectors, a center game area with a 480x480 canvas, and a 220px right sidebar for score tracking, a progress bar, and a live telemetry event log. Provide an empty div with id='lessonOverlay' for modal cards. Use the Inter font from Google Fonts and maintain a clean, light-grey SaaS aesthetic throughout."*

Paste the output into `index.html`. Save.

---

## Prompt B — CSS Styling

Paste into Copilot Chat with `style.css` open:

> *"Write CSS for a clean, light-themed cybersecurity dashboard using a white and light grey (#f8fafb) palette with #e5e7eb borders. Style the sidebars with subtle shadows and 1px borders. The difficulty selectors should be pill-shaped radio buttons where the active state has a green (#00A651) background and white text, while others use a light grey background. For the game canvas, add a 1px solid border and a very subtle green shadow. Style the telemetry log using a small monospace font, with .log-success in green (#00A651) and .log-danger in red (#E31937). Ensure there are no scanlines or dark terminal effects, focusing instead on a premium, modern dashboard feel."*

Paste into `style.css`. Save. Your browser should show a dark themed page.

---

## Prompt C — Snake Game Logic

Paste into Copilot Chat with `game.js` open:

> *"Build a complete vanilla JS snake game on a 480x480 canvas element with id='gameCanvas'. Use a 20x20 grid (CELL = 24px). The snake segments must be rendered as solid green (#00A651) rounded squares using the roundRect method with a 3px radius. Food items should be drawn as small 36x36 rounded square chips with a light grey background and the label 'DATA_INT' centered below them. Implement a basic game state with snake array, direction, food coords, score, and status. Create a move() function that handles growth, wall-death, self-collision, and score updates. Update the '#score' element and add system telemetry log entries for each item collected. Start the game loop on the Space key and display 'PRESS SPACE TO START' on the canvas when idle."*

Paste into `game.js`. Save.

---

## ✅ Test Before Moving On

- [ ] Page loads in browser
- [ ] Space bar starts the game
- [ ] Snake moves and responds to arrow keys
- [ ] Snake grows when it eats the gold dot
- [ ] Score updates on screen
- [ ] Wall or self-collision ends the game

→ **[04-threats-and-lessons.md](./04-threats-and-lessons.md)**
