# Sonic-environment

*A colour-to-timbre sonification of 3D terrain. Rain drops sample the surface, wind agents perturb their trajectories, and impacts are quantised to a step sequencer.*

**Sonic-environment** is a web prototype that turns a 3D terrain under the rain into music. Each drop plays the timbre of the colour of the surface it hits. Wind and weather change where the drops land, and therefore what you hear. Impacts are quantised on a rhythmic grid of 16 steps (or triplets).

Yamagomori project. Status: research prototype, a single HTML file, no installation.

## How to use

1. Open `index.html` in a recent browser (or the page published with GitHub Pages) and press **Start** (or the space bar). The browser needs a user interaction to enable audio.
2. Listen: the **weather arc** moves on its own from calm to storm and back.
3. Rotate the scene by dragging, pan with Shift or right click, zoom with the wheel or pinch. Double click to reset the view.
4. Load a **`.glb`** file to use the colours of a real territory (or drag it into the window).
5. In **Active colours**: click to mute a colour, double click to hear it alone.
6. Move wind, rain and season for manual control. **Record** saves the audio as a `.webm` file.

The page loads Three.js from a CDN, so an internet connection is required.

## Publish with GitHub Pages

1. Upload `index.html` and `README.md` to the root of a public repository.
2. Go to *Settings → Pages*, choose *Deploy from a branch*, branch `main`, folder `/ (root)`, then *Save*.
3. After a few minutes the site is online at `https://YOUR-USERNAME.github.io/REPOSITORY-NAME/`.

## How it works

| Layer | What it does |
|---|---|
| Terrain | Column-based base shape or a loaded `.glb`. The area is read as a 64x64 grid of height and colour |
| Adaptive palette | Finds up to 8 dominant colours in the model and assigns each a timbre based on hue, lightness and saturation |
| Rain | Drops fall and leave a white ring that follows the terrain profile |
| Quantiser | Impacts accumulate in 16 quadrants (4x4) and sound on the next step. Each quadrant has a silence threshold |
| Rhythm | 16 steps per bar, or 12-step triplets (shuffle). Chord loop: Cm7, Ebmaj7, Fm7, Gm7 |
| Bass | Rhythmic pattern over the chords. Terrain roughness, the colour hit and the wind open the filter and add ghost notes |
| Agents | Wind with direction, gusts, turbulence, terrain deflection, updraft over rock, canopy holding drops, storm cells |
| Weather arc | Calm, breeze, gusts, storm, clearing. Adjustable length; pauses automatically when you take manual control |
| Humidity | With more rain the clay jar drops in pitch, the grain sound is damped, the lithophone rings longer |

### Timbres by colour

| Family | Typical colours | Sound |
|---|---|---|
| Bell | reds, magenta, violet | FM bell |
| Marimba | orange, yellow | Soft marimba |
| Kalimba | light greens | Kalimba |
| Reed flute | dark greens | Breathy tone, grows with the wind |
| Lithophone | greys | Tuned stone |
| Grain | sand | Soft noise grains |
| Clay jar | browns | Terracotta drum |
| Breath | very dark colours | Breath that anticipates the beat |
| Drop | blues | Water drop |
| Air | very light colours | Long, airy tone |

## Loading a model

- Format: a single `.glb`, with embedded textures, vertex colours or material colour.
- Draco compression is handled through the library loaded from the CDN. Meshopt is not supported.
- If the model has no colours, materials are assigned by altitude bands.
- Details smaller than one cell (about 1/64 of the width) are lost.

## Controls

| Control | Action |
|---|---|
| Space | Start or stop |
| W | Show or hide the wind arrows |
| R | Automatic model rotation |
| M | Automatic weather arc on or off |
| Double click on the scene | Reset the view |

## Known limits

- Only partly tested across browsers and models. Any problem loading a `.glb` appears as a red message in the status panel.
- Recording downloads a `.webm` file (MediaRecorder).
- With the base shape, colours come from altitude rules and not from a real map.

## Structure

```
index.html   complete application (HTML, CSS, JavaScript)
README.md    this file
```
