# Patterns

Technical reference for building new experiments. Copy-paste starters, reusable patterns, and lessons learned.

---

## Boilerplate – Canvas 2D Experiment

The standard starting point. Every Canvas 2D experiment uses this structure.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Experiment Name</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: #000; overflow: hidden; cursor: crosshair; }
canvas { display: block; }
</style>
</head>
<body>
<canvas id="c"></canvas>
<script>
const canvas = document.getElementById('c');
const ctx = canvas.getContext('2d');

function resize() {
  const dpr = window.devicePixelRatio || 1;
  canvas.width = window.innerWidth * dpr;
  canvas.height = window.innerHeight * dpr;
  canvas.style.width = window.innerWidth + 'px';
  canvas.style.height = window.innerHeight + 'px';
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
}
resize();
window.addEventListener('resize', resize);

let paused = false;

document.addEventListener('keydown', e => {
  if (e.code === 'Space') { e.preventDefault(); paused = !paused; }
});

function draw(t) {
  if (!paused) {
    const w = window.innerWidth;
    const h = window.innerHeight;
    ctx.clearRect(0, 0, w, h);

    // Your drawing code here
  }
  requestAnimationFrame(draw);
}
requestAnimationFrame(draw);
</script>
</body>
</html>
```

---

## Boilerplate – WebGL Shader Experiment

The standard starting point for fragment shader experiments.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shader Name</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body { background: #000; overflow: hidden; cursor: crosshair; }
canvas { display: block; width: 100vw; height: 100vh; }
</style>
</head>
<body>
<canvas id="c"></canvas>
<script>
const canvas = document.getElementById('c');
const gl = canvas.getContext('webgl', { antialias: false, preserveDrawingBuffer: true });

let mouse = [0.5, 0.5], time = 0, paused = false, zoom = 1.0;

const vsrc = `attribute vec2 a_pos;
void main() { gl_Position = vec4(a_pos, 0.0, 1.0); }`;

const fsrc = `precision highp float;
uniform float u_time;
uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_zoom;

void main() {
  vec2 uv = (gl_FragCoord.xy - 0.5 * u_resolution) / min(u_resolution.x, u_resolution.y);

  // Your shader code here
  vec3 col = vec3(0.0);

  gl_FragColor = vec4(col, 1.0);
}`;

// Resize
function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  gl.viewport(0, 0, canvas.width, canvas.height);
}
resize();
window.addEventListener('resize', resize);

// Compile shader
function compile(type, src) {
  const s = gl.createShader(type);
  gl.shaderSource(s, src);
  gl.compileShader(s);
  if (!gl.getShaderParameter(s, gl.COMPILE_STATUS))
    console.error(gl.getShaderInfoLog(s));
  return s;
}

const prog = gl.createProgram();
gl.attachShader(prog, compile(gl.VERTEX_SHADER, vsrc));
gl.attachShader(prog, compile(gl.FRAGMENT_SHADER, fsrc));
gl.linkProgram(prog);
gl.useProgram(prog);

// Fullscreen triangle (covers viewport with 1 triangle instead of 2)
const buf = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, buf);
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([-1,-1, 3,-1, -1,3]), gl.STATIC_DRAW);
const aPos = gl.getAttribLocation(prog, 'a_pos');
gl.enableVertexAttribArray(aPos);
gl.vertexAttribPointer(aPos, 2, gl.FLOAT, false, 0, 0);

// Uniforms
const uTime = gl.getUniformLocation(prog, 'u_time');
const uRes = gl.getUniformLocation(prog, 'u_resolution');
const uMouse = gl.getUniformLocation(prog, 'u_mouse');
const uZoom = gl.getUniformLocation(prog, 'u_zoom');

// Events
canvas.addEventListener('mousemove', e => {
  mouse = [e.clientX / window.innerWidth, 1.0 - e.clientY / window.innerHeight];
});
canvas.addEventListener('wheel', e => {
  zoom = Math.max(0.3, Math.min(3.0, zoom + e.deltaY * 0.001));
  e.preventDefault();
}, { passive: false });
window.addEventListener('keydown', e => {
  if (e.code === 'Space') { paused = !paused; e.preventDefault(); }
  if (e.code === 'KeyS') {
    const link = document.createElement('a');
    link.download = 'shader-name.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
  }
});

// Render loop
function frame(now) {
  if (!paused) time = now * 0.001;
  gl.uniform1f(uTime, time);
  gl.uniform2f(uRes, canvas.width, canvas.height);
  gl.uniform2f(uMouse, mouse[0], mouse[1]);
  gl.uniform1f(uZoom, zoom);
  gl.drawArrays(gl.TRIANGLES, 0, 3);
  requestAnimationFrame(frame);
}
requestAnimationFrame(frame);
</script>
</body>
</html>
```

