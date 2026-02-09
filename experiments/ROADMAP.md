# Roadmap

The pipeline. Things we want to build, ordered by how badly we want to see them.

---

## Unbuilt from Round 2

These were fully specced but never built. The math is ready.

### 1. Fourier Epicycles
**Math**: Discrete Fourier Transform – decompose any path into a series of rotating circles.

Draw something freehand. The system decomposes your drawing into frequency components, then replays it as nested spinning circles – each circle's radius is the amplitude of a frequency, each rotation speed is the frequency itself. Watch a stack of spinning circles reconstruct your doodle.

**Interaction**: Draw on canvas → DFT decomposition → animated replay. Slider for number of terms (more circles = more accurate). Toggle to show/hide the circle stack.

**Why it'd be compelling**: Everyone's seen the "Fourier series draws Homer Simpson" video. This makes it interactive – draw anything, see it decomposed.

**Difficulty**: Medium

---

### 2. Reaction-Diffusion (Gray-Scott)
**Math**: Two-chemical reaction-diffusion system. Feed rate (f) and kill rate (k) control whether the system produces spots, stripes, waves, or chaos.

∂u/∂t = Du∇²u − uv² + f(1−u)
∂v/∂t = Dv∇²v + uv² − (f+k)v

GPU-accelerated on a ping-pong framebuffer. Click to seed new chemicals. Sliders for f and k navigate the wildly different pattern regimes.

**Interaction**: Click to seed, sliders for f/k, presets for "mitosis", "coral", "maze", "spots."

**Why it'd be compelling**: The parameter space is stunningly diverse – tiny changes in f/k produce completely different organisms. It's the ultimate "one equation, infinite outcomes" experiment.

**Difficulty**: Medium (WebGL ping-pong, similar to shader-feedback)

---

### 3. Flow Field (Curl Noise)
**Math**: 2D curl noise – take the curl of a 3D noise field to get a divergence-free velocity field. Particles follow the flow and never converge or diverge.

Thousands of particles streaming through a field of invisible forces. The noise evolves over time, so the flow shifts and eddies form. Trails persist and accumulate.

**Interaction**: Mouse warps the flow field locally. Scroll adjusts noise scale (tight eddies vs. sweeping currents). Click resets particles.

**Why it'd be compelling**: Flow fields are one of the most visually stunning generative art techniques. The curl-noise version guarantees smooth, looping flow with no sinks or sources.

**Difficulty**: Quick (canvas 2D, simple noise + particle system)

---

## Nature Simulations

Biology-inspired emergence. These are the "holy shit it's alive" experiments.

### 4. Flocking (Boids)
**Math**: Reynolds' 3 rules – separation (avoid crowding), alignment (steer toward average heading), cohesion (steer toward average position). Each boid follows all three simultaneously.

**Interaction**: Sliders for separation/alignment/cohesion weights. Click to add predator (boids flee). Mouse attracts or repels. Toggle "species" mode (2 flocks that avoid each other).

**Why it'd be compelling**: The flock behaves like a living organism. Tight turns, dynamic reshaping, predator avoidance – all from 3 rules.

**Difficulty**: Quick

---

### 5. Erosion Simulation
**Math**: Hydraulic erosion – rain droplets carry sediment downhill, depositing when they slow down. Thermal erosion breaks peaks. Height field evolves over time.

**Interaction**: Click to place mountains. Rain rate slider. Toggle between erosion modes. Time-lapse the terrain evolution.

**Why it'd be compelling**: Watch a procedural mountain range get carved by water. Rivers form, valleys deepen, sediment fans spread at the base. Geological time in real time.

**Difficulty**: Deep

---

### 6. Crystal Growth (DLA)
**Math**: Diffusion-limited aggregation – random walkers stick when they touch the growing crystal. The result is fractal branching patterns identical to real crystals, lightning, and coral.

**Interaction**: Click to place seed points. Slider for stickiness probability (affects branch density). Color by arrival time.

**Why it'd be compelling**: DLA produces the most naturally fractal structures of any simulation. And it's dead simple – random walk + stick rule = infinite complexity.

