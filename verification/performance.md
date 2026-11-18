# Stratos performance and verification

## Current spectator controls

The current 151,693-byte build adds ground camera movement, adjustable eye height, Follow Jet and Recenter controls. Chrome 157 on the RTX 4050 Laptop GPU passed the movement, follow/fixed, height, pause cleanup, orbit restoration, and smoke-loop checks at 2560 × 1440. The new capture is in `spectator-controls.png`.

Current SHA-256 `cb697d2bae4ec0c4b2b9ebe9f36dac4a52b3ba04eb92ed512e0390176fa89792`

The timing results below cover the preceding ground-camera build.

## Measured build

**148,183 bytes · 148.18 KB · 144.71 KiB**, minified and uncompressed. The full simulation is contained in `index.html`.

SHA-256 `e7ce483e65eb9fd94067e0b0deb42e5a8b931cd67c6c9b36b751c5eb546b4f49`

## Ground camera

Select **Airshow Practice** and press **Start Flight**. Smoke starts enabled. Press **1** or **2** for a roll, **3** for the inside loop, or **4** for the Immelmann. **T** switches between the fixed ground camera and the previous view. Scroll to zoom, and press **Shift+T** to choose a new ground position. **R** restarts practice from the original lookout.

Chrome 157 opened the build directly with hardware WebGPU at 2560 × 1440. The camera stayed 1.72 m above the same point of terrain throughout the inside loop. The jet's center remained in frame at all 24 sampled positions. Checks also covered the left roll with smoke, zoom, returning from orbit, camera cycling, relocation, entering ground view from free flight, and clearing the camera override on cinematic replay. The frame in `ground-airshow.png` shows the inside loop from the lookout.

## 60-second native benchmark

| Setting | Measured run |
| --- | --- |
| OS | Windows 11 26H2, build 26300.9974 |
| Browser | Chrome/157.0.8103.79, hardware-accelerated headless |
| GPU | NVIDIA GeForce RTX 4050 Laptop GPU, driver 617.14 |
| CPU | Intel Core i7-13650HX |
| Render target | 2560 × 1440, Ultra |
| Configuration changed during run | No |
| Average frame rate | 59.65 FPS |
| Peak JavaScript heap | 20.15 MiB (21,132,617 bytes) |

| Measurement | Samples | Mean | p99 | Maximum |
| --- | ---: | ---: | ---: | ---: |
| GPU scene time | 3579 | 6.06 ms | 10.94 ms | 12.52 ms |
| CPU frame work | 3579 | 0.72 ms | 3.20 ms | 11.90 ms |
| Browser frame interval | 3578 | 16.76 ms | 17.30 ms | 233.40 ms |

The cinematic route met the 11 ms mean and 16.7 ms maximum GPU limits on this laptop. Browser frame intervals exceeded 16.7 ms on 1,023 samples. The longest interval occurred 7.88 seconds into the route.

The opening scene warmed up for 1.5 seconds at native resolution. Ultra renders the scene natively and composites the cloud volume from an internal 1280 × 720 buffer. GPU timestamp queries bracketed the cloud pass through the final scene pass. CPU time covered animation-callback work through command submission. Frame intervals measured time between callbacks. Timing applies to the standard cinematic, with the ground camera and user-triggered smoke inactive. Peak GPU and whole-process memory were unavailable.

**Requested hardware gate remains unverified.** The specified RTX 5070 Ti, Ryzen 7800X3D, Windows 11 25H2, and 180 Hz display were unavailable. The independent visual review of the cinematic and aerobatics still found moderate terrain defects.

## Reproduce

Open `index.html` in hardware-accelerated Chrome. Set **Ultra · Native** and fullscreen at 2560 × 1440. Open DevTools undocked and run `await stratos.benchmark()`, then return focus to the flight window. Confirm the reported resolution and quality. Press **I** for the live overlay.

If your browser restricts WebGPU on local files, run this from the folder containing `index.html` with Node.js and open [localhost port 8000](http://127.0.0.1:8000).

```powershell
node -e "require('node:http').createServer((req,res)=>{res.setHeader('Content-Type','text/html; charset=utf-8');require('node:fs').createReadStream('index.html').pipe(res)}).listen(8000,'127.0.0.1')"
```