---

## Slider Panel Pattern

The glass morphism control panel used across 6+ experiments. Theme the colors to match each experiment's palette.

### CSS

```css
.controls {
  position: fixed; bottom: 16px; right: 16px;
  background: rgba(COLOR_R, COLOR_G, COLOR_B, 0.75);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(ACCENT_R, ACCENT_G, ACCENT_B, 0.1);
  border-radius: 14px;
  padding: 14px 18px;
  font: 11px/1.6 monospace;
  color: rgba(ACCENT_R, ACCENT_G, ACCENT_B, 0.55);
  min-width: 190px;
  z-index: 10;
  box-shadow: 0 4px 24px rgba(0,0,0,0.3);
}
.controls label {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 5px 0;
}
.controls span {
  min-width: 42px;
  text-align: right;
  color: rgba(ACCENT_R, ACCENT_G, ACCENT_B, 0.8);
}
input[type=range] {
  -webkit-appearance: none;
  width: 100px; height: 3px;
  background: rgba(ACCENT_R, ACCENT_G, ACCENT_B, 0.12);
  border-radius: 2px; outline: none; margin: 0 8px;
}
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 12px; height: 12px;
  background: ACCENT_HEX;
  border-radius: 50%; cursor: pointer;
}
.hint {
  color: rgba(ACCENT_R, ACCENT_G, ACCENT_B, 0.2);
  margin-top: 10px; font-size: 10px; line-height: 1.5;
}
```

### HTML

```html
<div class="controls">
  <label>name <input type="range" id="param" min="0" max="100" step="1" value="50"> <span id="paramV">50</span></label>
  <div class="hint">describe what the slider does</div>
</div>
```

### JS Binding

```javascript
const paramEl = document.getElementById('param');
let paramValue = 50;

paramEl.oninput = () => {
  paramValue = +paramEl.value;
  document.getElementById('paramV').textContent = paramValue;
};
```

### Themed Panel Examples

| Experiment | Background RGBA | Accent Color | Thumb Hex |
|-----------|----------------|--------------|-----------|
| Attractor | `rgba(16,10,30,0.75)` | `rgba(180,100,255,...)` | `#b480ff` |
| Phyllotaxis | `rgba(30,24,16,0.75)` | `rgba(252,225,132,...)` | `#FCE184` |
| Gravity Well | `rgba(0,0,0,0.6)` | `rgba(255,255,255,...)` | `rgba(255,255,255,0.7)` |
| Oscillators | `rgba(6,10,16,0.75)` | `rgba(100,200,255,...)` | `#64c8ff` |

---

## Interaction Models

### Hover-to-Focus

Used in Lissajous and Phyllotaxis. The mouse highlights nearby elements without changing the simulation.

```javascript
canvas.addEventListener('mousemove', e => {
  mouseX = e.clientX;
  mouseY = e.clientY;
});

// In draw loop – per element:
const dx = elementX - mouseX;
const dy = elementY - mouseY;
const dist = Math.sqrt(dx * dx + dy * dy);
const highlight = dist < 80; // radius of influence

ctx.globalAlpha = highlight ? 1.0 : 0.15; // dim everything else
```

### Click-to-Pause

Universal across experiments:

```javascript
let paused = false;
document.addEventListener('keydown', e => {
  if (e.code === 'Space') { e.preventDefault(); paused = !paused; }
});
// or
canvas.addEventListener('click', () => { paused = !paused; });
```

### Scroll-to-Adjust

Single parameter mapped to scroll wheel:

```javascript
let param = 1.0;
canvas.addEventListener('wheel', e => {
  param = Math.max(MIN, Math.min(MAX, param + e.deltaY * SENSITIVITY));
  e.preventDefault();
}, { passive: false });
```

### Keyboard Shortcuts

Standard set across shader experiments:

```javascript
window.addEventListener('keydown', e => {
  if (e.code === 'Space') { paused = !paused; e.preventDefault(); }
  if (e.code === 'KeyS') { /* screenshot */ }
  if (e.code === 'KeyR') { /* reset */ }
});
```

---

## Color Palettes

### HSL Generation

The most common color approach – generate colors from a hue:

```javascript
function hsl(h, s, l, a = 1) {
  return `hsla(${h}, ${s}%, ${l}%, ${a})`;
}

// Cycling hue
const hue = (time * 30) % 360;

// Position-based hue
const hue = (index / total) * 360;

// Distance-based brightness
const brightness = 1 - Math.min(dist / maxDist, 1);
```

### Temperature Ramp (Gravity Well Style)

Map a 0–1 value to a cool→hot gradient:

```javascript
function tempColor(t, alpha) {
  // t: 0 = cool/dim, 1 = hot/bright
  const r = Math.min(1, t * 3);
  const g = Math.min(1, Math.max(0, (t - 0.33) * 3));
  const b = Math.min(1, Math.max(0, (t - 0.66) * 3));
  return `rgba(${r*255|0}, ${g*255|0}, ${b*255|0}, ${alpha})`;
}
```

### Multi-Palette System (Phyllotaxis Style)

Predefine named palettes and switch between them:

```javascript
const palettes = [
  { name: 'gold',   bg: '#0a0804', colors: ['#FCE184', '#f5c542', '#d4982a'] },
  { name: 'ember',  bg: '#0a0404', colors: ['#ff6b35', '#ff4444', '#cc2200'] },
  { name: 'ice',    bg: '#040608', colors: ['#88ccff', '#44aaee', '#2288cc'] },
  { name: 'forest', bg: '#040804', colors: ['#88ff88', '#44cc44', '#228822'] },
  { name: 'violet', bg: '#08040a', colors: ['#cc88ff', '#aa44ee', '#8822cc'] },
];

let paletteIdx = 0;
const palette = palettes[paletteIdx];
document.body.style.background = palette.bg;
```

### GLSL Color Palette (Shader Experiments)

IQ's cosine palette – 4 vec3 parameters produce infinite smooth gradients:

```glsl
vec3 palette(float t, vec3 a, vec3 b, vec3 c, vec3 d) {
  return a + b * cos(6.28318 * (c * t + d));
}

// Example: warm sunset
vec3 col = palette(value, vec3(0.5), vec3(0.5), vec3(1.0), vec3(0.0, 0.33, 0.67));
```

---

## Performance Notes

### ImageData for Pixel-Level Work

When you need to write individual pixels (attractor density fields, cellular automata):

```javascript
const imageData = ctx.createImageData(width, height);
const data = imageData.data; // Uint8ClampedArray

// Write pixel at (x, y)
const i = (y * width + x) * 4;
data[i]     = r;  // 0-255
data[i + 1] = g;
data[i + 2] = b;
data[i + 3] = 255;

// Flush to canvas
ctx.putImageData(imageData, 0, 0);
```

### Float32Array / Float64Array for Physics

When you need precision beyond 8-bit (accumulation buffers, phase storage):

```javascript
// Density buffer (attractor) – Float32Array for millions of accumulations
const density = new Float32Array(width * height);
density[y * width + x] += 1;

// Phase storage (oscillators) – Float64Array for precision
const phases = new Float64Array(N);
// Kuramoto: dθ/dt = ω + (K/N) Σ sin(θ_j - θ_i)
```

### requestAnimationFrame Timing

Use the timestamp parameter for consistent animation speed:

```javascript
let lastT = 0;

function draw(t) {
  const dt = Math.min((t - lastT) / 1000, 0.05); // cap at 50ms to prevent jumps
  lastT = t;

  // Use dt for physics, t for oscillations
  position += velocity * dt;
  const wave = Math.sin(t * 0.001);

  requestAnimationFrame(draw);
}
```

### Trail Rendering Approaches

**Approach 1: Fade overlay** – draw a semi-transparent rectangle each frame:
```javascript
ctx.fillStyle = `rgba(0, 0, 0, ${fadeFactor})`;
ctx.fillRect(0, 0, w, h);
// Then draw new frame on top
```
Simple but the fade is exponential, not linear. Good enough for most cases.