**Difficulty**: Medium

---

### 7. Lightning (Lichtenberg Figures)
**Math**: Dielectric breakdown model – electric potential field solved via Laplace equation, growth probability proportional to local field gradient. The path of least resistance branches fractally.

**Interaction**: Click to set strike origin. Scroll adjusts branching probability (η parameter – higher = more branchy). Multiple strikes accumulate.

**Why it'd be compelling**: Instant lightning bolts that look real. The branching is physically motivated, not random – each new segment grows toward the strongest field gradient.

**Difficulty**: Medium

---

## 3D Explorations

Three.js or raw WebGL. New dimension, literally.

### 8. 3D Strange Attractor
**Math**: Lorenz, Rössler, or Chen attractor in 3D space. Camera orbits the trajectory. Trail accumulates as a glowing ribbon or point cloud.

**Interaction**: Mouse orbits camera. Scroll adjusts trail length. Sliders for attractor parameters. Toggle between attractor types.

**Why it'd be compelling**: We already have the 2D attractor. Seeing these curves in 3D – the butterfly shape of Lorenz, the folded band of Rössler – is transformative. The depth makes the chaos tangible.

**Difficulty**: Medium

---

### 9. Phyllotaxis Sphere
**Math**: Fibonacci sphere packing – place N points on a sphere using the golden angle. Same math as the flat phyllotaxis but mapped to spherical coordinates.

**Interaction**: Mouse rotates sphere. Scroll adjusts point count. Slider for angle (watch the patterns reorganize). Color by latitude or spiral index.

**Why it'd be compelling**: The 2D version is beautiful. The 3D version is a planet covered in Fibonacci spirals. It connects phyllotaxis to the geometry of spheres.

**Difficulty**: Quick

---

### 10. Oscillator Grid with Height
**Math**: Same Kuramoto model as the 2D oscillators, but phase maps to vertical displacement. A flat grid that breathes, ripples, and synchronizes in 3D.

**Interaction**: Same as oscillators – click pulse, scroll coupling. Camera orbit. Toggle between phase-as-color and phase-as-height.

**Why it'd be compelling**: The 2D oscillator grid is already mesmerizing. Adding the Z dimension turns it into a living surface – waves propagate, sync domains rise and fall.

**Difficulty**: Medium

---

## Audio-Reactive

Sound as input. Frequencies as parameters.

### 11. Frequency Landscape
**Math**: FFT bins mapped to a scrolling 3D terrain. Low frequencies are mountains, high frequencies are fine texture. The landscape is generated in real time from what you hear.

**Interaction**: Mic input or audio file upload. Camera auto-scrolls forward. Scroll adjusts camera angle. Color mapped to amplitude.

**Why it'd be compelling**: Music becomes a place you can fly through. Every song generates a unique landscape.

**Difficulty**: Medium

---

### 12. Chladni Patterns
**Math**: Chladni plate vibration – 2D standing waves. `sin(n·πx/L)·sin(m·πy/L)` produces nodal lines where particles accumulate (the "sand on a vibrating plate" effect). Drive the modes with audio frequency.

**Interaction**: Mic input selects which mode resonates. Sliders for manual mode selection. Particles settle on nodal lines.

**Why it'd be compelling**: Historically one of the most beautiful physics demos. Making it audio-reactive means your voice literally draws the patterns.

**Difficulty**: Medium

---

## Cursor-as-Physics

The mouse isn't a pointer – it's a force.

### 13. Gravity Cursor
**Math**: Cursor position creates a gravity well in a particle field. Inverse-square attraction. Click to toggle between attract and repel. Hold to increase mass.

**Interaction**: Mouse = gravity source. Click toggles polarity. Scroll adjusts mass. Particles orbit, accrete, scatter.

**Why it'd be compelling**: Similar to the gravity well experiment but the cursor IS the well. Direct, physical, satisfying. Watch thousands of particles orbit your fingertip.

**Difficulty**: Quick

---

