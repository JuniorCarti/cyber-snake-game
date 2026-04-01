# 04 — Lesson Cards

Your snake game already spawns threat/defense pairs from Step 3. This step adds the **lesson card overlay** — when the snake collects a defense node or hits a threat, the game pauses and shows an educational card about that cybersecurity topic.

> **🆘 Stuck at any point?** The `reference/` folder in this repo has working versions of every file.

---

## Step 1 — Confirm Everything Works So Far

Before adding lesson cards, verify:

- [ ] Snake moves and eats food (score increases)
- [ ] Threat (red) and defense (green) nodes spawn as pairs
- [ ] Eating defense gives +500, hitting threat gives -1000
- [ ] No red errors in the browser console (`F12` → Console)
- [ ] `lessons.json` is in the same folder as `index.html`

If any of these fail, go back to [03-build.md](./03-build.md) and fix them first.

---

## Step 2 — Add Lesson Card HTML

> Paste this prompt into Copilot Chat:

```
Add the lesson card HTML inside the existing <div id="lesson-overlay" class="hidden"></div> in my index.html.

Replace that empty div with this structure:

<div id="lesson-overlay" class="hidden">
  <div id="lesson-card">
    <div id="card-timer-bar"></div>
    <div id="card-header">
      <div id="card-header-left">
        <span id="card-category">CATEGORY</span>
        <h2 id="card-title">Title</h2>
      </div>
      <div id="card-header-right">
        <span class="resume-label">RESUME IN</span>
        <span id="card-countdown">20s</span>
      </div>
    </div>
    <div id="card-body">
      <div id="card-threat" class="card-section">
        <div class="section-icon threat-icon">⚠</div>
        <div>
          <span class="section-label threat-label">THREAT: NAME</span>
          <p class="section-desc" id="threat-desc">Description</p>
        </div>
      </div>
      <div id="card-defense" class="card-section">
        <div class="section-icon defense-icon">🛡</div>
        <div>
          <span class="section-label defense-label">DEFENSE: NAME</span>
          <p class="section-desc" id="defense-desc">Description</p>
        </div>
      </div>
    </div>
    <div id="card-buttons">
      <button id="extend-btn" class="card-btn">+10S</button>
      <button id="continue-btn" class="card-btn primary">CONTINUE (+500 PTS) [SPACE]</button>
    </div>
  </div>
</div>

Output ONLY the modified lesson-overlay section. I will paste it to replace the existing empty div.
```

**Replace** the `<div id="lesson-overlay" class="hidden"></div>` in your `index.html` with the output. **Save.**

---

## Step 3 — Style the Lesson Card

> Paste this prompt into Copilot Chat:

```
Add CSS to my existing style.css for the CyberDefender lesson card overlay. Append these styles (do NOT replace existing CSS):

#lesson-card:
- background white, border-radius 12px, max-width 480px, width 90%, padding 0
- box-shadow 0 8px 32px rgba(0,0,0,0.12), overflow hidden, position relative

#card-timer-bar:
- height 3px, background #00A651, width 100%, transition width 0.1s linear
- position at the top of the card

#card-header:
- display flex, justify-content space-between, align-items flex-start, padding 20px 24px 12px

#card-category:
- font-size 10px, letter-spacing 1px, color #9ca3af, text-transform uppercase, font-weight 600

#card-title:
- font-size 20px, font-weight 700, color #1f2937, margin-top 4px

#card-countdown:
- font-size 28px, font-weight 700, color #1f2937

.resume-label:
- font-size 10px, color #9ca3af, letter-spacing 0.5px

#card-body:
- padding 0 24px 16px

.card-section:
- display flex, gap 12px, padding 12px 0, align-items flex-start

.section-icon:
- width 32px, height 32px, border-radius 6px, display flex, align-items center, justify-content center, font-size 16px, flex-shrink 0

.threat-icon: background rgba(239,68,68,0.1), color #ef4444
.defense-icon: background rgba(0,166,81,0.1), color #00A651

.section-label:
- font-size 11px, font-weight 700, letter-spacing 0.5px, text-transform uppercase

.threat-label: color #ef4444
.defense-label: color #00A651

.section-desc:
- font-size 13px, color #4b5563, line-height 1.5, margin-top 4px

#threat-desc: border-left 2px solid #ef4444, padding-left 10px
#defense-desc: border-left 2px solid #00A651; padding-left 10px

#card-buttons:
- display flex, gap 8px, padding 16px 24px, border-top 1px solid #f3f4f6

.card-btn:
- flex 1, padding 10px, border-radius 20px, border none, cursor pointer, font-size 13px, font-weight 600

#extend-btn:
- background #f3f4f6, color #374151

#continue-btn:
- color white, font-size 14px

#continue-btn.defense-btn: background #00A651
#continue-btn.threat-btn: background #E31937

Output ONLY the new CSS to append.
```