**Approach 2: Trail array** – store last N positions:
```javascript
const trail = [];
trail.push({ x, y });
if (trail.length > maxTrail) trail.shift();

for (let i = 0; i < trail.length; i++) {
  const alpha = i / trail.length;
  ctx.globalAlpha = alpha;
  ctx.beginPath();
  ctx.arc(trail[i].x, trail[i].y, r, 0, Math.PI * 2);
  ctx.fill();
}
```
More control but more memory. Use for precise trail effects.

**Approach 3: Line from trail** – draw a line through trail points:
```javascript
ctx.beginPath();
ctx.moveTo(trail[0].x, trail[0].y);
for (let i = 1; i < trail.length; i++) {
  ctx.lineTo(trail[i].x, trail[i].y);
}
ctx.stroke();
```
Used in the gravity well for meteor trails.

### Batch Path Drawing

When drawing many identical shapes, use a single `beginPath()` / `stroke()`:

```javascript
// GOOD – one draw call
ctx.beginPath();
for (let i = 0; i < N; i++) {
  ctx.moveTo(x + r, y);
  ctx.arc(x, y, r, 0, Math.PI * 2);
}
ctx.stroke(); // one call

// BAD – N draw calls
for (let i = 0; i < N; i++) {
  ctx.beginPath();
  ctx.arc(x, y, r, 0, Math.PI * 2);
  ctx.stroke(); // called N times
}
```

This makes a massive difference when drawing 1000+ circles (orbiters, oscillators).

### WebGL Fullscreen Triangle

One triangle covers the entire viewport (cheaper than a quad):

```javascript
gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([-1,-1, 3,-1, -1,3]), gl.STATIC_DRAW);
gl.drawArrays(gl.TRIANGLES, 0, 3);
```

The oversized triangle gets clipped to the viewport. Avoids the diagonal seam of a two-triangle quad.

---

## Lessons Learned

### Bugs We Hit

**DPR mismatch** – forgetting to call `ctx.setTransform(dpr, 0, 0, dpr, 0, 0)` after resize makes mouse coordinates wrong. The canvas is in device pixels but your event handlers are in CSS pixels. Always apply the DPR transform.

**Animation jumps on tab switch** – `requestAnimationFrame` pauses when the tab is hidden. When you come back, the timestamp jumps by however long you were away. Fix: cap the delta time.

```javascript
const dt = Math.min((t - lastT) / 1000, 0.05);
```

**WebGL texture not rendering** – forgetting `gl.texParameteri` for `CLAMP_TO_EDGE` and `NEAREST` filtering on float textures. WebGL defaults to `REPEAT` and `LINEAR`, which don't work with float textures.

**Scroll prevention** – `addEventListener('wheel', ..., { passive: false })` is required to call `e.preventDefault()`. Without the `passive: false` option, the browser ignores the `preventDefault()` and scrolls the page anyway.

**Canvas toDataURL on WebGL** – needs `preserveDrawingBuffer: true` in the context options, or the screenshot is blank. The GPU clears the buffer after compositing.

### Things to Avoid

**Mouse hijacking** – making the cursor position directly control the simulation center or camera target. The experiment should look good without any mouse input. Mouse should enhance, not drive.

**Too many parameters** – if you need more than 6 sliders, the experiment is probably trying to do too much. Split it into two experiments, or find the 3 parameters that actually matter.

**Confusing labels** – "explore" beats "preset_lerp_index." Name sliders by feel, not implementation. "glow" not "density_decay_multiplier." "speed" not "dt_scale_factor."

**Linear animations** – always use easing. Even a simple `sin` oscillation is better than linear interpolation. For DOM animations: `cubic-bezier(0.34, 1.56, 0.64, 1)` for transforms, `cubic-bezier(0.4, 0, 0.2, 1)` for opacity.

**Forgetting the hint text** – every control panel should have a `.hint` div at the bottom explaining what to do. "hover: highlight spiral arm · click: pause" – short, scannable, discoverable.

### Patterns That Always Work

- **Distance-based phase offset** – any grid where phase = f(distance from center) produces waves
- **Accumulation over time** – let density build up instead of clearing each frame
- **Sine + cosine for orbits** – `x = r·cos(θ), y = r·sin(θ)` never gets old when you offset the phase
- **Noise as variation** – add simplex noise to any regular structure to make it organic
- **Color from position** – map x, y, or distance to hue for instant visual richness
