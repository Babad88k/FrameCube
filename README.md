# Frame Cube

Turn a short video into a 3D spacetime cube.

Each frame is an **X–Y** image. The next frame steps along **Z** (time). Play the clip and earlier frames stay in the volume, fading instead of disappearing.

A sample reel loads on start so you can orbit the cube immediately. Drop in your own clip when you want.

![Slices view — stacked video frames along the time axis](docs/slices.png)

![Volume view — pixels as a point cloud](docs/volume.png)

## Features

- **Slices** — stacked frames as translucent planes
- **Volume** — every pixel as a point in the cube; dark pixels can be cut away
- **Play / scrub** — the current frame is bright; past frames stay visible and fade
- **Spread** — pull the time axis apart
- **Trail** — how quickly past frames fade
- **Future** — show or hide frames that have not played yet
- **Export** — download a PNG sprite sheet of every extracted frame
- **Upload** — MP4, WebM, or MOV, first **5 seconds** only

Drag to orbit. Scroll to zoom. Drop a file onto the page to load it.

## Getting started

You need **[Node.js 22+](https://nodejs.org/)**.

```bash
git clone https://github.com/<you>/frame-cube.git
cd frame-cube
npm install --legacy-peer-deps
npm run dev
```

Open [http://localhost:8080](http://localhost:8080).

`--legacy-peer-deps` is required because React Three Fiber pins an older React 19 range than this project uses.

Stop the server with `Ctrl+C`.

### Production build

```bash
npm run build
npm run preview
```

No account or database. Frame extraction and the cube both run in the browser.

## Keyboard

| Key | Action |
| --- | --- |
| Space | Play / pause |
| ← → | Step one frame |
| Home / End | Jump to first / last frame |
| V | Toggle slices / volume |

## How the cube is built

1. The video is sampled at **12 fps**, capped at **5 seconds** (~60 frames).
2. Each frame is scaled so the long side is **128 px**.
3. Frames are placed as X–Y slices along Z.
4. While playing, opacity falls off behind the playhead so the history remains as a trail.

**X** = frame width · **Y** = frame height · **Z** = time

## Stack

- React 19 + TypeScript
- [TanStack Start](https://tanstack.com/start)
- [Three.js](https://threejs.org/) via [React Three Fiber](https://r3f.docs.pmnd.rs/)
- Tailwind CSS v4
- Zustand

## Limits

| | |
| --- | --- |
| Max duration | 5 seconds (longer files use the first 5) |
| Max upload | 80 MB |
| Formats | MP4, WebM, MOV, and other `video/*` types the browser can decode |
