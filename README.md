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
| **Heads Up!** | Stickhandling a wiggling zig-zag training aid while ducking cannonballs from a French bulldog. |
| **The Floor Is Lava** | Keeping your puck on a winding path that slides toward you across a lane of lava. |
| **Dog Attack** | A static level: stickhandling around little animals (French bulldogs, sharks or T-rexes) wandering about in a small patch of floor. |

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

The guaranteed route through the clutter zig-zags across the lane and is kept narrow, and a guard watches every 0.35 m strip of the lane, adding a filler object whenever a strip has been empty too long. At the default density the longest empty stretch is about 3 to 8 m, instead of 40 to 50 m before, so there is no hiding in the middle.

One lane, as wide as three treadmill lanes (1.65 m), packed with objects of every size. Instead of switching lanes, you have to work through the clutter with toe drags and fancy handles.

- **Big and odd shapes:** Insanity uses the treadmill objects except the dynamite, and adds hockey sticks lying flat at all sorts of angles (mostly diagonal or across the lane), a goalie stick, a crossed pair of sticks, two kinds of hockey bag, a goalie pad, a bucket of pucks, a helmet, a wide goal net, a low team bench and an ice resurfacer that fills one whole half of the lane. A puck can't slide over a flat stick, so these force wider moves, lifts and toe drags instead of just dangling around thin objects. Every object has a footprint (a line plus a radius) that the generator keeps the gap around, so long objects block whole strips of the lane and the gaps vary a lot in size and shape.
- **Density 1 to 10:** density 1 is a sparse scatter with wide gaps. At density 10 neighbouring objects are only about 20 cm apart.
- **Always passable:** every new object is checked so that a route through the lane still exists. It can twist and turn, and at the highest densities it is tight.
- **Speed:** levels 1 to 10, the same speeds as the treadmill.

### Heads Up!

An endless zig-zag stickhandling aid slides down the middle lane toward you: black pods joined by rods, like a real training aid. Its shape slowly breathes between the sharp zig-zag from the product photo and almost dead straight, with a small ripple from pod to pod, so you keep adjusting your hands.

At the far end of the lane a French bulldog with a cannon strapped to its back wanders a little left, right and back and forth, with the odd hop, wagging its tail and twitching its ears. Every so often it plants its feet, barks, and the fuse on the cannon glows while the barrel swings to your head. Then it fires. Duck under the ball while you keep stickhandling.

- **Hit detection:** the ball is aimed at your head height (measured when you enter or press RECENTER, so recenter while standing normally). A ball that passes within about 27 cm of the headset counts as a hit, so duck roughly 30 cm. A hit tints your view red for about a second.
- **Warning:** each shot is telegraphed by a bark and a glowing fuse, and the warning gets shorter at higher speed levels.
- **Speed 1 to 10:** sets how fast the training aid slides toward you and how fast the cannonballs fly (3.1 m/s at level 1, 5.8 m/s at level 10).
- **Shots 1 to 10:** the shot volume. Level 1 is a shot about every 5 s. Level 10 is a shot about every 1.4 s, and from level 5 up the dog sometimes fires bursts of 2 or 3 balls.
- **Score:** the panel counts balls you dodged and balls that hit you.
- **Sound:** a synthesized bark, cannon boom and thud. Turn it off with `headsUp.sound`.

### The Floor Is Lava

One continuous lane of glowing lava, 3.2 m wide at 100% playspace, with a safe path winding through it. The path slides toward you at the chosen speed, so you keep stickhandling your real puck sideways to stay on it while it bends left and right. The path is 0.85 to 1.1 m wide depending on difficulty, which leaves room for real stickhandling. The lava is drawn only beside the path, not under it, and the path itself is almost clear with bright edges and a faint dashed centre line, so your puck stays easy to see on it. Lava drifts along with the path so you can feel the speed.

A thin white line across the lane marks where the game assumes your real puck is (the same 0.55 m in front of you that Keep Away uses). Watch the path where it crosses that line. The game can't see your puck, so you judge whether you stayed on the path yourself, like the other modes. The panel counts the distance you have travelled along the path.

**PLAYSPACE − / +** (50% to 150%, steps of 10%) scales the lava's width and how far ahead it reaches, so the whole thing fits your room, and the path never leaves the lava. Below 100% the path itself narrows slightly (to 80% of its width at 50%) so it can still wander. It never gets wider than the values below.

| Difficulty | Path |
| --- | --- |
| **Easy** | Straight-ish. Long, gentle drifts left and right about half a metre either way, so you still need to move your hands. The widest path (1.10 m). |
| **Medium** | Clear, regular bends about 0.65 m either way, with some S-bends (1.00 m wide). |
| **Hard** | Frequent, sharper bends up to 0.8 m either way and plenty of S-bends (0.92 m wide). |
| **Pro** | Lots of turns and twists, up to 0.9 m either way, often swinging straight into the opposite direction. The narrowest path (0.85 m). |

