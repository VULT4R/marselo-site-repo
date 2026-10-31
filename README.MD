# marselo.site

A one-page joke website about **Marselo**, a smiling grey ball with long legs and a
big mouth who is obsessed with Colgate. It has two parts: a talking Marselo on the
main page, and a physics playground called **combat mode** where you can do terrible
things to him (he always comes back).

Everything lives in a single `index.html` (HTML, CSS and JavaScript, no build step,
no libraries).

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site |
| `guy.png`, `sadguy.png`, `marselo-parts.png`, `marselopic.jpg` | Marselo's pictures and sprite parts |
| `break.mp3` | Sound played when Marselo finishes melting. Must be next to `index.html` |
| `updates.txt` | Update log, newest first |
| `README.MD` | This file |

To run it, open `index.html` in a browser, or host the folder on any static host.

## Main page

* Marselo talks back when you type to him (greetings, how are you, jokes, roasts,
  random thoughts) and says things on his own when you are idle ("chatty mode").
* Rainbow cursor trail.
* Voice settings: pick a voice, pitch and talk speed. The voice list contains your
  browser's own voices, Google voices (streamed online, same in every browser) and
  silly voices (chipmunk, giant, demon...).

## Combat mode

Pick a tool in the bar, then press **E** to spawn it facing right or **Q** to spawn
it facing left (at your cursor). Grab anything with the mouse.

### Controls

| Key | Action |
|---|---|
| E / Q | spawn the selected tool facing right / left |
| 1-9 | select a tool |
| F | use the held tool (fire, swing, spray, inject, cut) |
| A / D | lock the tool's angle and rotate it (until you let go) |
| Mouse wheel | rotate the held tool |
| X | delete the held tool |
| G | slow motion |
| I | invincible on / off |

Held tools hang and swing like real pendulums from the spot you grabbed them. Pressing
A or D freezes the swinging; let go and grab again to get the swinging back.

### Tools

* **Bat, glove, sword, ninja star, bomb, AK, flamethrower**: the classics. The sword can
  stab and stay stuck; flick the mouse fast to pull it out.
* **Chainsaw**: touch a body part while it runs and the part rips off. He bleeds for
  about 5 seconds and a blood pool forms and slowly fades.
* **Colgate**: sprays white paste with blue stripes.
* **Fire extinguisher**: puts Marselo out when he is on fire.
* **Acid syringe**: thrust the needle in, hold F. He melts down to his bones, then
  collapses into loose bones and respawns after 3 seconds (plays `break.mp3`).
* **Sleep syringe**: he sleeps for 60 seconds and ignores everything.
* **Laser cutter**: slices whatever the beam crosses into physics pieces that can be
  picked up, carried and sliced again. It never kills him; you can keep cutting him
  forever.

### Phone and touchscreen play

* On a phone the on-screen buttons show automatically: ◀ ▶ rotate, **F** use, **+◀ / +▶**
  spawn the selected tool facing left / right, and the bin deletes the held tool.
* Tap a tool to select it, or **drag it up out of the bar** to use it immediately.
* On a PC with a touchscreen, turn on **touchscreen mode** in the left panel.

### Maps and cars

* Left panel -> **map**: room, beach or city (your choice is remembered).
* On the **city** map a random car drives in from the right about every 30 seconds and
  flattens Marselo like a cartoon; he bounces back up after 3 seconds.
* The **spawn car** button (left panel) sends a car on any map. Spam it for traffic.
* Loose pieces on the floor can be picked up with the mouse (X deletes the held piece).

### Fruit Ninja mode

Open it from the **fruit ninja** button on the main page or the combat panel. Hold the
mouse button (or your finger) and swipe to slice the flying Marselo variants. You have
3 hearts, each Marselo that falls uncut costs one. The dark Marselo with a lit fuse is a
bomb: cutting him ends the game instantly. Golden Marselo is worth 5, slicing 3+ in one
swipe gives a combo bonus. The game is endless and gets harder; top 10 scores are saved
in the browser.

### Health, death, hits and skins

* He has a health bar. At zero he swells up, bursts and sprays Colgate, then respawns
  after 3 seconds. The **invincible** toggle keeps him alive.
* The **hit counter** survives the Reset button and page reloads (saved in the browser).
* Hits unlock skins: cowboy hat (100), cool shades / aviators (500), aloha shirt (1000), propeller
  beanie (2000), road work (3500), duck captain (5000), royal Marselo (7500).
  The skins panel shows all skins, locked ones dimmed.

### How it works (short)

* Marselo is a verlet-physics ragdoll: a big round head plus eight limb bones joined by
  distance constraints, drawn from sprite parts.
* Tools are rigid bodies; the grab point is pinned to the mouse by a velocity constraint,
  so everything swings naturally.
* Stuck swords and needles use a point-on-line constraint between the tool and the
  body part they went into.
* The laser splits convex polygons (head circle, limb sprites) along the beam line and
  turns each half into its own rigid body with the sprite clipped to the polygon.
* The acid effect draws a skeleton under the skin and clips the skin from top to bottom.

## Notes

* Google voices and the extra online voices need an internet connection and are
  streamed from an unofficial endpoint, so they may stop working one day. The browser's
  own voices always work.
* Sounds are generated with the Web Audio API, except `break.mp3`.
