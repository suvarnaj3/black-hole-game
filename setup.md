# Local Setup Guide — The Black Hole Game

## Prerequisites
Make sure you have [Node.js](https://nodejs.org/) installed.

---

## Step 1: Fork the Repository

Go to [github.com/garv767/black-hole-game](https://github.com/garv767/black-hole-game) and click **Fork** (top right). This creates your own copy of the repo under your GitHub account.

## Step 2: Clone Your Fork
```bash
git clone https://github.com/YOUR_USERNAME/black-hole-game.git
```

Then add the original repo as `upstream` so you can pull in changes from the main project:
```bash
cd black-hole-game
git remote add upstream https://github.com/garv767/black-hole-game.git
```

## Step 3: Install Dependencies
```bash
npm install
```

## Step 4: Run the Development Server
```bash
npm run dev
```

> 📱 **Always test on your phone, not just your laptop.** Vite also prints a `http://192.168.x.x:5173` network URL in the terminal — open that on your phone while on the same Wi-Fi. This is the primary demo device.

---

## Step 5: Project Structure

Keep it simple. Everything lives in 5 files:

```
src/
├── App.jsx        ← all game state (useState here, props drilled down)
├── Board.jsx      ← Suvarna
├── Menu.jsx       ← Ketki
├── GameOver.jsx   ← Ketki
└── utils.js       ← Garv (adjacency + scoring + AI, one file)
```

No custom hooks. No separate utils folder. `App.jsx` owns all state and passes it down as props.

---

## Step 6: Shared State Shape

Agree on this before branching. Garv commits it as a comment at the top of `App.jsx`:

```js
// SHARED STATE SHAPE — read this before touching props
// board: Array(21 or 28).fill(null)
//   each cell: null | { player: 1|2|3, value: 1-10 }
// currentPlayer: 1 | 2 | 3
// gameMode: 'pvp' | 'pve' | '3p'
// selectedNumber: number | null   ← which chip the player tapped in the tray
// phase: 'menu' | 'playing' | 'gameover'
// scores: { 1: 0, 2: 0, 3: 0 }
```

## Step 7: Number Picker UI Convention

Players pick their number from a **sticky chip tray at the bottom of the screen** — no keyboard, no modal. Suvarna builds this as part of the Board component.

```
┌─────────────────────────┐
│      game board         │
├─────────────────────────┤
│  Player 1 — pick a num  │
│  [1][2][3][5][7][8][10] │  ← used numbers disappear
└─────────────────────────┘
```

- Minimum tap target: 48 × 48px
- Used numbers are removed from the tray entirely (not greyed out)
- Selected number highlights before the player taps the board circle

---

## Step 8: Git Workflow

Never work on `main`. Each person works on their own branch inside their fork:

```bash
# Create your branch
git checkout -b feature-your-task-name

# ...make your changes...

git add .
git commit -m "feat: description of what you built"
git push origin feature-your-task-name
```

Then go to **your fork** on GitHub and click **"Compare & pull request"** to open a PR against `garv767/black-hole-game` (the original). Garv reviews and merges.

**If the main repo has new changes since you forked**, sync before pushing:
```bash
git fetch upstream
git merge upstream/main
```

**Branches:**
- `feature-core-engine` — Garv
- `feature-game-flow` — Ketki
- `feature-ui-board` — Suvarna

---

## Timeline

| | Mar 13–14 | Mar 15 | Mar 16 | Mar 17 | Mar 18 |
|---|---|---|---|---|---|
| **Garv** | utils.js (adjacency, scoring, AI) | State wiring in App.jsx | Integration | Testing | 🎤 Present |
| **Ketki** | Menu.jsx + turn logic | GameOver.jsx | Integration | Testing | 🎤 Present |
| **Suvarna** | Board.jsx + chip tray | Animations + mobile polish | Integration | Testing | 🎤 Present |