Speed uses levels 1 to 10, the same speeds as the treadmill (1.0 to 3.7 m/s). The path is shaped so it never bends tighter than its own width, and the sideways speed it asks of your hands is capped for each difficulty. At high speed levels the bends are therefore gentler but come much more often.

### Dog Attack

A static level: nothing slides toward you. A rectangle on the floor, marked with a faint green fill and a bright border, holds a handful of French bulldogs that wander around inside it. They walk in random directions, change direction at random, sometimes stop for a sniff, turn away from the border and steer around each other, so there is always something moving that you have to stickhandle around. They are about as long as an adult sneaker (0.3 m). Each has its own coat colour, and they never overlap.

The rectangle starts 3 ft in front of you and reaches 3 ft to your left, 3 ft to your right, and 3 ft ahead of its near edge (6 ft wide by 3 ft deep).

- **PLAYSPACE − / +:** scales the whole rectangle, including how far in front of you it starts, from 50% to 200% in steps of 10%. The animals stay the same size. A small playspace can't hold as many, so the count drops to what fits, and the panel shows the count in use.
- **SHIFT ◀ / ▶:** slides the whole play area left or right in 0.1 m steps (up to 1.5 m each way), so it lines up with where you actually stand. It also exists in The Floor Is Lava. The panel shows how far it is shifted in feet.
- **DENSITY − / +:** 1 to 10, animals per square metre. The count grows with the playspace size, capped at what physically fits.
- **ANIMAL ◀ / ▶:** French bulldog, shark or T-rex. Sharks glide with a swishing tail, T-rexes stomp on two legs. All are about the size of a sneaker.
- **Speed 1 to 10:** how fast the dogs walk, 0.3 to 1.1 m/s.
- **EASY / MEDIUM / HARD / PRO:** 4, 6, 8 or 11 dogs, changing direction more often and stopping less as you go up.

## Objects

Each object is built from Three.js shapes, so there are no external assets.

- **Water bottle:** clear blue bottle with a label and an orange nozzle
- **Pylon:** classic orange training cone
- **Dynamite:** red stick with a "TNT" label and a lit fuse
- **Hockey skates:** a pair with steel blades
- **Hockey gloves:** a pair lying flat on the floor
- **Mini net:** a red-framed net with translucent netting

The Treadmill uses all six. Insanity leaves out the dynamite and the tall, thin objects (bottle and pylon) turn up much less often there, so you can't just sit in a gap between them. It adds eleven bigger, wider ones:

- **Hockey stick** (two sizes, two colours): lying flat, mostly at diagonals across the lane
- **Goalie stick:** long shaft with a wide paddle
- **Crossed sticks:** two sticks lying across each other
- **Equipment bag:** a big duffel
- **Goalie leg pad:** long and flat
- **Bucket of pucks**
- **Helmet**
- **Wide net:** a 1.1 m wide red-framed goal net
- **Team bench:** a low, solid bench 1.2 m long
- **Ice resurfacer:** 1.5 m long and 0.84 m wide, so exactly half the lane, always on the left or the right half and usually pointing at you. It is the rarest object.

Keep Away uses full-size defencemen in red jerseys instead. Heads Up! uses a zig-zag aid of black pods and rods, a French bulldog and a cannon.

## Control panel

A floating panel sits about 1 m in front of you near eye level. Aim a controller ray at it and pull the trigger, or point and pinch with hand tracking.

| Control | What it does |
| --- | --- |
| **◀ ▶** | Switches game mode. |
| **START / PAUSE / RESUME** | Starts, freezes or continues the session. Everything freezes while paused. |
| **− SPEED / SPEED +** | Sets the speed level, 1 to 10, for the current mode. |
| **3 / 4 / 5 LANES** | Treadmill only: number of lanes. |
| **EASY / MEDIUM / HARD / PRO** | Treadmill, Keep Away and The Floor Is Lava: layout, defender count or how twisty the path is. |
| **DENSITY − / +** | Insanity only: clutter level, 1 to 10. |
| **PLAYSPACE − / +** | Dog Attack and The Floor Is Lava: scales the play area. |
| **SHIFT ◀ / ▶** | Dog Attack and The Floor Is Lava: slides the play area left or right. |
| **DENSITY − / +** (Dog Attack) | How many animals, 1 to 10. |
| **ANIMAL ◀ / ▶** | Dog Attack: dog, shark or T-rex. |
| **SHOTS − / +** | Heads Up! only: cannon shot volume, 1 to 10. |
| **RESET** | Stops the session and clears the timer, counts and floor. |
| **MENU HOME** | Puts the panel back in its default spot after you have dragged it. |
| **RECENTER** | Re-anchors the play area to where you are standing and facing. The panel keeps its position relative to you, including a spot you dragged it to. |

**Moving the panel:** aim at the empty background of the panel (not a button), hold the trigger or pinch, and move your hand. The panel follows your ray, always turns to face you, and the border turns yellow while you are moving it. Let go to drop it, for example down by your feet or off to the side so it is out of the way of the cannon in Heads Up!. It stays within about 3 m of you, and the spot is saved on the headset between sessions. Presses that start on a button still work as normal buttons.

