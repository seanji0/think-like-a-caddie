[README.md](https://github.com/user-attachments/files/35056106/README.md)
# Think Like a Caddie

A single-file, browser-based golf simulator. Enter your handicap and club distances, then play a par-4 by choosing target lines, clubs, chips, and putt reads. Every shot is drawn from a dispersion model built from your handicap, your go-to miss, and your lie.

**No build step, no dependencies.** Open `index.html` in a browser and play.

## Features

- **Setup:** handicap slider, one-way go-to miss (draw/hook, fade/slice, or straight), putting touch, and a full club picker (choose which clubs are in your bag and set each carry distance)
- **Shot model:** angular spread and distance variance scale with handicap; rough, trees, and bunkers widen dispersion and cost distance; water adds a penalty stroke
- **Aiming:** click to set a target line; a live tag shows distance from the tee and distance for the shot
- **Short game:** chip types (bump & run, pitch, flop, sand splash) depend on your lie
- **Putting:** color-coded break arrows (green = slow, yellow = medium, red = fast) show slope direction and speed; a compact version appears on approach shots too
- **Animated ball flight:** shots curve from the aim line to where they actually finish
- **Quality of life:** undo last stroke, mid-round club/distance editing, automatic tap-in finish inside ~2 feet

## Run locally

```bash
git clone <your-repo-url>
cd <your-repo>
open index.html     # or just double-click the file
```

Fonts (Fraunces, Inter, IBM Plex Mono) load from Google Fonts, so the first load needs an internet connection; the game falls back to system fonts offline.

## Host on GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Under **Build and deployment**, set Source to **Deploy from a branch**, choose `main` and `/ (root)`
4. Your game will be live at `https://<username>.github.io/<repo>/`

## How the model works

| Piece | Behavior |
|---|---|
| Angular dispersion | Grows with handicap, multiplied by lie (rough 1.35x, trees 1.9x, bunker 1.55x) |
| Distance variance | Grows with handicap and worsens from bad lies |
| Go-to miss | Constant one-way bias on every shot's mean direction |
| Putting | Break is computed from the green's slope; your aim is compared to the ideal line, plus handicap-scaled touch noise |

This is a probability model, not a physics engine.

## Roadmap ideas

- More holes / a full 18
- Per-hole green contours instead of a single tilted plane
- Round scorecard and stats tracking
