# Gesture on the Beat

An interactive version of the "Say the word on the beat" meme. Instead of saying words, you
copy hand gestures. MediaPipe's Gesture Recognizer checks each one through your webcam.

## Run it

The webcam and MediaPipe need the page to be served over `http://localhost`, not opened as a file:

```sh
cd "Say the Word Game"
python3 -m http.server 8000
```

Then open http://localhost:8000 in Chrome or Edge, allow camera access and press **Start**.
An internet connection is needed: MediaPipe and the model load from a CDN.

## How it plays

- The template video has 5 rounds. Each round, the 8 gestures pop into the boxes one per beat,
  over the 8 beats before the highlight starts.
- The green highlight moves through the boxes on the beat (about 0.33 s per box at 1×).
  Show that box's gesture to the camera while it is highlighted.
- A box counts as a hit if MediaPipe recognises the gesture (score ≥ 0.5) from slightly before
  the beat until 0.3 s after it.
- Difficulty goes up each round: round 1 uses 2 gestures in pairs, and round 5 uses all 7
  with no repeats in a row. Sequences are new every game.
- Use 0.5× or 0.75× speed to practise.

## Gestures (MediaPipe built-in labels)

✊ Closed_Fist · ✋ Open_Palm · ☝️ Pointing_Up · 👍 Thumb_Up · 👎 Thumb_Down · ✌️ Victory · 🤟 ILoveYou

## Tweaking

All timing is at the top of the script in `index.html`. These values were measured from the
template video:

- `ROUNDS`: when each round's highlight starts (`sweep`). The gestures pop in over the 8 beats before it.
- `BEAT`: seconds per box
- `GRACE_BEFORE` / `GRACE_AFTER`: how lenient the scoring is
- `makeRound()`: how each round's sequence is generated
