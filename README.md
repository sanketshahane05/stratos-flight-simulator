# Stratos Flight Simulator

Stratos is a single-file WebGPU flight simulator with a procedural alpine coast, clouds, live cockpit instruments, multiplayer airshows, and a ground camera with movement and jet-following controls for watching aerobatics.

![A smoke loop seen from the ground lookout](verification/ground-airshow.png)

## Fly

[Play Stratos in your browser](https://sanketshahane05.github.io/stratos-flight-simulator/).

Download [index.html](index.html) and open it in a WebGPU-enabled browser. Chrome 157 was tested with hardware acceleration. Solo flight runs offline without installation, a build step, or external assets. Multiplayer rooms need an internet connection.

For a ground-level airshow, choose **Airshow Practice** and click **Start Flight**. Smoke and spectator following start on. Press **3** to watch a loop. The **Following jet** button anchors your viewpoint to the jet's horizontal movement. Toggle it for a fixed lookout, use the arrow keys to move, and press **Home** or **Recenter** to choose a clear position near the jet.

## Play on a phone

Open the live site in a WebGPU-capable mobile browser. Touch controls appear automatically: drag the left stick up to climb and sideways to roll, set the throttle with the slider, and hold Boost or Brake. The lower buttons switch cameras, toggle smoke, change its color, and open guided Tricks. Landing gear, pause, sound, and HUD controls are available without a keyboard.

Landscape gives a wider view. **Airshow Practice** starts at a clear ground lookout; the stick then moves the camera, with Height, Zoom, Follow, and Recenter controls for framing the jet. The pilots button opens multiplayer hosting, joining, and watching friends.

Phones start with **Low · Mobile** graphics and a capped render resolution. High and Ultra remain available in settings. WebGPU availability depends on the browser and device: use current Chrome on compatible Android devices, or Safari on iOS 26 or later. Older phones and in-app browsers may lack support. See the [mobile verification](verification/mobile.md) for tested layouts and limits; physical-phone performance has not been measured.

## Fly with friends

Click **Fly with friends**, enter a callsign, and choose **Host room**. Copy the invite link for your friends, or share the eight-character room code. A room supports four pilots, and everyone starts in the same procedural world with their own aircraft and smoke color.

Press **N** to open the room while flying. Choose **Watch** beside a pilot to track that aircraft from the ground. The arrow keys, height controls, Follow Jet toggle, and Recenter button work while watching another pilot.

The host's browser stays open for the session. Players exchange flight data over native WebRTC data channels at 20 Hz. PeerJS's public cloud provides room discovery, and the client uses its documented public STUN/TURN configuration for connection setup. Availability depends on those shared services and the players' networks. See the [multiplayer verification](verification/multiplayer.md) for the measured connectivity limits.

| Control | Action |
| --- | --- |
| Mouse, W/S, A/D | Pitch and roll, throttle, rudder |
| Shift, Space, G | Afterburner, air brake, landing gear |
| C, F, T | Cycle cameras, toggle orbit camera, toggle ground camera |
| Arrow keys | Move the spectator forward, backward, left, or right |
| PageUp, PageDown | Raise or lower the spectator above the terrain |
| L | Toggle following the jet and a fixed lookout |
| Scroll, Home, Shift+T | Zoom from ground view, recenter near the jet |
| B, V | Toggle smoke, cycle its color |
| 1, 2, 3, 4 | Left roll, right roll, inside loop, Immelmann |
| X, R, P | Cancel a maneuver, restart, pause |
| H, I, M | Toggle HUD, performance overlay, sound |
| N | Open the multiplayer room and pilot list |
| Esc | Release the mouse |

## Verification

[Watch the 60-second fly-through](verification/fly-through.mp4). See the [performance report](verification/performance.md), [raw benchmark](verification/benchmark.json), and [independent visual review](verification/visual-review.md) for the hardware and sampling details.

## Credits

Created by Sanket Shahane with [OpenAI Codex](https://github.com/codex).

Released under the [MIT License](LICENSE).
