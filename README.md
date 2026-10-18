# breathe

A one-page interactive piece for the assignment *a page with a constraint*.

## The constraint

**The page only moves to your breath.**

There is nothing to click, scroll or tap once it begins. The only input is the
sound of you breathing out.

## Concept

This is a short break from screens. After hours of work, you spend about two
minutes with a single plastic bag floating in a quiet, empty space. Before you
begin, you type a few words for what you want to let go of: *work stress*,
*the deadline*, a name, a feeling. Those words are held by the bag. Every time
you exhale, letters break loose from it and blow away.

Screens use our attention the way we use plastic bags: briefly, carelessly,
and then they throw it away. This page turns that around. For two slow
minutes, the screen asks for nothing but your breath, and what you let go of
is something you chose.

## The experience

**1. The question.** The page opens on a sunlit, sand-colored space with a few
lines of typewriter text:

> what do you want to let go of?
>
> breathe out slowly. the bag will listen.

You type your words and press *begin*, and the browser asks for permission to
use the microphone.

**2. Calibration.** One line appears: *stay quiet for a moment.* For a few
seconds the page listens to the room so it can tell your breath apart from the
hum of a laptop fan, traffic or air conditioning.

**3. The bag.** Then all text disappears, and only the bag remains, with a
thin green line of horizon far below. It is never completely still: it
sways, turns slightly and breathes a little on its own. When you breathe in
or stay silent, it hangs in the air and flutters gently.

When you breathe out, it moves:

- **The longer the exhale, the further it goes.** A long, gentle breath
  carries the bag smoothly across the space and releases more letters, which
  travel far before they fade.
- **The harder the exhale, the more chaotic it gets.** A sharp puff makes the
  bag jolt, flutter and spin, and the letters scatter roughly.

The piece rewards slow, long breaths. Breathing calmly is the way to get the
most out of it.

Letters break off one at a time from your words. They appear in deep blue
typewriter type, each slightly different in size, angle and opacity. They
drift, rotate and fade as they leave. Nothing collects or piles up. They're
released, not accumulated.

**4. The bag changes.** At first the bag is crumpled and heavy, carrying your
words. It sags low and barely lifts. As letters leave, it becomes more open
and buoyant and answers your breath more easily. In the last part of the two
minutes it also slowly fades, becoming more and more like the sky behind it.

**5. The ending.** After about two minutes, breath stops moving the bag. It
sinks slowly and comes to rest, empty, on the horizon line. After a pause, a
last line of text fades in:

> let go.

The page then stays still. There is no restart button. To begin again, reload
the page.

**Without a microphone.** If microphone access is denied or unavailable, a
small line appears: *no microphone. hold the spacebar to breathe out.* Holding
the spacebar then acts as an exhale, and the longer you hold it, the further
the bag drifts.

## Visual direction

Still, warm and minimal, like late light on a white wall by the sea. The
palette is Mediterranean, flat and saturated, with no pastels and no
gradients: whitewashed walls, terracotta, blue tiles, cypress.

| Role | Color | Hex |
|---|---|---|
| Sky / background | sunlit lime-wash sand | `#EFE6D5` |
| Bag | burnt orange | `#C34811` |
| Released letters | deep blue | `#0B369A` |
| Horizon line | deep green | `#1D6813` |

- **Only the bag is on screen** during the experience. There's no navigation
  and no title, and the only text is the released letters.
- **The bag** comes from a photograph of a real plastic bag, recolored to
  burnt orange. Its translucency comes from the photo itself: the thin
  plastic lets the sand-colored background glow through, and the creases,
  folds and handles read as deeper orange.
- **The letters** use a typewriter face (Special Elite).
- **The green** is used only once, as a thin, distant horizon line low on the
  screen. It's the only trace of land or sea.

The four colors are defined as CSS variables at the top of `index.html` so
they can be adjusted by hand.

## How it works

- **Breath detection:** The Web Audio API reads the microphone through an
  `AnalyserNode`. Each frame, the page measures the loudness of the incoming
  sound and compares it to the room's noise level measured during calibration.
  Sound above that baseline counts as an exhale. The signal is smoothed so
  the bag's movement eases in and out and never twitches.
- **Two readings of each breath:** The *duration* of an exhale drives how far
  the bag drifts and how many letters are released. The *force* (how loud it
  is) drives turbulence: flutter, spin and scatter.
- **Animation:** Everything is drawn in the browser with plain JavaScript on
  a `requestAnimationFrame` loop. The bag photo is tinted and given its
  transparency at load time, then swayed, rotated, scaled and drifted every
  frame.
- **No audio leaves the device.** The microphone is analyzed live in the
  browser. Nothing is recorded, stored or sent anywhere.

## Files

```
index.html   the whole piece: HTML, CSS and JavaScript in one file
bag.png      the photographed bag (the red bag from the source photo)
README.md    this file
```

No frameworks, no build step, no API keys. The only external resource is the
typewriter font from Google Fonts.

## Previewing locally

Browsers only allow microphone access on secure pages, so opening
`index.html` directly from the Finder (`file://…`) will not work. Serve the
folder locally instead. In Terminal:

```sh
cd ~/Documents/GitHub/breathe
python3 -m http.server 8000
```

Then open <http://localhost:8000> in Chrome, Safari or Firefox and allow
microphone access when asked. Press `Ctrl+C` in Terminal to stop the server.

For best results, use headphones or a quiet room, and breathe toward the
laptop's microphone from a short distance.

## Hosting

The piece is hosted on GitHub Pages, which serves pages over HTTPS, so the
microphone works there without any extra setup. In the repository settings,
under **Pages**, set the source to the `main` branch and root folder. The
site will be published at `https://<username>.github.io/breathe/`.
