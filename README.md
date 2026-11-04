# Chess Post-Mortem

A free chess game review site. Paste a chess.com or Lichess game link (or a PGN) and get a full Stockfish review: move labels from Brilliant to Blunder, accuracy for both players, key moments, best lines and "retry this move".

Everything runs in the visitor's browser. There is no server and no game data leaves the device, apart from fetching the game from chess.com or Lichess.

## Features

- Move labels (Brilliant, Great, Best, Excellent, Good, Book, Inaccuracy, Mistake, Miss, Blunder) with coach notes
- Eval bar with the gain or loss of every move, plus an eval graph you can scrub
- Accuracy per player and per game phase, key moments, best lines, "retry this move"
- Autoplay, four board colour themes, and shareable review links (`#g=…` in the address)

## Put it online with GitHub Pages

1. Create a new public repository on GitHub, for example `chess-review`.
2. Upload every file in this folder to the repository, keeping the `engine` and `data` folders and the `.nojekyll` file.
3. In the repository, open **Settings → Pages**. Under **Build and deployment**, set **Source** to **Deploy from a branch**, pick the `main` branch and the `/ (root)` folder, and save.
4. After a minute or two the site is live at `https://<your-username>.github.io/chess-review/`. Share that link.

## How games are loaded

- **Lichess links** use Lichess's public game export API.
- **chess.com links** use chess.com's public Published-Data API. It lists games by player and month, so the site needs one player's username. It reads it from chess.com's share text ("a vs b - link") or from the username box, then searches that player's last 12 months.
- **PGN** can always be pasted directly or opened from a `.pgn` file.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app (layout, styles and code) |
| `engine/stockfish-19-lite-single.js`, `.wasm` | Stockfish 19 engine (GPLv3), from the `stockfish` npm package |
| `engine/stockfish-19-asm.js` | Slower fallback engine for browsers that block WebAssembly |
| `data/openings.json` | Opening names, from lichess-org/chess-openings (CC0) |

## Credits and licences

- Stockfish 19 by the Stockfish developers, packaged by stockfish.js (GPLv3): https://github.com/nmrugg/stockfish.js
- chess.js (BSD-2-Clause) for move rules, loaded from jsDelivr.
- Pieces by Colin M.L. Burnett (GPLv2+ / BSD).
- Accuracy uses Lichess's published formula. Move labels use chess.com's published expected-points thresholds, so numbers can differ slightly from chess.com's own review.

Because the engine is GPLv3, keep this README and its source links when you redistribute the site.
