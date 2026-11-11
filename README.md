# 🏒 Stickhandling MR

A mixed-reality hockey stickhandling trainer for the **Meta Quest 3**, running entirely in the Quest Browser. Obstacles slide across your real floor toward your feet while you see your room through passthrough. Read them early, then stickhandle around them.

It is a single `index.html` file built with [Three.js](https://threejs.org/) and WebXR. There is no build step and nothing to install on the headset.

## Features

- **True mixed reality:** full-color passthrough, so you train on your own floor (`immersive-ar` session with a `local-floor` reference space).
- **6 obstacle types:** water bottles, pylons, sticks of dynamite, hockey skates, hockey gloves and mini nets.
- **3, 4 or 5 lanes:** pick the width of your training area.
- **4 difficulty modes:** Easy, Medium, Hard and Pro.
- **10 speed levels:** from about 1.0 m/s up to about 3.7 m/s.
- **Floating control panel:** start/pause, speed, lanes, difficulty, timer, reset and recenter, all at eye level.
- **Controllers or hands:** point and pull the trigger, or point and pinch with hand tracking.
- **Remembers your settings:** lanes, difficulty and speed level are saved between sessions.

## Requirements

- Meta Quest 3 or Quest 3S with the Meta Quest Browser
- The page served over **HTTPS** (GitHub Pages, Vercel and Netlify all work)
- A clear floor area. The play zone is about 4 m long by up to 2.75 m wide (5 lanes), plus space to move.

## Quick start

1. Open the hosted page in the Meta Quest Browser - https://levans902.github.io/hockey-vr/
2. Tap **Enter Mixed Reality** and allow the permission prompt.
3. Stand where you want to train and face the direction the obstacles should come from. The play area anchors to your position and facing when you enter.
4. Use a controller ray or a hand pinch on the floating panel to choose your settings, then press **START**.

## How to play

Obstacles spawn 4 m in front of you at floor level and slide toward your feet along the lanes. Faint blue strips on the floor show the lanes, and a white ring marks your spot. Carry the puck around the obstacles by reading them as they approach. The timer runs while you play, and the panel counts how many obstacles have passed you.

There is no collision scoring yet. It is a training tool, so judge your own clean passes.

## Control panel

| Control | What it does |
| --- | --- |
| **START / PAUSE / RESUME** | Starts, freezes or continues the session. Obstacles freeze while paused. |
| **− SPEED / SPEED +** | Changes the level from 1 to 10. |
| **3 / 4 / 5 LANES** | Sets the number of lanes. This clears the floor. |
| **EASY / MEDIUM / HARD / PRO** | Sets how obstacles are laid out (see below). |
| **RESET** | Stops the session and clears the timer, count and floor. |
| **RECENTER** | Re-anchors the play area and panel to where you are standing and facing. |

## Difficulty modes

| Mode | Behavior |
| --- | --- |
| **Easy** | One obstacle, in one random lane, per spawn. |
| **Medium** | About half the lanes are filled in each wave. The open gap drifts gradually. |
| **Hard** | Most lanes are filled, but never all. The open lane wanders unpredictably, wave timing varies and objects are offset front to back. |
| **Pro** | No waves. Single obstacles appear at random times in random lanes, like a scattered obstacle field. |

Medium, Hard and Pro always keep a path open, so every layout can be stickhandled by a good player. In Pro, a hidden open lane never gets obstacles. It can only shift one lane at a time, and always leaves at least 0.7 seconds to move over.

## Obstacles

Each spawn picks one of these at random:

- **Water bottle:** clear blue bottle with a label and an orange nozzle
- **Pylon:** classic orange training cone
- **Dynamite:** red stick with a "TNT" label and a lit fuse
- **Hockey skates:** a pair with steel blades
- **Hockey gloves:** a pair lying flat on the floor
- **Mini net:** a red-framed net with translucent netting

## Speed levels

Speed is `0.7 + level × 0.3` metres per second, so level 1 is 1.0 m/s and level 10 is 3.7 m/s. Higher levels also shorten the time between spawns.

## Deploying

Because it is a single static file, any static host works.

**GitHub Pages:** push `index.html` to a repo, then enable Pages under *Settings → Pages* and open the published URL on your Quest.

**Vercel / Netlify:** import the repo and deploy with no build command. The output is the repo root.

Three.js loads from the jsDelivr CDN through an import map, so the headset needs internet access the first time the page loads.

## Customizing

Everything adjustable is in the `CONFIG` object near the top of the script in `index.html`:

| Setting | Purpose |
| --- | --- |
| `spawnDistance` | How far ahead obstacles appear, in metres. |
| `laneSpacing` | Distance between lane centres. |
| `baseSpeed`, `speedStep` | Speed at each level. |
| `spawnIntervalBase`, `spawnIntervalPerLevel`, `spawnIntervalMin` | Time between spawns. |
| `startLevel`, `startLanes`, `startDifficulty` | Defaults on first launch. |
| `hardIntervalJitter`, `hardDepthJitter` | How irregular Hard feels. |
| `proExtra`, `proIntervalJitter`, `proMinDepthGap`, `proShiftTime`, `proShiftChance` | Pro density and fairness. A smaller `proShiftTime` is harder. |
| `panelDistance`, `panelWidth`, `panelHeightOffset` | Size and position of the control panel. |

## Troubleshooting

- **"WebXR not available":** open the page over HTTPS in the Meta Quest Browser, not a desktop browser.
- **No passthrough:** make sure passthrough is enabled in your Quest settings, and enter with the button on the page.
- **Panel or lanes are in the wrong place:** press **RECENTER** while standing where you want to train.
- **Panel too high or low:** adjust `panelHeightOffset` in `CONFIG`.
- **Can't press panel buttons:** aim the controller ray (or pinch ray) at the button until it highlights, then pull the trigger or pinch.

## Tech notes

- Three.js 0.160 (ES module via import map)
- WebXR Device API, `immersive-ar`, `local-floor`, optional `hand-tracking`
- The control panel is a canvas texture on a plane, with ray-picking from the XR controllers
- Obstacle models are built from Three.js primitives, so there are no external assets
- Pixel ratio is fixed at 1 with fixed foveation, to keep a steady frame rate on Quest

## License

Add your license of choice here.
