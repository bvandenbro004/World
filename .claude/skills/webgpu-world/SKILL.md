---
name: webgpu-world
description: Engine conventions for the fantasy-continent project — constraints, code layout, performance rules, build and verification. Load before writing or reviewing any scene code.
---

# WebGPU world conventions

Inherited from Abyssal Garden (see `prompt.txt` and `README.md`); the underwater scene is the reference implementation, not the content.

## Constraints
- WebGPU + WGSL directly. No Three.js, Babylon or any other engine or library at runtime.
- Everything procedural: no images, models, audio or font files. Sound via Web Audio synthesis.
- Each playable region ships as **one self-contained HTML file** built from `source/`. Report the minified size.
- Zero per-frame JS allocations; preallocate every buffer.
- Low / Medium / High detail levels, adaptive resolution then draw distance; must still load on a phone on Low.

## Priorities when they conflict
1. Visual quality and fidelity to the region spec in `world/regions/`.
2. Stable frame pacing (target: ≤ 11 ms average GPU time, no frame > 16.7 ms at 2560×1440 on a desktop RTX-class GPU; tune to the user's hardware once known).
3. Small bundle size.

## Code layout (`source/src/`)
`world.js` layout, `shaders.js` look (WGSL), `main.js` renderer/camera/controls/viewpoints/camera path, `audio.js`, `quality.js`, `math.js` (noise, RNG, mesh helpers), `dev.js` (fly-through + benchmark, dev build only), `template.html` (page and menu).
Keep engine code (renderer, terrain/vegetation systems, quality, controls) separate from region content so later regions reuse the engine. Region content lives in its own module per region.

## Controls
WASD move, mouse look (pointer lock), Shift faster, Esc menu, `1`–`6` viewpoints, `H` stats, `M` sound. Walking with gravity on terrain by default; `F` toggles free flight (Q/E up/down) unless the region spec says otherwise. Touch support as in the original.

## Build
```
cd source && npm install && npm run build        # index.html
npm run build:dev                                 # dev.html: F = fly-through, B = benchmark
```

## Verification (every build)
1. Render the 6 viewpoints from the build spec in headless Chromium with WebGPU enabled (`/opt/pw-browsers/chromium`, flags `--enable-unsafe-webgpu --enable-features=Vulkan`) and save screenshots under the scratchpad.
2. Capture a short frame sequence along the fly-through for shimmer/popping.
3. Run the benchmark; report avg / p99 / max GPU frame time. Headless software GPU numbers are only indicative; say so.
4. Hand screenshots (not code) to `visual-critic`.
