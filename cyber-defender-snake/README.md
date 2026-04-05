# CyberDefender Snake

A cybersecurity educational game built with vanilla JavaScript, HTML5 Canvas, and CSS.

## How to Play

1. **Start**: Press SPACE to begin
2. **Move**: Use arrow keys or WASD to control the snake
3. **Objective**: Collect data packets (white diamonds) to grow and score points
4. **Cybersecurity**: Red threat nodes and green defense nodes appear as pairs
   - Collect defense nodes (+500 points) to learn cybersecurity concepts
   - Avoid threat nodes (-1000 points) or face risk briefings
5. **Difficulty**: Choose from Easy (160ms), Normal (120ms), Hard (80ms), or Expert (50ms)

## Features

- **Educational**: Learn cybersecurity through interactive lessons
- **Responsive**: Works on desktop and mobile devices
- **Real-time Dashboard**: Score, telemetry logs, session timer, and statistics
- **Lesson Cards**: Pause for educational content with countdown timers
- **Mobile Controls**: Touch-friendly controls for mobile play

## Technical Details

- **Language**: Vanilla JavaScript (ES6+)
- **Graphics**: HTML5 Canvas with 20x20 grid system
- **Styling**: CSS with Inter font from Google Fonts
- **Data**: Lessons loaded from JSON curriculum file
- **Controls**: Keyboard (arrows/WASD) and touch controls

## Files

- `index.html` - Main HTML structure and dashboard layout
- `style.css` - Complete styling for cyber theme and responsive design
- `game.js` - Full game logic, rendering, and event handling
- `lessons.json` - Cybersecurity curriculum data

## Running Locally

```bash
# Start a local server (Python 3)
python -m http.server 8000

# Or with Node.js
npx serve .

# Then open http://localhost:8000 in your browser
```

## Browser Compatibility

Works in all modern browsers that support:
- HTML5 Canvas
- ES6+ JavaScript features
- CSS Grid and Flexbox
- fetch() API

## Educational Content

The game includes lessons on:
- **Classic Cyber Risks**: Phishing, Ransomware, SQL Injection, DDoS, etc.
- **Emerging AI Risks**: Prompt Injection, Deepfake Fraud, Data Poisoning, etc.
- **Defensive Strategies**: MFA, Backups, Firewalls, Encryption, etc.

Each lesson card shows the threat description and corresponding defense strategy.