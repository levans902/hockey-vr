# 🏒 SickMitts VR

A mixed-reality hockey stickhandling trainer for the **Meta Quest 3**, running entirely in the Quest Browser. You see your real floor through passthrough, keep using your **real puck on your hockey pad**, and the game adds virtual obstacles and defenders around you. There is no virtual puck.

The whole game is a single `index.html` built with [Three.js](https://threejs.org/) and WebXR. There is no build step and nothing to install on the headset.

## Game modes

Use the ◀ ▶ arrows at the top of the floating panel to switch modes. Each mode remembers its own speed setting.

| Mode | What it trains |
| --- | --- |
| **Endless Object Treadmill** (default) | Reading objects early and stickhandling around them across several lanes. |
| **Keep Away** | Protecting the puck from opposing defencemen who skate around you and attack. |
| **Insanity** | Toe drags and tight, fancy hands through dense clutter in one wide lane. |

### Endless Object Treadmill

Objects spawn 4 m in front of you at floor level and slide along the floor toward your feet.

- **Lanes:** choose 3, 4 or 5 lanes. Faint blue strips on the floor show them, and a white ring marks your spot.
- **Difficulty** controls how objects are laid out:

| Difficulty | Behavior |
| --- | --- |
| **Easy** | One object, in one random lane, per spawn. |
| **Medium** | About half the lanes are filled in each wave. The open gap drifts gradually. |
| **Hard** | Most lanes are filled but never all. The open lane wanders unpredictably, and wave timing and depth are jittered. |
| **Pro** | No waves. Single objects appear at random times in random lanes, like a scattered obstacle field. |

Medium, Hard and Pro always keep a path open, so every layout can be stickhandled by a good player. In Pro, a hidden open lane never gets objects. It must move after a short time, and any lane left empty for too long gets the next object, so standing in one lane doesn't work.

### Keep Away

Opposing defencemen skate around you in the zone in front of and beside you, never behind. They always face you and skate forwards, backwards and sideways. At random times they set up, lunge at where your puck is, swing their stick, then back off and reset.

| Difficulty | Defenders | Extras |
| --- | --- | --- |
| **Easy** | 1 | One attack at a time. |
| **Medium** | 2 | One attack at a time. |
| **Hard** | 3 | Up to two attacks at once, with occasional fake lunges. |
| **Pro** | 4 | Up to two attacks at once, with more fake lunges and a tighter zone. |

- **Zone:** a faint half-circle on the floor, 3.2 m out, marks the area in front of and beside you.
- **Personal space:** defenders never come closer than about 0.75 m to your body.
- **Puck position:** the game assumes your real puck is about 0.55 m in front of you.
- **Speed:** levels 1 to 10 set both the skating and lunge speed, and shorten the wait between attacks at higher levels.
- There is no hit detection. The defenders can't actually take your puck, so it is a training aid rather than a scored game.

### Insanity

One lane, as wide as three treadmill lanes (1.65 m), packed with the same objects. Instead of switching lanes, you have to work through the clutter with toe drags and fancy handles.

- **Density 1 to 10:** density 1 is a sparse scatter with wide gaps. Density 10 is about four objects per metre of lane with only about 20 cm between neighbours.
- **Always passable:** a hidden open path winds slowly through the clutter, so there is always a way through, even at density 10.
- **Speed:** levels 1 to 10, the same speeds as the treadmill.

## Objects

Each object is built from Three.js shapes, so there are no external assets.

- **Water bottle:** clear blue bottle with a label and an orange nozzle
- **Pylon:** classic orange training cone
- **Dynamite:** red stick with a "TNT" label and a lit fuse
- **Hockey skates:** a pair with steel blades
- **Hockey gloves:** a pair lying flat on the floor
- **Mini net:** a red-framed net with translucent netting

Both the Treadmill and Insanity use all six. Keep Away uses full-size defencemen in red jerseys instead.

## Control panel

A floating panel sits about 1 m in front of you near eye level. Aim a controller ray at it and pull the trigger, or point and pinch with hand tracking.

| Control | What it does |
| --- | --- |
| **◀ ▶** | Switches game mode. |
| **START / PAUSE / RESUME** | Starts, freezes or continues the session. Everything freezes while paused. |
| **− SPEED / SPEED +** | Sets the speed level, 1 to 10, for the current mode. |
| **3 / 4 / 5 LANES** | Treadmill only: number of lanes. |
| **EASY / MEDIUM / HARD / PRO** | Treadmill and Keep Away: layout or defender count. |
| **DENSITY − / +** | Insanity only: clutter level, 1 to 10. |
| **RESET** | Stops the session and clears the timer, counts and floor. |
| **RECENTER** | Re-anchors the play area and panel to where you are standing and facing. |

The panel also shows a timer, the level and speed, and either how many objects have passed you or how many attacks have been made. Your last mode, lanes, difficulty, speed levels and density are saved on the headset between sessions.

## Speeds

| Mode | Speed at level 1 | Speed at level 10 |
| --- | --- | --- |
| **Treadmill / Insanity** | 1.0 m/s | 3.7 m/s |
| **Keep Away** (lunge speed) | 1.4 m/s | 3.7 m/s |

## Requirements

- Meta Quest 3 or Quest 3S with the Meta Quest Browser
- The page served over **HTTPS** (GitHub Pages, Vercel and Netlify all work)
- A clear floor area: about 4 m deep in front of you, and up to about 2.75 m wide with 5 lanes. Keep Away uses a zone about 3.2 m out.

## Quick start

1. Open the hosted page in the Meta Quest Browser.
2. Tap **Enter Mixed Reality** and allow the permission prompt.
3. Stand where you want to train and face the direction things should come from. The play area anchors to your position and facing when you enter.
4. Pick a game with the arrows, adjust the settings, then press **START**.
5. Stickhandle your real puck on your pad.

## Files

Put all of these in the same folder:

| File | Purpose |
| --- | --- |
| `index.html` | The whole game. |
| `manifest.webmanifest` | App name, colors and icons for a home-screen shortcut. |
| `icon-192.png`, `icon-512.png` | Shortcut / app icons. |
| `apple-touch-icon.png` | Touch icon (180 × 180). |
| `favicon-48.png` | Browser tab icon. |

## Deploying

Because it is a static site, any static host works.

**GitHub Pages:** push the files to a repo, then enable Pages under *Settings → Pages* and open the published URL on your Quest.

**Vercel / Netlify:** import the repo and deploy with no build command. The output is the repo root.

Three.js loads from the jsDelivr CDN through an import map, so the headset needs internet access the first time the page loads.

## Customizing

Everything adjustable is in the `CONFIG` object near the top of the script in `index.html`.

| Setting | Purpose |
| --- | --- |
| `spawnDistance`, `laneSpacing` | How far ahead objects appear, and the space between lanes. |
| `baseSpeed`, `speedStep` | Treadmill and Insanity speed at each level. |
| `spawnIntervalBase`, `spawnIntervalPerLevel`, `spawnIntervalMin` | Time between waves on the Treadmill. |
| `startLevel`, `startLanes`, `startDifficulty` | Defaults on first launch. |
| `hardIntervalJitter`, `hardDepthJitter` | How irregular Hard feels. |
| `proExtra`, `proIntervalJitter`, `proMinDepthGap`, `proShiftTime`, `proMaxSafeHold`, `proMaxEmpty` | Treadmill Pro density and fairness. A smaller `proShiftTime` is harder. |
| `insanity.targetMax`, `gapMin`, `pathSlope` | Insanity: objects at density 10, tightest gap, and how quickly the open path wanders. |
| `keepAway.defenderScale` | How big the defenders look (1.0 is full size). |
| `keepAway.puckOffset` | Where the game assumes your puck is in front of you. |
| `keepAway.maxRadius`, `attackGap`, `perDifficulty` | Zone size, spacing between attacks, and each difficulty's defender count and aggression. |
| `panelDistance`, `panelWidth`, `panelHeightOffset` | Size and position of the control panel. |

## Troubleshooting

- **"WebXR not available":** open the page over HTTPS in the Meta Quest Browser, not a desktop browser.
- **No passthrough:** make sure passthrough is enabled in your Quest settings, and enter with the button on the page.
- **Panel or play area in the wrong place:** press **RECENTER** while standing where you want to train.
- **Panel too high or low:** adjust `panelHeightOffset` in `CONFIG`.
- **Can't press panel buttons:** aim the controller or pinch ray at the button until it highlights, then pull the trigger or pinch.
- **Changes don't show up:** the Quest Browser caches pages heavily. Check the small `build` label on the start screen and at the bottom of the panel to see which copy you have, then clear the site data in the browser settings and reload.
- **Home-screen icon didn't update:** delete the old shortcut and create it again. Existing shortcuts tend to keep their old icon.

## Tech notes

- Three.js 0.160 (ES module via import map)
- WebXR Device API: `immersive-ar`, `local-floor`, optional `hand-tracking`
- The control panel is a canvas texture on a plane, with ray picking from the XR controllers
- Pixel ratio is fixed at 1 with fixed foveation, to keep a steady frame rate on Quest

## License

Add your license of choice here.
