# CLAUDE.md

Notes for future Claude Code sessions on this project.

## What this is

A single-file static HTML game (`index.html`) with no dependencies and no build step. Open the file directly in a browser; nothing to serve.

## Core mechanic

Tic-tac-toe where the symbol you place each turn is determined by a wheel spin, not by which player you are. Player X might be forced to place an O — possibly into a position that wins the game for Player O. The winner is whoever has three of their symbol in a row, regardless of who placed the marks.

## Architecture

- All HTML, CSS, and JS live inline in `index.html`. No build pipeline.
- Game state is a handful of module-level `let` variables at the top of the script block.
- Wedges are objects: `{ s: 'X' | 'O', w: number }`. The weight `w` determines both the wedge's arc length on the wheel and its probability of being landed on — they're the same thing.
- `pickWedgeIndex` is a single weighted random picker that serves all four mode combinations. Random vs. Balanced differs only in whether the chosen wedge is spliced out after the spin.

## Design decisions worth knowing

- **Starting player alternates between games.** Tracked in `firstPlayer`; toggled in `showStartOverlay`. The start overlay is shown every game (including the first) to make this explicit.
- **Balanced uses 12 wedges (6+6), not 10.** With 10, one symbol could be exhausted before a 9-spin draw board fills, forcing the remaining spins. 12 leaves enough headroom while still cutting streak probability ~2× vs. pure random.
- **Bias slider is constrained to 10..90.** Avoids zero-weight wedges and the edge cases that follow.
- **Slider value runs opposite to X-share.** Low slider value = X-favored = X on the left. Computed as `xShare = (100 - biasValue) / 100`. This was a UX choice (X first, like in the player names) rather than a math convenience.
- **Wheel rotation resets to 0 (with `transition: none`) before each rebuild** to avoid CSS interpolating between layouts that no longer correspond.
- **Spin result is decided before the animation starts.** The wheel is choreographed to land on the chosen wedge; the wheel has no physical fairness. This is how all "spin the wheel" web animations work.
- **Wedge letters drop off the wheel when arc < 14°.** At extreme bias, the tiny wedges would otherwise show unreadable single characters.

## Deliberate non-features

- No `localStorage` — settings reset on refresh. Acceptable for a kitchen-table game.
- No sound effects. (Considered, not built.)
- No online multiplayer; this is purely local pass-the-device.
- No accessibility audit yet. ARIA labels and keyboard support haven't been added.

## Repo / deployment

- Local folder name is `randomized-tic-tac-toe`; intended GitHub repo name is `enhanced-tic-tac-toe`. The mismatch is intentional and was discussed — local folder kept as-is to avoid mid-session rename hassles.
- Intended deployment: GitHub Pages on a custom subdomain managed via Namecheap DNS. Not yet pushed to a remote.

## To-do

Pre-deployment polish, none blocking:

- [ ] Push to GitHub as `enhanced-tic-tac-toe` and enable GitHub Pages.
- [ ] Configure a custom Namecheap subdomain (CNAME file + DNS record).
- [ ] Add a favicon (a single-emoji data-URI is plenty).
- [ ] Add meta description and Open Graph tags so shared links look intentional.
- [ ] Accessibility pass: ARIA labels on the wheel and cells, keyboard support for cell selection.
- [ ] (Optional) Rename the local folder to match the repo name.

## Working style

The user prefers to discuss design choices before implementation, especially for UX questions. When they ask "what do you think?" or "what should we consider?", lead with 2–3 sentences of recommendation + tradeoff rather than jumping to code.