The panel also shows a timer, the level and speed, and either how many objects have passed you or how many attacks have been made. Your last mode, lanes, difficulty, speed levels and density are saved on the headset between sessions.

## Speeds

| Mode | Speed at level 1 | Speed at level 10 |
| --- | --- | --- |
| **Treadmill / Insanity** | 1.0 m/s | 3.7 m/s |
| **Keep Away** (lunge speed) | 1.4 m/s | 3.7 m/s |
| **Dog Attack** (dogs walking) | 0.3 m/s | 1.1 m/s |
| **Heads Up!** (training aid) | 1.0 m/s | 3.7 m/s |
| **The Floor Is Lava** (path) | 1.0 m/s | 3.7 m/s |

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
| `insanity.gapMax`, `gapMin`, `pathClear`, `pathSlope` | Insanity: clear space between objects at density 1 and 10, the room the route through the clutter must leave for your puck, and how sharply that route may turn. |
| `insanity.openMaxLow`, `openMaxHigh`, `guardGap`, `stripW`, `pathMinHalf` | Insanity's open-strip guard: the longest stretch (m) any 0.35 m strip of the lane may stay empty at density 1 and 10, how tight the filler objects may sit, and how narrow the guaranteed route is. |
| `keepAway.defenderScale` | How big the defenders look (1.0 is full size). |
| `keepAway.puckOffset` | Where the game assumes your puck is in front of you. |
| `keepAway.maxRadius`, `attackGap`, `perDifficulty` | Zone size, spacing between attacks, and each difficulty's defender count and aggression. |
| `headsUp.aidSpacing`, `aidAmplitude`, `aidPeriod`, `aidPhasePerPod` | Heads Up!: gap between pods, how far they swing sideways at full zig-zag (0 is straight), seconds per breathing cycle, and how much the shape ripples. |
| `headsUp.dogDistance`, `dogScale`, `dogRangeX`, `dogRangeZ`, `dogSpeed` | Heads Up!: how far away the bulldog is, how big it looks, and how much and how fast it wanders. |
| `headsUp.ballRadius`, `ballSpeedBase`, `ballSpeedStep`, `arcHeight`, `hitRadius`, `aimNoise` | Heads Up!: cannonball size, speed, how much it lobs, how close counts as a hit, and shot inaccuracy. |
| `lava.lavaWidth`, `startStraight`, `puckLine`, `pathFill` | The Floor Is Lava: width of the lava, how long the path is straight at the start, whether the puck line is shown, and how solid the path looks (0 is clear, 1 is solid slate; the bright edges always show). |
| `dogAttack.startDist`, `halfWidth`, `depth`, `scaleMin`, `scaleMax` | Dog Attack: where the play area starts, how far it reaches sideways and ahead (all 3 ft by default), and the PLAYSPACE range. |
| `dogAttack.sizes`, `densMin`, `densMax`, `shiftMax`, `shiftStep`, `sepDist`, `turnRate`, `baseSpeed`, `speedStep`, `perDifficulty` | Dog Attack: how big each animal looks, the animals per m² at density 1 and 10, the shift limits and step, , how much room they keep, how fast they turn and walk, and how each difficulty changes how often they change direction, turn sharply and stop. |
| `lava.scaleMin`, `scaleMax`, `shiftMax`, `shiftStep`, `edgeMargin` | The Floor Is Lava: PLAYSPACE range, shift limit and step and how far inside the lava the path stays. |
| `lava.perDifficulty` | The Floor Is Lava: for each difficulty, `width` of the path, `sMax` (steepest bend), `turnMin` / `turnMax` (distance between bends), `aMax` (how sharp a bend can be), `xMax` (how far it wanders) and `latMax` (the most sideways speed it can ask of you). |
| `headsUp.telegraphBase`, `intervalMax`, `intervalMin`, `burstChanceMax` | Heads Up!: warning time before a shot, time between shots at shots 1 and 10, and how often bursts happen. |
| `headsUp.tintPeak`, `tintFade` | Heads Up!: strength of the red hit tint (0 to 1) and how long it takes to fade. |
| `panelScale`, `panelDistance`, `panelWidth`, `panelHeightOffset` | Size and position of the control panel. `panelScale` (1.25 by default) makes the whole menu bigger while the text stays the same size; set it to 1 for the old size. |

## Troubleshooting

- **"WebXR not available":** open the page over HTTPS in the Meta Quest Browser, not a desktop browser.
- **No passthrough:** make sure passthrough is enabled in your Quest settings, and enter with the button on the page.
- **Panel or play area in the wrong place:** press **RECENTER** while standing where you want to train. If you dragged the panel somewhere awkward, press **MENU HOME**.
- **Panel in the way:** grab its background and drag it somewhere else.
- **Dog Attack or Floor Is Lava runs outside your room:** use **PLAYSPACE −** until the area fits.
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
