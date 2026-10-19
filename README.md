# Aliento

*A page with a constraint.*

## Concept

In Spanish, *aliento* means both breath and encouragement. Advice from an elder is aliento in both senses: it is given with their breath, and it keeps us going. This page keeps the memories and advice of elders, living or dead, so that younger generations carry forward the people who came before them.

The visitor sees an old hand. They write something an elder told them, a memory or a piece of advice, into a band of light across the back of the hand. Then they breathe on the screen. The words become light, travel up one of the fingers and leave the fingertip. Then they become part of a luminous memory tree growing behind the hand. Each memory adds a ring at the base of the tree, the way tree rings record years and wrinkles record a life.

The hand is photographic, grayscale and still: it belongs to the body. The tree is digital and glowing: it is an archive. The space between them is the subject of the piece, memory leaving the body and becoming something that lasts.

## The constraint

**A memory can only be released with your breath.**

There is no submit button. Typing a memory is not enough. To let it go, you have to give it your own breath, the way an elder once gave it theirs.

## The experience

**Opening.** The page begins on a dark screen with a single word: *aliento*. Clicking it asks for permission to use the microphone. A short bilingual line, *silencio… / quiet…*, holds the room for a few seconds while the page listens to its silence and learns how loud the room is. Then the hand fades in.

**The hand.** The elder's hand, cut out from its photograph, rests on a dark background. A soft band of light lies across the back of the hand, near the wrist. That band is where the visitor writes. There is no navigation and no title, only the hand, the light and the tree behind it.

**Writing.** The visitor types a memory directly into the band of light. When they press Enter, the band clears and quietly asks *¿de quién? / from whom?*. They can name the elder ("mi abuela", "my grandfather") or skip this and breathe straight away. Once there is something to release, the band glows stronger and the page waits.

**Breathing.** When the visitor exhales onto the screen, the text dissolves into light. The light travels from the band up through one finger and leaves the fingertip. The fingers take turns in order: the first memory leaves through the thumb, the next through the index finger, then the middle, ring and little fingers, and then the thumb again, like counting on your fingers. A long, gentle exhale carries the light smoothly. A short, sharp one moves it in a quicker, less even way.

**The tree.** There is a single tree, standing behind the hand on a black ground. The light flies into the background and joins it. A new ring ripples outward across the ground from its trunk, and the canopy grows a little denser. The rings are fine, concentric lines in iridescent magenta, cyan, yellow and lavender, spreading like ripples in water around the base of the trunk and behind the wrist of the hand. The canopy is soft and blue-violet, dissolving into vertical scanlines and faint glyph-like dashes, as if the tree were being read off a screen. Over time, as memories gather, the tree grows denser and brighter. It treats every elder the same, whether they are still alive or have died, because on this tree the memory is what keeps them present.

**Reading.** Hovering over a ring or a branch reveals the memory it holds in small text, along with who it came from when that was given.

## Breath

The page listens through the microphone using the Web Audio API and measures the volume of the incoming sound. During the opening silence it calibrates a baseline for the room. Afterwards it treats a sustained rise above that baseline as an exhale, and it smooths the signal so that a cough or a voice does not count as breath. The strength and length of the exhale shape how the light travels.

If the visitor denies the microphone, holding the spacebar acts as a breath.

## Memories

The tree begins with seed memories written by the author, kept in `memories.json` so they can be edited at any time without touching the page. Each memory has this shape:

```json
{ "text": "...", "from": "my grandmother", "lang": "es" }
```

Memories left by visitors are saved in their own browser (localStorage) and grow on the same tree, after the seeds. They stay on that visitor's device, so each person who comes back finds their own memories still there. The page fills in `lang` automatically by guessing whether the memory is written in Spanish or English. Memories can be in either language.

## Files

- `index.html`: the whole page, in plain HTML, CSS and JavaScript, with no frameworks and no build step.
- `memories.json`: the seed memories.
- `hand.png`: the hand photograph.
- `hand-cutout.png`: the same hand with its gray background removed, used on the page.
- `hand-labeled.png`: a map of the hand used during development, never shown on the page. It marks the fingers A (thumb) to E (little finger) and the input bar.
- `tree-reference.png`: a style reference for the tree, never shown on the page.

Every position (the input bar, the five fingertips, the path up each finger) and every color lives in a single `CONFIG` object at the top of the script, so they can be adjusted by hand.

## Previewing locally

Browsers only allow the microphone on a secure origin, so opening `index.html` by double-clicking it won't work. Instead, run a small local server from this folder:

```sh
cd ~/Documents/GitHub/aliento
python3 -m http.server 8000
```

Then open <http://localhost:8000> in the browser. `localhost` counts as secure, so the microphone prompt will appear.

To tune the breath detection, open <http://localhost:8000/?debug>. A small panel shows the microphone level, the room's baseline and the threshold a breath must cross. If gentle breaths aren't detected, raise `breath.sensitivity` in `CONFIG` (for example to `1.5` or `2`).

Visitor memories live in your browser's localStorage. To clear them while testing, run `localStorage.removeItem('aliento.memories')` in the browser console.

## Publishing

The site is hosted on GitHub Pages, which serves over HTTPS, so the microphone works there too. Push the folder to GitHub, then in the repository go to **Settings → Pages** and publish from the main branch.
