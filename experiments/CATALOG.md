# Catalog

A living inventory of every experiment. 21 shipped, 0 WIP, infinite ideas.

---

## Math Art

The core collection. Local rules, emergent behavior, canvas-based.

| # | File | Title | Math Concept | Interaction | Color Theme | Status |
|---|------|-------|-------------|-------------|-------------|--------|
| 1 | `orbiters.html` | Orbiters | Phase-offset circular motion, wave propagation | None (pure animation) | Monochrome (white bg, black) | Shipped |
| 2 | `lissajous.html` | Lissajous Table | Parametric curves – x = sin(a·t), y = sin(b·t) | Hover to highlight, sliders (speed, trails, grid) | Monochrome (white bg, black curves) | Shipped |
| 3 | `phyllotaxis.html` | Phyllotaxis Engine | Golden angle spiral (137.5°), Fibonacci spirals | 6 sliders, hover to reveal spiral arms | 5 palettes: gold, ember, ice, forest, violet | Shipped |
| 4 | `oscillators.html` | Coupled Oscillators | Kuramoto model – phase-coupled synchronization | Click/drag pulse, scroll coupling, R/space | Deep blue/cyan gradient | Shipped |
| 5 | `attractor.html` | Strange Attractor | Chaotic attractors, density field accumulation | Sliders (shape, speed, glow), click clear | Purple/magenta gradient | Shipped |
| 6 | `sun.html` | Gravity Well | N-body gravity, orbital mechanics, accretion | 5 sliders, hover (2nd well), click burst | Black bg, temperature-mapped particles | Shipped |
| 7 | `moire.html` | Moiré Patterns | Interference patterns from overlapping periodic structures | Mouse offset, click cycle, scroll spacing, C color | Monochrome or RGB multiply | Shipped |

---

## Shaders

GPU-powered. WebGL fragment shaders. Connected via 1–8 key navigation.

| # | File | Title | Math Concept | Interaction | Color Theme | Status |
|---|------|-------|-------------|-------------|-------------|--------|
| 8 | `shader-sdf.html` | SDF – Signed Distance Functions | Raymarching, SDF primitives, smooth min, shadows, AO | Mouse orbit, scroll zoom, S screenshot | Dark space, position-based color | Shipped |
| 9 | `shader-noise.html` | Noise – Fractal Brownian Motion | Simplex noise, fBm, ridge noise, heightmap shading | Mouse X/Y (lacunarity/octaves), scroll scale | Ocean-to-volcanic gradient | Shipped |
| 10 | `shader-warp.html` | Warp – Domain Warping | IQ domain warping, nested fBm layers | Mouse stir, scroll warp depth | Warm ambers, teals, cosmic purples | Shipped |
| 11 | `shader-feedback.html` | Feedback – Frame Buffer Loops | Ping-pong FBOs, recursive transform, color rotation | Click drop ink, mouse field, scroll strength | Organic flowing, color cycling | Shipped |
| 12 | `shader-cosmos.html` | Cosmos – The Grand Finale | Raymarching, nebula, volumetric god rays, film grain | Mouse orbit, scroll depth | Deep space purple/blue | Shipped |
| 13 | `shader-audio.html` | Audio Reactive | FFT analysis, SDF deformation from frequency bands | Click toggle mic, scroll sensitivity | Hue-shifting by frequency | Shipped |
| 14 | `shader-morph.html` | Morph | Shape morphing (referenced in navigation) | Mouse, scroll, S screenshot | – | Referenced |
| 15 | `shader-physarum.html` | Physarum – Slime Mold Intelligence | Agent-based simulation, trail diffusion, sensor steering | Mouse attract, click deposit, scroll sensor angle | Teal/cyan gradient | Shipped |

---

## Interactive Toys

DOM-based, CSS-animated, personality-driven.

| # | File | Title | Concept | Interaction | Status |
|---|------|-------|---------|-------------|--------|
| 16 | `angry-button.html` | Don't Click | Glass button that spawns an angry creature with speech | Click | Shipped |
| 17 | `useless-switch.html` | Don't Turn This On | Hand emerges from hole and turns switch back off | Click toggle | Shipped |
| 18 | `the-eye.html` | The Eye | Realistic eye that tracks cursor, dilates, goes bloodshot | Mouse movement, click blink | Shipped |
| 19 | `love-game.html` | Love Connection | 2-player co-op – collect hearts, hug to fill love meter | WASD + Arrow keys | Shipped |
| 20 | `flip-clock.html` | 3D Flip Clock | WebGL2 voxel clock with proximity-reactive tile flips | Mouse orbit + hover, sliders, screenshot | Shipped |
| 21 | `living-code.html` | Living Code | Self-mutating code grid with noise-driven entropy | Mouse entropy, click burst, space reset | Shipped |

---

## Stats

- **Total experiments**: 21
- **Canvas 2D**: 8 (orbiters, lissajous, phyllotaxis, oscillators, attractor, sun, moire, living-code)
- **WebGL/Shaders**: 9 (7 shader series + flip-clock + physarum on WebGL)
- **DOM/CSS only**: 4 (angry-button, useless-switch, the-eye, love-game)
- **With slider panels**: 6 (attractor, flip-clock, lissajous, phyllotaxis, sun, oscillators)
- **With keyboard nav**: 8 (all shader-* files share 1–8 navigation)
- **Pure animation (no input)**: 1 (orbiters)
