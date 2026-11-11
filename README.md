# hockey-vr
Quest 3 AR Stick Handling Game


**What it does
**
Passthrough: it requests immersive-ar with the local-floor reference space, so Y = 0 is your real floor. The renderer clears to transparent, so you see your tiles.
Obstacles: red cylinder defenders (with a head), orange pylons and red/white block barriers spawn 4 m ahead at floor level. They slide toward your feet and are removed just behind you.
Lanes: each obstacle is randomly Left, Middle or Right (±0.6 m). The code makes it a bit less likely to repeat the same lane back to back.
Floor guides: faint, semi-transparent lane strips and a ring at your feet show where the lanes are.
Panel: a floating panel sits about 1 m ahead near eye level, with:
a timer
Start/Pause/Resume
Speed − and + (levels 1–10)
Reset
Recenter
a “passed” counter
Pointing: aim a controller ray at the panel and pull the trigger. Hand pinch also works, because hand tracking is requested as an optional feature.
Anchoring: the whole play area anchors to where you stand and face when you enter. If you move or turn, hit Recenter.

Tuning
Everything adjustable is in the CONFIG object at the top of the script: spawn distance, lane offsets, base speed and speed per level, spawn interval, and panel size and distance. Speed is baseSpeed + level × speedStep, so the default runs from about 1.0 to 3.7 m/s.

Obstacles currently only pass through you, with no collision or scoring. I can add a feet-zone hit check with a flash and haptic buzz, or a hockey glove obstacle, if you want them.
