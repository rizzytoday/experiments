# Desktop Experiment – Full Glow-Up Design

**Purpose:** Interactive art toy – people should lose 20 minutes exploring, clicking, zooming, discovering hidden behaviors.

## 1. Reactive Color System
- Global hue rotates 360deg over ~60s
- Cursor X offsets hue +-40deg (left=cool, right=warm)
- Mouse speed + interaction intensity shifts saturation/lightness
- Each experiment has a hue offset from global base (0, 45, 90, etc.)
- Window border glow inherits experiment hue
- Background grid tints toward nearest window hue
- One `getHue(offset)` function replaces all hardcoded white rgba

## 2. Physics Play
- Cursor velocity creates directional "wake" force (not just radial push)
- Click-hold = gravity attractor (sucks elements toward click point)
- Shift+click = repulsor (blasts outward)
- Scroll wheel adjusts force radius (visible as ring size change)
- Pinch-to-zoom on trackpad = per-window zoom (replaces/supplements slider)
- Drag-reorder turbulence bleeds into nearby canvases
- Trail points have inertia (drift after push, settle back)
- Pendulum bobs gain energy from cursor pumping
- Cubes create splash wave from cursor impact
- Waves get amplitude injection at cursor point

## 3. Cross-Window Contamination
- Each experiment emits a "signal" (trail density, energy, amplitude, frequency)
- Adjacent grid neighbors pick up ~15% of neighbor signal
- Dragging window past others = ~40% bleed during pass
- Expanded (2x2) windows have stronger signal radius
- Faint connecting lines between adjacent windows pulse with signal
- Color hue bleeds between neighbors by ~10deg

## 4. Keyboard Shortcuts
- Space: pause/resume all (cursor still works on frozen state)
- 1-8: solo experiment (fullscreen, fade others)
- R: replay all
- G: toggle background grid
- C: cycle color mode (reactive / mono-white / mono-gold)
- Tab: cycle focus between windows
- Shift+click: clone window (max 4 clones)
- Alt+drag: detach from grid, free-float
- Shift+scroll: time dilation (0.25x to 4x)
- X: chaos mode (100% cross-window for 5s)
- M: mirror mode (horizontal flip all)
- I: invert (white bg, dark strokes)
- ?: hint circle appears after 10s idle

## 5. New Experiments (6 additions → 14 total)
- **Game of Life** – Conway's. Click toggles cells. Age-based color. Signal: population density
- **Boids** – 200 flocking birds. Cursor = predator. Click = food. Signal: flock velocity
- **Galaxy** – 500 orbiting stars. Cursor = gravity well. Click-fling. Signal: angular momentum
- **Mandelbrot** – Auto-zoom. Cursor picks target. Scroll = speed. Signal: zoom depth
- **Perlin Terrain** – Side-scroll noise terrain. Cursor warps field. Parallax layers. Signal: roughness
- **Double Pendulum** – Two-segment chaos. Click to grab+release tip. Signal: angular energy

## 6. Pinch-to-Zoom
- Trackpad pinch gesture maps to per-window zoom
- Captures wheel event with ctrlKey (how browsers report pinch)
- Smooth CSS transform scale on canvas
- Works alongside existing slider (syncs both)
