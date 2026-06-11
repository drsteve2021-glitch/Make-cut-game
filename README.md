# Paper Cuts

A two-player, browser-based paper-cutting game. Players take turns slicing a sheet of grid paper along internal lines, and the player who makes the final cut wins.

Built for the KGTS Tech Task (Task 2).

**Live demo:** [your-link-here]

---

## The Game

The sheet is a rectangular grid of unit squares. On each turn, a player cuts one piece along an internal grid line (horizontally or vertically), splitting it into two smaller pieces. Play continues until the entire sheet is reduced to 1×1 squares. The last player to make a valid cut wins (Normal Play Convention).

The setup can also begin with some cuts already made, as the rules allow.

---

## How to Run

No installation or build step required — it's a single self-contained HTML file.

1. Open `index.html` in any modern browser, **or**
2. Visit the live link above.

Two players share the same screen and take turns.

---

## How to Play

- Hover near any internal grid line inside a piece — a red blade guide appears — and click to cut all the way across that piece.
- You can only cut internal lines, never the outer border.
- The status bar shows whose turn it is, how many cuts have been made, and a progress bar toward fully reducing the sheet.
- The game ends when every piece is a 1×1 square, and the player who made the final cut is declared the winner.
- Use the controls to change the grid size or add random pre-cuts before starting.

---

## How It Works

### Game-state management

The entire board is represented as a **list of rectangular regions**. Each region records the columns and rows it covers: `{ c0, r0, c1, r1 }`. The starting sheet is a single region; a region is fully reduced when both its width and height equal 1.

A move calls `splitRegion()`, which removes one region from the list and replaces it with the two pieces created by the cut. Because the board is just a list of rectangles, the game logic stays simple and there is no need to track individual cut lines.

### Win/loss detection

After every cut, `allUnits()` checks whether every region is a 1×1 square. The moment that is true, the player who just moved is the winner. Since every offered cut splits exactly one region into two, there are no invalid moves to handle — the only end condition that needs checking is whether the sheet is fully reduced.

---

## A Note on Strategy

This game has an interesting mathematical property: **every cut increases the number of pieces by exactly one.** Starting from one sheet and ending with `cols × rows` unit squares, the game always lasts exactly `(cols × rows − starting pieces)` cuts, no matter how either player plays.

This means the winner is determined purely by the **parity** of that number, not by skill. If the total number of cuts is odd, Player 1 makes the last cut; if even, Player 2 does. The game is a clean demonstration of a combinatorial game whose outcome is fixed by its structure — which is also why it is built as a two-player game rather than a game against an AI.

---

## Tech Stack

- **HTML / CSS / JavaScript** — no frameworks, no dependencies.
- Layout rendered with absolutely-positioned pieces over a CSS-grid "cutting mat".

---

## Author

Steve B — First-year B.Tech, IIT Kharagpur.
