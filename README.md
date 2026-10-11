# stage — self-hosted player

Drop this folder into a GitHub repository and turn Pages on. Nothing else to build.

```
index.html    the player
stage.riv     the signed build (copy of stage/build/stage.riv)
```

`stage.riv` must be served from the **same origin** as `index.html`. It carries no
`access-control-allow-origin`, so a cross-origin fetch will fail.

The runtime is loaded from the CDN (`@rive-app/webgl2@2.x.x`, currently 2.44.2) — the
same package and version specifier the rive.to player uses.

## Query parameters

| parameter | effect |
|---|---|
| `?test`   | skips straight to the stage→backstage slide, 1 second after load |
| `?debug`  | shows a small readout (current `stage` value, then slide progress) |

## Test checklist

1. Open the page. The stage should render full-bleed, mist running, curtains framing.
2. Solve puzzles 1, 2 and 3. When `stage` reaches 4 the curtains close and the slide fires.
3. The stage should glide off to the right while backstage glides in from the left.
4. After the slide, the stage canvas is removed. Click the door — it must respond.
5. The door click should flip `walk`, play the zoom, then the jumpscare (screen to black).
6. Then the hint reveal: the note appears, zooms in, straightens, glitches, and the
   fake hint swaps to the real one, holds ~2.5s, then the screen goes black again.
7. Open `?debug` and confirm the readout shows `stage = 4` at the moment of the slide.

To test the slide without playing the puzzles, open `?test` (or `?test&debug`).
