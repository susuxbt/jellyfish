# Jellyfish Smack 🎐

A smack of bioluminescent sea nettles, drawn point by point on a 2-D canvas.
No sprites, no meshes, no physics library — just a pixel buffer and some math.

**[▶ Live demo](https://susuxbt.github.io/jellyfish/)**

![demo](demo.mp4)

## What's going on

Each jelly integrates real impulse physics: a long refill phase, then a short
contraction that fires thrust, plus linear and quadratic water drag and turning
momentum. Between pulses they sink gently, so the pulsing feels necessary
rather than decorative.

- **Traveling contraction wave** — every bell point samples the pulse phase with
  a lag proportional to its distance from the apex, so each squeeze rolls
  visibly from the top of the bell down to the rim.
- **Translucent 3-D bell** — a surface of revolution sampled over polar angle
  *and* azimuth, with limb-brightened silhouette edges (you see more material
  tangentially), a specular sheen, pigment-stripe meridians and scalloped lappets.
- **Lagged tentacles** — the fourteen tentacles and four oral arms are jointed
  chains whose segment angles come from the body's *past* headings, stored in a
  ring buffer. They trail and whip through turns instead of rotating rigidly.
  Catmull-Rom interpolation smooths them into silky curves.
- **Gradient bioluminescence** — a smooth radial halo painted straight into the
  pixel buffer, whose brightness is wired to the physics thrust, so it flashes
  on every swim stroke.

## Controls

| Control | What it does |
| --- | --- |
| pulse power / water drag | the propulsion physics |
| tentacle lag | how far back in the body's history the chains read |
| tentacle reach / flexibility | length and wave amplitude |
| drift together | how strongly they align with neighbours |
| trail persistence | how much of the previous frame survives |
| anatomy layers | toggle bell, canals, manubrium, tentacles, arms |
| startle! | a fright response — double-strength pulses and a bright flash |

Click the water to startle the jellies near your cursor.

## Running it

It's a single self-contained HTML file with zero dependencies. Open `index.html`
in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Credits

Inspired by the tweet-sized p5.js sketches where every point is positioned by
pure math. Built with Claude Code.
