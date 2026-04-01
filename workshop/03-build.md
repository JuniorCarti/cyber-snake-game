# 03 — Build the Game (Step by Step)

Open **Copilot Chat** (`Ctrl+Shift+I` or click the Copilot icon in the sidebar).

**How this works:** You'll paste each prompt below into Copilot Chat. Copilot will generate code. Copy the **entire** output into the correct file, save, and check your browser before moving on.

> **Important:** Use the prompts **in order**. Each one builds on the last. Save (`Ctrl+S`) after every paste — Live Server will auto-refresh your browser.

> **🆘 Stuck?** If your AI gives you broken code and you can't fix it, the `reference/` folder in this repo has working versions of every file. Copy what you need and keep going.

---

## Step 1 — HTML Structure

> Open `index.html` in VS Code, then paste this prompt into Copilot Chat:

```
Generate a complete index.html file for a game called "CyberDefender".

Requirements:
1. Add a <link> to Google Fonts "Inter" (weights 400, 600, 700).
2. Add a <link rel="stylesheet" href="style.css">.
3. Add <script src="game.js" defer></script> at the end of <body>.

Build this exact structure using these exact element IDs:

TOP NAV BAR (<nav id="top-bar">):
- Left: brand text "CyberDefender" in a <span class="brand">, then "[v1.0.4]" in a <span class="version">, then a <span class="connection-badge">● CONNECTION: STABLE</span>
- Center: <span id="latency">[LAT: 520ms]</span> and <span id="session-timer">[SESSION: 00:00:00]</span>
- Right: <span id="security-posture">SECURITY POSTURE<br><strong>99.98% EFFECTIVE</strong></span>

MAIN LAYOUT (<div id="dashboard"> with three children):

LEFT SIDEBAR (<aside id="left-sidebar">):
- <h3>OPERATOR CONSOLE</h3> and <p>LEVEL 4 CLEARANCE</p>
- <div id="difficulty-section"> with label "DIFFICULTY" and four buttons:
    <button class="diff-btn" data-speed="160">Easy</button>
    <button class="diff-btn active" data-speed="120">Normal</button>
    <button class="diff-btn" data-speed="80">Hard</button>
    <button class="diff-btn" data-speed="50">Expert</button>
- <div id="score-accumulation"> with heading "SCORE ACCUMULATION" and <div id="score-log">No recent activity...</div>
- <div id="mobile-controls"> at the bottom with 4 arrow buttons (↑ ↓ ← →) with classes "ctrl-btn" and data-dir attributes "up", "down", "left", "right"

CENTER (<main id="game-container">):
- <canvas id="gameCanvas" width="480" height="480"></canvas>
- Below the canvas: <div id="canvas-footer"> with <span id="coordinates">[X: 0, Y: 0]</span> and <span id="zone-label">[ZONE: SECTOR-7C]</span>

RIGHT SIDEBAR (<aside id="right-sidebar">):
- <div id="score-section"> with label "CURRENT SCORE" and <div id="score-value">0</div>
- <div id="rank-section"> with "RANK: " text and <span id="rank-label">GUARDIAN PRIME</span> and <span id="rank-percent">0%</span>
- <div id="progress-section"> with a <div id="progress-track"><div id="progress-fill"></div></div>
- <div id="telemetry-section"> with heading "LIVE TELEMETRY" and <div id="telemetry-log"></div>
- <div id="node-distribution"> with heading "NODE DISTRIBUTION" and three stat rows for THREATS, DEFENSE, PACKETS (each with a <span> for the count, IDs: threats-count, defense-count, packets-count)

OVERLAY (after #dashboard):
- <div id="lesson-overlay" class="hidden"></div>

Output ONLY the complete HTML file, nothing else.
```

**Paste** the output into `index.html`. **Save.**

### ✅ Check: Open your browser — you should see the layout elements (unstyled). If the page is completely blank, check the browser console (`F12`) for errors.

---

## Step 2 — CSS Styling

> Open `style.css`, then paste this prompt into Copilot Chat:

```
Create a complete style.css for the CyberDefender game dashboard. Use these exact specifications:

GLOBAL:
- *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
- body: font-family "Inter", sans-serif; background #f8fafb; color #1f2937; min-height 100vh; display flex; flex-direction column

TOP BAR (#top-bar):
- White background, border-bottom 1px solid #e5e7eb, padding 8px 20px
- Display flex, align-items center, justify-content space-between
- .brand: color #00A651, font-weight 700, font-size 16px
- .version: color #9ca3af, font-size 11px, margin-left 4px
- .connection-badge: color #00A651, font-size 12px, margin-left 16px
- #session-timer, #latency: color #6b7280, font-size 11px, font-family monospace
- #security-posture: text-align right, font-size 11px, color #00A651

DASHBOARD (#dashboard):
- display flex, flex 1, overflow hidden

LEFT SIDEBAR (#left-sidebar):
- width 200px, min-width 200px, background white, border-right 1px solid #e5e7eb
- padding 16px, display flex, flex-direction column, gap 20px, overflow-y auto
- h3: font-size 13px, font-weight 700, letter-spacing 0.5px, color #1f2937
- p: font-size 11px, color #6b7280

DIFFICULTY BUTTONS (.diff-btn):
- padding 6px 14px, border-radius 20px, border 1px solid #e5e7eb
- background #f3f4f6, color #374151, font-size 11px, cursor pointer
- .diff-btn.active: background #00A651, color white, border-color #00A651

GAME CONTAINER (#game-container):
- flex 1, display flex, flex-direction column, align-items center, justify-content center
- padding 20px, background #f8fafb

CANVAS (#gameCanvas):
- border 1px solid #e5e7eb, border-radius 8px
- box-shadow 0 1px 3px rgba(0,166,81,0.08)
- background #f0faf0
- max-width 100%

CANVAS FOOTER (#canvas-footer):
- width 480px, display flex, justify-content space-between, margin-top 4px
- font-size 10px, color #9ca3af, font-family monospace

RIGHT SIDEBAR (#right-sidebar):
- width 220px, min-width 220px, background white, border-left 1px solid #e5e7eb
- padding 16px, display flex, flex-direction column, gap 16px, overflow-y auto

SCORE (#score-value):
- font-size 36px, font-weight 700, color #1f2937

RANK:
- #rank-label: font-weight 600
- #rank-percent: color #00A651, font-weight 700

PROGRESS (#progress-track):
- height 4px, background #e5e7eb, border-radius 2px, overflow hidden
- #progress-fill: height 100%, background #00A651, width 0%, transition width 0.3s

TELEMETRY (#telemetry-log):
- max-height 200px, overflow-y auto, font-family monospace, font-size 11px
- .log-entry: padding 6px 0, border-bottom 1px solid #f3f4f6
- .log-time: color #9ca3af, margin-right 8px
- .log-success: color #00A651, font-weight 600
- .log-danger: color #E31937, font-weight 600

SCORE ACCUMULATION (#score-log):
- max-height 150px, overflow-y auto, font-size 11px, color #6b7280
- .score-entry: display flex, justify-content space-between, padding 4px 0, border-bottom 1px solid #f9fafb
- .event-score: font-weight 700, font-size 12px

MOBILE CONTROLS (#mobile-controls):
- margin-top auto, display grid, grid-template-columns repeat(3, 1fr), gap 4px, max-width 120px
- .ctrl-btn: width 32px, height 32px, border-radius 6px, border 1px solid #e5e7eb, background #f9fafb, cursor pointer, display flex, align-items center, justify-content center

LESSON OVERLAY (#lesson-overlay):
- position fixed, inset 0, background rgba(255,255,255,0.6), backdrop-filter blur(8px)
- display flex, align-items center, justify-content center, z-index 1000
- #lesson-overlay.hidden: display none

NODE DISTRIBUTION (#node-distribution):
- .stat-row: display flex, justify-content space-between, font-size 11px, padding 4px 0

RESPONSIVE (max-width 768px):
- #left-sidebar, #right-sidebar: display none
- #mobile-controls: display grid

Output ONLY the CSS code.
```

**Paste** into `style.css`. **Save.**

### ✅ Check: Your browser should now show a clean three-column dashboard with a white top bar, white sidebars, and a light green canvas area in the center. It won't do anything yet — that's next.

---

## Step 3A — Game Setup, State & Drawing

We'll build `game.js` in three smaller steps so it's easier to test. Start with the canvas, state, and drawing.

> Open `game.js`, then paste this prompt into Copilot Chat:

```
Write the first part of game.js for CyberDefender Snake.

CANVAS SETUP (at the very top of the file):
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");
const COLS = 20;
const ROWS = 20;
const CELL = 24;

GAME STATE (create a single object called "state"):
const state = {
    status: "idle",
    snake: [{x:10, y:10}, {x:9, y:10}, {x:8, y:10}],
    direction: {x:1, y:0},
    nextDirection: {x:1, y:0},
    food: null,
    score: 0,
    speed: 120,
    gameInterval: null,
    sessionSeconds: 0,
    sessionTimer: null,
    threat: null,
    defense: null,
    activeCurriculum: null,
    lessonsCompleted: 0,
    totalThreats: 0,
    totalDefenses: 0,
    totalPackets: 0,
    cardTimeLeft: 20,
    cardTimer: null
};

FUNCTIONS TO WRITE:

1. spawnFood(): Generate random {x, y} where x is 0-19 and y is 0-19. Keep generating until the position does NOT overlap any snake segment. Set state.food to the valid position.

2. drawRoundedRect(x, y, w, h, r): Helper that draws a rounded rectangle path using ctx.beginPath(), ctx.moveTo(), ctx.lineTo(), ctx.quadraticCurveTo(), and ctx.closePath(). Do NOT use ctx.roundRect() — it's not supported in older browsers.

3. drawChip(cx, cy, fillColor, strokeColor, symbol, symbolColor, label): Draws a 36x36 rounded chip centered on grid cell (cx, cy). Fill with fillColor, stroke with strokeColor. Draw the symbol text centered inside. Draw the label text 8px below the chip in grey.

4. draw(): Clear the entire canvas. Fill background with #f0faf0. Draw grid lines with strokeStyle "rgba(0,166,81,0.08)".
   Then draw:
   - Each snake segment: filled rounded rect (CELL-2 size, 3px radius, 1px inset). Color #00A651, head #00C261.
   - Food (if state.food exists): drawChip with fill "rgba(255,255,255,0.9)", stroke "rgba(156,163,175,0.5)", symbol "◈" in "#9ca3af", label "DATA_INT".
   - Threat (if state.threat exists): drawChip with fill "rgba(239,68,68,0.1)", stroke "rgba(239,68,68,0.5)", symbol "✉" in "rgba(239,68,68,0.8)", label "THREAT: " + name (truncated to 12 chars).
   - Defense (if state.defense exists): drawChip with fill "rgba(0,166,81,0.1)", stroke "rgba(0,166,81,0.5)", symbol "🛡" in "rgba(0,166,81,0.8)", label "DEFENSE: " + name (truncated to 12 chars).
   - Dashed tether: if BOTH threat and defense exist, draw a dashed line between them with strokeStyle "rgba(0,0,0,0.15)", setLineDash([4,4]). Use ctx.save()/ctx.restore().
   - If status is "idle": draw semi-transparent overlay then "PRESS [SPACE] TO START" centered on canvas, 16px font, color #6b7280.
   - If status is "gameover": draw semi-transparent overlay then "GAME OVER — PRESS [SPACE]" centered, 16px font, color #E31937.
   - Update document.getElementById("coordinates") with head position.

AT THE VERY BOTTOM of the file, add these two lines:
spawnFood();
draw();

Output the COMPLETE file. Do NOT use ctx.roundRect(). Do NOT use TODO or placeholder comments. Every function must be fully implemented.
```

**Paste** the full output into `game.js`. **Save.**

### ✅ Check: You should see the canvas with faint grid lines and "PRESS [SPACE] TO START" in the center. A small white DATA_INT chip should be visible somewhere on the grid. If the canvas is blank, press F12 → Console and fix any red errors.

> **⚠️ Not working?** Compare your output against `reference/game.js` — copy the top section (everything from the start through the `draw()` function and the two initialization lines at the bottom).

---

## Step 3B — Movement, Collision & Game Loop

> Paste this prompt into Copilot Chat. **Make sure your current game.js is open** so Copilot can see it:

```
I have a game.js with canvas setup, state object, spawnFood(), drawRoundedRect(), drawChip(), and draw() functions. I need to add the game loop. Add these functions ABOVE the spawnFood()/draw() lines at the bottom. Do NOT rewrite the existing code — output ONLY the new functions:

1. move(): Runs every game tick.
   - Copy nextDirection into direction: state.direction = { ...state.nextDirection }
   - Calculate newHead = { x: snake[0].x + direction.x, y: snake[0].y + direction.y }
   - WALL CHECK: if newHead.x < 0 or >= 20 or newHead.y < 0 or >= 20, call gameOver() and return
   - SELF CHECK: if any snake segment has same x,y as newHead, call gameOver() and return
   - Add newHead to front: state.snake.unshift(newHead)
   - Set let ate = false
   - FOOD: if newHead.x === state.food.x && newHead.y === state.food.y then: state.score += 1, state.totalPackets++, spawnFood(), ate = true, call addTelemetryLog("DATA PACKET COLLECTED +1", "success"), call addScoreEntry("Data Packet", 1, "#6b7280")
   - DEFENSE: if state.defense exists and newHead matches defense position then: state.score += 500, state.totalDefenses++, ate = true, call addTelemetryLog("NODE SECURED — " + state.defense.name, "success"), call addScoreEntry("Defense: " + state.defense.name, 500, "#00A651"), set state.defense = null, if state.threat exists set state.threat = null, if state.activeCurriculum exists call showCard("defense") and return
   - THREAT: if state.threat exists and newHead matches threat position then: state.score = Math.max(0, state.score - 1000), state.totalThreats++, call addTelemetryLog("THREAT DETECTED — " + state.threat.name, "danger"), call addScoreEntry("Threat: " + state.threat.name, -1000, "#E31937"), set state.threat = null, if state.defense exists set state.defense = null, if state.activeCurriculum exists call showCard("threat") and return
   - If !ate then state.snake.pop() (remove tail for normal movement)
   - If state.threat === null and typeof CURRICULUM !== "undefined" and CURRICULUM.length > 0 and Math.random() < 0.02 then call spawnThreatPair() (if it exists)
   - Call draw()
   - Call updateDashboard()

2. startGame(): Only run if status is "idle" or "gameover".
   - Reset: snake = [{x:10,y:10},{x:9,y:10},{x:8,y:10}], direction = {x:1,y:0}, nextDirection = {x:1,y:0}, score = 0, status = "playing", threat = null, defense = null, activeCurriculum = null, totalThreats = 0, totalDefenses = 0, totalPackets = 0, lessonsCompleted = 0
   - Clear #score-log innerHTML and #telemetry-log innerHTML
   - Call spawnFood()
   - if (state.gameInterval) clearInterval(state.gameInterval)
   - state.gameInterval = setInterval(move, state.speed)
   - if (state.sessionTimer) clearInterval(state.sessionTimer)
   - state.sessionSeconds = 0
   - state.sessionTimer = setInterval that increments sessionSeconds and updates #session-timer with formatted [SESSION: HH:MM:SS]
   - Call addTelemetryLog("SESSION INITIALIZED", "success")
   - Call updateDashboard() then draw()

3. gameOver(): Set status = "gameover", clearInterval(state.gameInterval), clearInterval(state.sessionTimer), call addTelemetryLog("SESSION TERMINATED", "danger"), call updateDashboard(), call draw()

4. updateDashboard(): Set #score-value text to state.score. Set #progress-fill width to min(score/50*100, 100)%. Set #rank-percent to min(score,100)%. Set #threats-count, #defense-count, #packets-count.

5. addTelemetryLog(message, type): Prepend a div.log-entry to #telemetry-log. Inside: <span class="log-time">HH:MM:SS</span> <span class="log-success" or "log-danger">message</span>. Use current time.

6. addScoreEntry(label, points, color): Prepend a div.score-entry to #score-log. Inside: <span class="event-label" with color>label</span><span class="event-score" with color>+/-points</span>. Clear "No recent activity..." text first.

NOTE: showCard() and spawnThreatPair() don't exist yet — the move() function should only call them if they're defined. Use: if (typeof showCard === "function") showCard(type) and if (typeof spawnThreatPair === "function") spawnThreatPair().

Output ONLY the 6 new functions. I will paste them into my existing file.
```

**Paste** the 6 functions into `game.js`, **above** the `spawnFood();` and `draw();` lines at the bottom. **Save.**

### ✅ Check: The canvas still shows "PRESS [SPACE] TO START" but nothing should be broken. If you see console errors, fix them before continuing.

> **⚠️ Not working?** Copy the `move()`, `startGame()`, `gameOver()`, `updateDashboard()`, `addTelemetryLog()`, and `addScoreEntry()` functions from `reference/game.js`.

---

## Step 3C — Controls & Event Listeners

> Paste this prompt into Copilot Chat:

```
I have a game.js with state, draw(), move(), startGame(), gameOver(), updateDashboard(), addTelemetryLog(), and addScoreEntry() functions. I need to add event listeners. Add this code ABOVE the spawnFood()/draw() initialization lines at the bottom:

1. window.addEventListener("keydown", (e) => { ... }):
   - If e.code === "Space": preventDefault(). If state.status is "idle" or "gameover", call startGame(). If state.status is "paused", call dismissCard() if it exists (typeof dismissCard === "function").
   - If state.status !== "playing", return (ignore other keys).
   - Create a keyMap object: { ArrowUp: {x:0,y:-1}, KeyW: {x:0,y:-1}, ArrowDown: {x:0,y:1}, KeyS: {x:0,y:1}, ArrowLeft: {x:-1,y:0}, KeyA: {x:-1,y:0}, ArrowRight: {x:1,y:0}, KeyD: {x:1,y:0} }
   - Look up newDir = keyMap[e.code]. If found: only set state.nextDirection = newDir if it's not the exact reverse of state.direction (check: newDir.x !== -state.direction.x || newDir.y !== -state.direction.y). Call e.preventDefault().

2. Difficulty buttons: document.querySelectorAll(".diff-btn").forEach(btn => btn.addEventListener("click", () => { remove "active" from all .diff-btn, add "active" to clicked btn, state.speed = parseInt(btn.dataset.speed), if state.status === "playing" then clearInterval(state.gameInterval) and state.gameInterval = setInterval(move, state.speed) }))

3. Mobile controls: document.querySelectorAll(".ctrl-btn").forEach(btn => btn.addEventListener("click", () => { if state.status !== "playing" return. Map btn.dataset.dir: up={x:0,y:-1}, down={x:0,y:1}, left={x:-1,y:0}, right={x:1,y:0}. Same reverse-prevention check. Set state.nextDirection. }))

Output ONLY the event listener code. I'll paste it above the initialization lines at the bottom of game.js.
```

**Paste** the event listener code into `game.js`, above the `spawnFood();` / `draw();` lines at the bottom. **Save.**

### ✅ Test — the game should now be fully playable:

Open your browser at `http://127.0.0.1:5500`.

1. **"PRESS [SPACE] TO START"** visible on canvas
2. **Press Space** — snake starts moving right
3. **Arrow keys / WASD** — snake changes direction
4. **Eat DATA_INT chip** — snake grows, score +1, telemetry log updates
5. **Hit a wall** — "GAME OVER" appears, press Space to restart
6. **Click difficulty buttons** — speed changes
7. **Session timer** ticks in the top bar

**If something doesn't work**, open `F12` → Console, copy the error, and ask Copilot to fix it. Or compare with `reference/game.js`.

> **🛑 Don't move to Step 4 until the snake moves and you can eat food.** This is the foundation.

---

## Step 4 — Add Threat & Defense Spawning

Now that the snake works, let's add cybersecurity threat/defense node pairs.

> Paste this prompt into Copilot Chat:

```
I have a working CyberDefender snake game in game.js. I need to add threat/defense pair spawning.

Add these to my existing game.js (do NOT rewrite the whole file — output ONLY the new/modified code):

1. At the top of the file (after the canvas/state setup), add:
   let CURRICULUM = [];
   fetch("lessons.json").then(r => r.json()).then(data => { CURRICULUM = data; }).catch(err => console.warn("Could not load lessons.json:", err));

2. Add function spawnThreatPair(): Pick a random lesson from CURRICULUM. Store it in state.activeCurriculum. Generate a random position for the threat (not on snake, not on food, not on defense). Generate a random position for the defense (not on snake, not on food, not on threat). Set:
   state.threat = { x, y, name: lesson.threat.name }
   state.defense = { x, y, name: lesson.defense.name }

The move() function already has a check that calls spawnThreatPair() randomly if state.threat is null. So just adding this function will enable threat/defense spawning.

Output ONLY the fetch code and the spawnThreatPair function.
```

**Paste** the `CURRICULUM` + `fetch` code near the top of `game.js` (after the state object). **Paste** the `spawnThreatPair` function above the `move()` function. **Save.**

### ✅ Check:

1. Play the game for 10-20 seconds — a red **threat node** and green **defense node** should appear
2. A dashed line should connect them
3. Eating the defense node gives +500 points and a green telemetry log
4. Hitting the threat subtracts 1000 points and logs a red warning
5. Check the console — there should be no fetch errors for `lessons.json`

> **⚠️ Nodes not appearing?** Make sure `lessons.json` is in the same folder as `index.html`. Check the console for fetch errors.
5. Check the console — there should be no fetch errors for `lessons.json`.

---

→ **[04-threats-and-lessons.md](./04-threats-and-lessons.md)**