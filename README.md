# Randomly Better Games

A two-player twist on classic grid games where you can't always choose your symbol. On each turn, a wheel spins and decides what you'll be placing — sometimes you'll find yourself playing for your opponent. The winner is whoever lines up the required number of their symbol in a row, regardless of which player physically placed them.

Currently supports **Tic-Tac-Toe** and **Connect 4**, switchable from the start screen.

## How to play

Open `index.html` in any modern browser. There are no dependencies and no build step.

Two players share one device. At the start of each game, the wheel announces who goes first (this alternates between games). On your turn:

1. Tap **Spin!** to spin the wheel.
2. Wait for the wheel to stop — it'll land on either an X or an O.
3. Tap any open cell to place that symbol.

The next player takes over and the process repeats. Three in a row of either symbol ends the game.

## Modes

Before each game, two independent toggles on the start screen control how the wheel behaves:

### Random vs. Balanced

- **Random** — each spin is an independent 50/50 coin flip. Streaks happen, and that's part of the chaos.
- **Balanced** — the wheel starts with 12 wedges (6 X, 6 O). The landed wedge is removed after each spin, so the odds shift to dampen long streaks without making any single spin predetermined.

### Fair vs. Biased

- **Fair** — both symbols have equal arc lengths.
- **Biased** — a slider lets you tilt the wheel anywhere from 10/90 to 90/10. Recommended only when both players agree on the bias.

The two toggles combine. Balanced + Biased, for example, favors the chosen symbol early but the bias naturally relaxes as the favored symbol's wedges deplete faster.

## Deployment

This is a single static HTML file intended for hosting on GitHub Pages (or any static host). No backend, no storage, no analytics.
