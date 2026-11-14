# Hanzi Playground

The eight Hanzi Heroes — 一 丁 上 下 木 人 乙 又 — at play in a playground, in a 2D version and a 3D version.

![The heroes as clay models in a sunlit 3D park](assets/preview-3d.jpg)

The heroes wander around, sit on the grass and the bench, ride the swings and seesaw, go down the slide and chase each other. No hero has a fixed job: each one picks its next activity at random. Click a hero to make it hop.

Live at **https://lokzzstudio.github.io/Hanzi_Playground/**

## Pages

| File | What it is |
| --- | --- |
| `index.html` | Entry page: choose the 2D or the 3D version. |
| `2d.html` | Flat illustrated playground in SVG. One self-contained file with no dependencies. |
| `3d.html` | 3D park built with three.js. Drag to look around, scroll to zoom. |

## Run it

Open `index.html` in any modern browser. There is no build step.

The 3D version loads three.js from the jsDelivr CDN, so it needs an internet connection. The 2D version works offline.

Add `?lineup` to the address of either version to see the whole cast standing in a row.

## Publishing

Every push to `main` deploys the repo to GitHub Pages through `.github/workflows/static.yml`. Under **Settings → Pages**, **Source** must be set to *GitHub Actions*.

## How it is built

Both versions share the same behaviour. A small state machine (`idle`, `walk`, `sit`, `chase`, `flee`, `use`) drives each hero. Swings, seesaw ends, bench seats and the slide are *slots*: a hero claims a free slot, walks to it and rides it.

**2D** — The characters are hand-written SVG with radial-gradient shading for a clay look, one entry each in the `HEROES` array. Heroes and equipment are sorted by their ground line on every frame, so nearer things draw in front.

**3D** — Everything is generated in code; there are no model or image files.

- Each hero is modelled from spheres, lathe shapes and swept limbs in a matte clay material, one entry each in the `HEROES` array.
- The scene is lit by a physical sky and a late-afternoon sun with soft shadows. Grass is about 100,000 blades that sway in the wind; trees are leaf cards that cast dappled shade.
- A depth-of-field pass keeps the playground sharp and softens the distance.
- If the frame rate drops, the page lowers its own quality in steps: resolution first, then depth of field, then grass density. Add `?fixed` to the address to turn that off.
