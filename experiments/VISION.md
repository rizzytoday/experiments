# Vision

## The Thesis

The universe runs on math. Not metaphorically – literally. Every spiral, orbit, wave, and flicker you've ever seen is a function being evaluated in real time. The galaxy and the sunflower share the same spiral. Your heartbeat and a pendulum follow the same curve.

These experiments exist to make that visible.

Not "math education." Not "data visualization." This is math as art – where the code is the brush, the equations are the paint, and emergence is the whole point.

One equation. One canvas. No dependencies. Let it run.

---

## The Orbiters Principle

The single most important lesson from building these experiments came from the simplest one.

**Orbiters** is 100 lines of code. A grid of circles. Each has a dot orbiting inside it. The only twist: the phase offset of each dot is proportional to its distance from the center of the grid.

That's it. One rule. `phase = distance * 0.45`.

And the result is a hypnotic, pulsing, organic wave that looks like it was designed by a team of motion graphics artists. It wasn't designed at all – it emerged from a single local rule applied globally.

This is the principle:

> **Emergence beats applied formulas.**
>
> Don't design the global pattern. Design the local rule.
> The global pattern will design itself.

The first round of experiments tried to make pretty things by applying math – "let's draw a Lissajous curve." They worked, but they felt like illustrations.

The second round reversed the approach – "let's give each element a simple rule, and see what the whole system does." Orbiters, oscillators, attractors, the gravity well. These feel alive. They surprise you. They have behaviors you didn't program.

That's the difference between a drawing and a system.

---

## What Makes an Experiment "Alive"

After building 21 of these, a pattern emerged. The ones that work – the ones you stare at – share 4 ingredients:

### 1. Local Rule → Global Behavior

One equation per element. The emergent behavior comes from many elements following the same rule with different inputs.

- **Orbiters**: phase = distance from center
- **Oscillators**: dθ/dt = ω + (K/N) Σ sin(θ_j − θ_i) – each needle adjusts to its neighbors
- **Phyllotaxis**: place dot n at angle n × 137.5° – Fibonacci spirals appear on their own
- **Gravity Well**: F = G/d² – particles spiral, accrete, and form orbital patterns nobody asked for

### 2. Structure + Motion Contrast

The best experiments have something still and something moving. The tension between structure and motion is what makes them watchable.

- **Orbiters**: still circles, moving dots
- **Lissajous**: still grid, tracing curves
- **Attractor**: still canvas, accumulating density
- **Oscillators**: still grid, pulsing needles

### 3. Visual Density from Overlap

Sparse things look like demos. Dense things look like art. When elements overlap, interfere, and accumulate – you get texture, depth, visual richness that a single element could never produce.

- Orbiters' interlocking circles create moiré-like interference
- The attractor accumulates millions of points into density fields
- Phyllotaxis packs thousands of dots into concentric spirals
- Oscillators run 2,304 coupled needles on a 48×48 grid

### 4. One Equation Does All the Work

No conditionals, no special cases, no "if near the edge, do something different." The beauty comes from a single mathematical relationship applied uniformly. The equation IS the design.

---

## Design Language

Every experiment follows the same constraints. These aren't arbitrary – they're load-bearing.

### Standalone HTML

One file. No build step. No dependencies. No npm install. Open the file, see the art. This forces clarity – you can't hide behind abstractions. Every line is visible.

### Canvas (2D or WebGL)

The browser is the gallery. Canvas for particle systems and physics. WebGL for shaders and GPU compute. Both are native, fast, and universal.

### DPR-Aware

Every canvas respects `window.devicePixelRatio`. Crisp on retina, correct on everything else. This is non-negotiable – blurry math art is just blurry.

### No Dependencies

Zero external libraries. Not even a math utility. If you need noise, write noise. If you need a matrix, multiply it yourself. This keeps the experiments honest – every behavior is traceable to code you wrote.

### Themed Color Palettes

Each experiment has a color identity:
- **Gold/Amber** – phyllotaxis (warmth, nature, the golden ratio)
- **Purple/Magenta** – attractors (chaos, fractal space, mystery)
- **Blue/Cyan** – oscillators (precision, cold mathematics, sync)
- **Monochrome** – orbiters, lissajous, moiré (pure form, no distraction)
- **Warm Space** – gravity well (cosmic, heat-mapped particles)
- **Shifting Hue** – shaders (the GPU does what it wants)

### Glass Morphism Control Panels

When an experiment has sliders, they live in a frosted glass panel – `backdrop-filter: blur(20px)`, monospace type at 11px, themed to match the experiment's palette. The panel is part of the aesthetic, not bolted on.

---

## Interaction Philosophy

Not every experiment needs interaction. But when it does, it should feel like an invitation, not a demand.

### Good Interactions

**Hover-to-focus** (Lissajous, Phyllotaxis) – move your mouse near a curve or spiral arm, and it highlights. Everything else dims. You're exploring, not controlling. The system is still running – you're just shining a flashlight.

**Scroll-to-adjust** (Oscillators, Shaders) – scroll wheel maps to a single continuous parameter. Coupling strength, zoom depth, warp intensity. One axis of control. Feels like turning a dial.

**Click-to-event** (Gravity Well, Attractor) – click triggers a burst, a clear, a reset. Discrete, dramatic, satisfying. Not a mode change – an event.

**Sliders-as-exploration** (Phyllotaxis, Attractor, Sun) – 3–6 sliders that let you wander through parameter space. Each slider changes one thing. The label tells you what. The hint text tells you what to expect. You're playing with it.

### Bad Interactions

**Mouse hijacking** – when the cursor position IS the simulation (cursor becomes a gravity well, everything chases your mouse). It stops being art and starts being a tech demo. The cursor should influence, not dominate.

**Too many sliders** – if you have more than 6, you have a control panel, not an exploration. Trim it down. Find the parameters that actually matter.

**Confusing parameter names** – "explore" is better than "preset_lerp_index." "glow" is better than "density_decay_multiplier." Name them by what they feel like, not what they compute.

**Mandatory interaction** – the experiment should be beautiful by default, with no input at all. Interaction should be discovery, not a requirement.

---

## Zen's Voice

This is art that reveals math, not math dressed up as art.

The difference matters. We're not taking equations and making them pretty for Instagram. We're building systems where the math is the source of beauty – where `sin` and `cos` and `phase offset` produce something that makes you stop scrolling and stare.

The experiments are personal. They're not tutorials. They're not demos. They're the answer to: "what happens if I try this?"

And sometimes the answer is boring. And sometimes it's orbiters.

Keep building. Keep the files simple. Let the math do the work.

— riz
