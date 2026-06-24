# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A vanilla-JavaScript Tetris game (HTML5 Canvas). See `README.md` for gameplay, controls, and a full architecture walkthrough.

## No toolchain — keep it that way

This project is intentionally dependency-free: no `package.json`, no build step, no bundler/transpiler, no tests, no linter. Do not add any of these or run `npm install` / `npm test` — there is nothing to install or build. Plain ES6+ that runs directly in the browser.

## Run / verify

Open `index.html` in a browser, or serve statically (`python3 -m http.server`). There is no automated test — verify changes by playing the game in the browser.

## Cross-file couplings (easy to break)

- **Canvas size**: `COLS`, `ROWS`, and `BLOCK` in `game.js` must match the `<canvas id="board">` `width`/`height` in `index.html` (`width = COLS * BLOCK`, `height = ROWS * BLOCK`). Change one, change the other.
- **Piece colors**: the integers inside `PIECES` in `game.js` are indices into the `COLORS` array. A piece's value must point to its intended color; keep both arrays aligned.

## Architecture

All game logic lives in `game.js`: module-level mutable state (`board`, `current`, `next`, `score`…), a `requestAnimationFrame` `loop`, and DOM/canvas rendering in `draw`. `index.html` is the markup/canvas; `style.css` is presentation only.
