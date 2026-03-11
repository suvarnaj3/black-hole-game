# Garv's Tasks: State, Logic & AI

**Your file:** `src/utils.js` + wiring `src/App.jsx`
**Your branch:** `feature-core-engine`

---

### Task 1: Commit the shared state shape *(do this Day 1, before anyone branches)*

Add the agreed state shape as a comment block at the top of `App.jsx` and push it to `main` so Suvarna and Ketki can branch off it immediately. See `setup.md` Step 5 for the exact shape.

---

### Task 2: `utils.js` — Adjacency Map *(Mar 13)*

The most critical function in the project. Everything else depends on it.

```js
// For a given circle index, return the indices of all its neighbors
export function getNeighbors(index, totalCircles) { ... }
// totalCircles: 21 (2-player) or 28 (3-player)
// returns: number[]
```

Map out the triangle on paper first. Row 1 has index 0, row 2 has indices 1–2, row 3 has 3–5, etc. Each circle touches up to 6 neighbors. Hardcoding the map as a lookup object is totally fine and more reliable than calculating it dynamically.

---

### Task 3: `utils.js` — Scoring *(Mar 13)*

```js
export function calculateScores(board, totalCircles) { ... }
// 1. Find the black hole: the one remaining null in the board
// 2. Call getNeighbors(blackHoleIndex) to get surrounding indices
// 3. Sum the values of those circles grouped by player
// 4. Lowest total wins
// returns: { scores: { 1: n, 2: n }, winner: 1 | 2 }
```

---

### Task 4: `utils.js` — AI Opponent *(Mar 14)*

```js
export function getAIMove(board, totalCircles, valueToPlace) { ... }
// returns: index (which circle the AI picks)
```

- **Phase 1 (must ship):** Random move — pick any empty circle. Gets the game playable immediately.
- **Phase 2 (if time allows):** Heuristic — high numbers away from center, low numbers near likely black hole positions (circles with fewer neighbors).

---

### Task 5: Wire `App.jsx` *(Mar 15)*

`App.jsx` owns all state with `useState`. Your job is to wire the logic to the UI components:

```jsx
// App.jsx owns:
const [board, setBoard] = useState(Array(21).fill(null));
const [currentPlayer, setCurrentPlayer] = useState(1);
const [selectedNumber, setSelectedNumber] = useState(null);
const [phase, setPhase] = useState('menu');
const [scores, setScores] = useState({ 1: 0, 2: 0, 3: 0 });

// placeNumber runs when a player taps a board circle
function placeNumber(index) {
  if (!selectedNumber || board[index] !== null) return;
  const newBoard = [...board];
  newBoard[index] = { player: currentPlayer, value: selectedNumber };
  setBoard(newBoard);
  // check if board full → calculateScores → setPhase('gameover')
  // else → advance turn (Ketki's nextTurn logic)
  // if pve and it's now AI turn → call getAIMove → place → advance turn
}
```

Pass `board`, `placeNumber`, `selectedNumber`, `setSelectedNumber` down to `<Board>`.
Pass `scores`, `winner` down to `<GameOver>`.
Pass `setPhase`, `setGameMode` down to `<Menu>`.