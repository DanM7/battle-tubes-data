# Battle Tubes data

Tunable game data for [Battle Tubes](https://github.com/DanM7/battle-tubes), kept in its own repo so edits never trigger a Netlify deploy of the game.

Everything lives in **`game.json`**: riders, CPU opponents, difficulties, physics, attacks, scores, passwords, taunts, audio cue lists, create-a-player color swatches, menu footer, and About pages.

## How the game loads it

- **Development:** check out this repo next to the game (`../battle-tubes-data/game.json`). `npm run dev` in the game serves that file at `/game.json`, so local edits show up on reload.
- **Production:** the built game fetches  
  `https://raw.githubusercontent.com/DanM7/battle-tubes-data/main/game.json`  
  (see `REMOTE_URL` in the game’s `src/gameData.js`).

Push changes here; the live site picks them up on the next page load—no game redeploy.

## Editing tips

- Colors are `"#rrggbb"` strings.
- Attack `reachEndExtra` and opponent `preferredDistanceExtra` are offsets from the tube width (so tube size can change without rewriting every distance).
- The last `heightBands` entry is `null` (unlimited / tallest band).
- Unlock and cheat passwords stay in sealed form (same as before); seal new ones with the game’s `passwords.js` helpers if you add any.
- Sprite paths still point at files inside the game’s `public/` folder—art stays with the app; only the data table is external.
- **`site.footer`:** menu copyright line. Use `{yyyy}` for the current year and `{link}` where the `linkLabel` / `linkUrl` hyperlink should sit.
- **`site.about.pages`:** list of pages; each page is a list of `{ "title", "lines": [...] }` sections (same header + paragraphs layout as the About screen).
- **`characters[].stats.<mode>.enduranceBonus`:** optional −5…+5 added to the height-based endurance pips (result clamped 0–5). Use this when a taller 2010 rider should still read as high endurance (e.g. Burton).
