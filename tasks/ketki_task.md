# Ketki's Tasks: Menu, Turn Logic & Game Over

**Your files:** `src/Menu.jsx`, `src/GameOver.jsx`, turn logic in `src/App.jsx`
**Your branch:** `feature-game-flow`

---

### Task 1: `Menu.jsx` *(Mar 13)*

The start screen. Full screen, phone-friendly, no tiny buttons.

**Props it receives:** `onStart(gameMode)` — call this when the player confirms their choice.

```jsx
// Three big tappable cards or buttons:
// "1 vs AI"         → onStart('pve')
// "1 vs 1"          → onStart('pvp')
// "3 Players"       → onStart('3p')
```

You can build and test this entirely on its own — no dependency on Garv or Suvarna.

---

### Task 2: Turn Logic in `App.jsx` *(Mar 13–14)*

Write a `nextTurn()` function that Garv calls from `placeNumber()` after a valid move:

```js
function nextTurn() {
  // 2-player: 1 → 2 → 1
  // 3-player: 1 → 2 → 3 → 1
  // Also advance that player's "next number to place"
  // 2-player: values 1–10 per player
  // 3-player: values 1–9 per player
}
```

Also maintain per-player next number state so the UI always shows the right value:

```js
const [nextValues, setNextValues] = useState({ 1: 1, 2: 1, 3: 1 });
// After player 1 places their 3, nextValues[1] becomes 4, etc.
```

---

### Task 3: `GameOver.jsx` *(Mar 14–15)*

A full-screen modal that appears when `phase === 'gameover'`.

**Props it receives:** `scores` `{ 1: n, 2: n }`, `winner` `1 | 2 | 3`, `onPlayAgain()`

- Show each player's score clearly
- Announce the winner — add a note that lowest score wins since it's the opposite of most games
- One big "Play Again" button that resets everything to initial state without refreshing the page
- *Bonus:* Running win tally this session using `localStorage`

---

### Task 4: Integration *(Mar 16)*

- Confirm `Menu.jsx` correctly sets `gameMode` and flips `phase` to `'playing'`
- Confirm turn display shows the right player and right number at all times
- Confirm `GameOver.jsx` renders on `phase === 'gameover'` and Play Again fully resets all state
- Test all three game modes end-to-end