**Append** the output to the bottom of your `style.css`. **Save.**

---

## Step 4 — Lesson Card Logic

> Paste this prompt into Copilot Chat:

```
Add lesson card functions to my existing game.js. Append these functions (do NOT rewrite the whole file):

1. showCard(type):
   - type is "defense" or "threat"
   - Get the lesson data from state.activeCurriculum
   - Set #card-category textContent to lesson.category
   - Set #card-title textContent to lesson[type].name
   - Set .threat-label textContent to "THREAT: " + lesson.threat.name
   - Set #threat-desc textContent to lesson.threat.description
   - Set .defense-label textContent to "DEFENSE: " + lesson.defense.name
   - Set #defense-desc textContent to lesson.defense.description
   - Set #continue-btn class: remove both "defense-btn" and "threat-btn", add type + "-btn"
   - Set #continue-btn textContent: if type is "defense", "CONTINUE (+500 PTS) [SPACE]"; if "threat", "CONTINUE (-1000 PTS) [SPACE]"
   - Remove "hidden" class from #lesson-overlay
   - Set state.status = "paused"
   - clearInterval(state.gameInterval)
   - Call startCardTimer()

2. startCardTimer():
   - Set state.cardTimeLeft = 20
   - Get #card-timer-bar and #card-countdown elements
   - Set state.cardTimer = setInterval(() => {
       state.cardTimeLeft -= 0.1
       Update #card-timer-bar width to (state.cardTimeLeft / 20 * 100) + "%"
       Update #card-countdown textContent to Math.ceil(state.cardTimeLeft) + "s"
       If state.cardTimeLeft <= 0, call dismissCard()
     }, 100)

3. extendTimer():
   - state.cardTimeLeft = Math.min(state.cardTimeLeft + 10, 30)
   - Update #card-timer-bar and #card-countdown immediately

4. dismissCard():
   - clearInterval(state.cardTimer)
   - Add "hidden" class to #lesson-overlay
   - Set state.status = "playing"
   - state.gameInterval = setInterval(move, state.speed)

5. Modify the existing move() function:
   - In the DEFENSE CHECK: after the existing score/log code, add: if (state.activeCurriculum) { showCard("defense"); return; }
   - In the THREAT CHECK: after the existing score/log code, add: if (state.activeCurriculum) { showCard("threat"); return; }

6. Add event listeners:
   - #extend-btn click: call extendTimer()
   - #continue-btn click: call dismissCard()
   - In the existing keydown listener, add: if key is Space and status is "paused", call dismissCard() and preventDefault

Also add cardTimeLeft: 20 and cardTimer: null to the state object.

Output the COMPLETE new functions AND the modified sections of move() and the keydown listener. Show enough context that I know exactly where to paste each piece.
```

**Add** the new functions to `game.js`. **Modify** the `move()` function and keydown listener as instructed. **Save.**

---

## ✅ Final Check

Play the game and verify:

- [ ] Threat + defense node pair appears during gameplay
- [ ] Dashed line connects them
- [ ] Collecting the **defense node** pauses the game and shows a lesson card with green "CONTINUE" button
- [ ] Hitting the **threat node** pauses the game and shows a card with red "CONTINUE" button
- [ ] Card shows the correct threat name, defense name, and descriptions
- [ ] Timer bar depletes from left to right, countdown shows
- [ ] **+10S** button adds time
- [ ] **CONTINUE** button (or Space) closes the card and resumes the game
- [ ] Game resumes cleanly — snake keeps moving

**If the card doesn't appear:** Open browser console (`F12`), check for errors, and paste the error into Copilot Chat with your code:

```
The lesson card is not appearing when I eat a defense node.
Here is my move() function and showCard() function:
[paste both functions]
Fix the issue.
```

---

**You've built CyberDefender! 🛡️**