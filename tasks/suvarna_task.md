# Suvarna's Tasks: Board, Chip Tray & Mobile UI

**Your file:** `src/Board.jsx`
**Your branch:** `feature-ui-board`

> 📱 **Mobile-first means you design for 390px width first.** Desktop is a bonus. Test everything on your phone throughout development — not just at the end.

---

### Task 1: Pyramid Layout *(Mar 13)*

Build the triangle board. The board should take up the majority of the screen.

**Props it receives:**
- `board` — `Array(21 or 28).fill(null)`, each cell is `null | { player: 1|2|3, value: number }`
- `onCircleClick(index)` — call this when a circle is tapped
- `selectedNumber` — the number currently selected in the chip tray (show a preview on hover/tap)
- `totalCircles` — 21 or 28

```
Row 1:  ○                    ← index 0
Row 2:  ○ ○                  ← index 1–2
Row 3:  ○ ○ ○                ← index 3–5
Row 4:  ○ ○ ○ ○              ← index 6–9
Row 5:  ○ ○ ○ ○ ○            ← index 10–14
Row 6:  ○ ○ ○ ○ ○ ○          ← index 15–20
```

Color per player: **Player 1 — Blue**, **Player 2 — Red**, **Player 3 — Green**. Empty circles are neutral.

Start with mock data so you don't need to wait for Garv:
```js
const mockBoard = Array(21).fill(null);
mockBoard[3] = { player: 1, value: 5 };
mockBoard[7] = { player: 2, value: 3 };
```

---

### Task 2: Sticky Number Chip Tray *(Mar 13–14)*

This replaces the keyboard entirely. It lives at the bottom of the screen, always visible during play.

**Props it receives:**
- `currentPlayer` — 1, 2, or 3
- `usedNumbers` — `{ 1: Set, 2: Set, 3: Set }` — numbers already placed per player
- `selectedNumber` — currently highlighted chip
- `onSelectNumber(n)` — call when a chip is tapped
- `gameMode` — to determine max number (10 for 2-player, 9 for 3-player)

```
┌──────────────────────────┐
│  Player 1 — tap a number │
│  [1][2][3][5][7][8][10]  │  ← used numbers disappear
└──────────────────────────┘
```

- Minimum chip size: **48 × 48px**
- Selected chip: strong highlight (filled background in player's colour)
- Used numbers: remove from tray entirely
- The tray should be **sticky to the bottom** — `position: fixed; bottom: 0`
- Add enough bottom padding to the board so the tray never overlaps circles

**Interaction flow:**
1. Player taps a chip → it highlights, `selectedNumber` is set
2. Player taps an empty board circle → number is placed, chip disappears from tray
3. Turn advances — tray updates to next player's remaining numbers

---

### Task 3: Mobile Layout *(Mar 14)*

- Board should scale to fit the screen without scrolling — use `vmin` units for circle sizes
- The whole game must be playable in portrait mode with one hand
- No horizontal scrolling at any screen size
- Test at 390px (iPhone 14), 375px (iPhone SE), and 414px (older Android)

Suggested layout:
```
┌──────────────────┐
│  Turn indicator  │  ← small text, not a full header
│                  │
│   [  board  ]    │  ← takes most of the vertical space
│                  │
│  [chip tray]     │  ← fixed bottom
└──────────────────┘
```

---

### Task 4: Black Hole Reveal *(Mar 15)*

When `phase === 'gameover'`:

**Props it receives:** `blackHoleIndex`, `scoringIndices` (array of adjacent circle indices)

- The black hole circle: dramatic CSS animation — pulse, dark colour, or a "collapse" effect
- Adjacent circles: highlight them in a distinct colour to show which ones were scored
- This is the visual centrepiece of the presentation — spend time on it

---

### Task 5: Integration *(Mar 16)*

- Swap mock board data for real `board` state from `App.jsx`
- Confirm `onCircleClick` triggers `placeNumber` correctly
- Confirm chip tray removes numbers as they are placed
- Confirm black hole reveal fires correctly when `phase === 'gameover'`
- Final pass on spacing, font sizes, and touch targets on a real phone