### 14. Light Source Cursor
**Math**: Cursor is a point light in a 2D scene. Particles cast "shadows" – rays from cursor through particle centers project shadow lines onto a boundary. Move the light, watch the shadows dance.

**Interaction**: Mouse = light position. Scroll adjusts number of shadow rays. Click to freeze/unfreeze particles.

**Why it'd be compelling**: Shadow play is primal. A simple particle field becomes a shadow puppet theater when you add a single light source.

**Difficulty**: Medium

---

## Multi-Experiment Connections

### 15. The Gallery (Index Page)
**Math**: The index page IS an experiment. Thumbnails of each experiment rendered as live canvas previews. They orbit, attract, respond to the mouse. Click one to enter.

**Interaction**: Mouse navigates. Scroll zooms. Thumbnails are alive – mini versions of each experiment running in real time.

**Why it'd be compelling**: Instead of a boring list of links, the gallery itself demonstrates the aesthetic. First impression IS the art.

**Difficulty**: Deep

---

## Advanced Interactions

### 16. Device Orientation (Mobile Gyroscope)
Take an existing experiment (phyllotaxis, oscillators) and map phone tilt to parameters. Tilt forward = zoom in. Tilt sideways = rotate. The phone becomes a window into a mathematical world you can look around in.

**Difficulty**: Quick (API is simple, experiment already exists)

---

### 17. WebMIDI Slider Control
Connect a physical MIDI controller. Map its knobs and sliders to experiment parameters. Phyllotaxis with hardware controls would feel like playing an instrument.

**Difficulty**: Quick (WebMIDI API is straightforward)

---

### 18. Terrain Erosion + Flow Field Hybrid
**Math**: Height map from noise. Rain particles follow gravity downhill (gradient descent). Water accumulates, carves channels. The flow field IS the terrain gradient. Curl noise adds turbulence to the water surface.

**Interaction**: Click to raise terrain. Right-click to dig. Rain rate slider. Toggle erosion types.

**Why it'd be compelling**: Combines two beautiful systems – procedural terrain and flow fields. Water follows physics, not predetermined paths.

**Difficulty**: Deep

---

### 19. Voronoi Shatter
**Math**: Voronoi tessellation with animated seed points. The cells shift, merge, split as seeds move. Color each cell by distance to edge (creates a glowing-cracks effect). Add physics so cells can "shatter" on click.

**Interaction**: Click to add new seeds. Mouse repels nearby seeds. Scroll adjusts seed count.

**Why it'd be compelling**: Voronoi is everywhere in nature (giraffe spots, dried mud, soap bubbles). Animating the seeds makes the tessellation feel alive and organic.

**Difficulty**: Medium

---

### 20. Pendulum Wave
**Math**: N pendulums with slightly different lengths. They start in sync, then desynchronize into beautiful wave patterns, then re-sync. The cycle period depends on the length ratios.

**Interaction**: Slider for number of pendulums. Click to release from sync. Toggle between side view and top-down (Lissajous-like patterns from above).

**Why it'd be compelling**: The pendulum wave is one of the most mesmerizing physical demonstrations. The sync → desync → resync cycle is deeply satisfying and mathematically inevitable.

**Difficulty**: Quick

---

## Ideas on the Back Burner

- **Mandelbrot deep zoom** – smooth coloring, arbitrary precision for deep zooms
- **L-system trees** – recursive branching with wind simulation
- **Wave equation** – 2D drum membrane simulation (ripple tank)
- **Cellular automata zoo** – Life, Langton's ant, wireworld, all in one page
- **Magnetic field lines** – place dipoles, watch field lines emerge
- **Double pendulum** – chaotic motion with trail persistence
- **Spirograph engine** – nested rotating circles with pen at arbitrary radius

---

## Difficulty Key

| Level | Time | Complexity |
|-------|------|-----------|
| Quick | 1–2 hours | Known patterns, straightforward math |
| Medium | Half day | New technique or WebGL pipeline work |
| Deep | Full day+ | Multiple systems interacting, heavy GPU compute |
