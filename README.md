# 🎹 Gesture Synth (web app)

Play chords with your hands in the browser using your webcam — purple/pink theme, hand-tracking via MediaPipe, real-time synth audio via Tone.js. Single HTML file, nothing to install.

---

## 1. Requirements

- A modern browser (Chrome, Edge, Safari, Firefox).
- A webcam and working audio output.
- **The page must be served over `https://` (or `localhost`)** — opening the file directly (`file://`) blocks camera access on most browsers, especially on mobile. See section 3.

---

## 2. Files

- `gesture_synth.html` — the whole app (HTML + CSS + JS in one file). Open it in a browser once it's hosted (see below).

---

## 3. Hosting (required for the camera to work)

Pick whichever is easiest for you:

- **Netlify Drop** (simplest, no signup): go to **app.netlify.com/drop**, drag and drop `gesture_synth.html`, open the generated `https://...netlify.app` link.
- **GitHub Pages**: push the file to a repo, enable Pages in the repo settings, open the generated URL.
- **Local dev server** (if you have Python installed): run `python -m http.server` in the folder, then open `http://localhost:8000/gesture_synth.html`.

---

## 4. How to play

- **Left hand** (screen-left): number of raised fingers (1–7) picks a chord from the scale — 1 finger = the **I** chord, 4 fingers = the **IV** chord, and so on.
- **Left hand height**: move it up or down to shift the chord an octave.
- **Right hand**: raise it and move it up/down to open or close the filter (brighter near the top, darker near the bottom).
- **Top-left menus**: change the **key** and the **synth tone** (Bright / Warm / Pad) any time.
- **Open Guide**: shows the same instructions in-app.
- Lower both hands to stop the sound; tap **stop** to end the session.

---

## 5. Troubleshooting

| Problem | Fix |
|---|---|
| Nothing happens when tapping "play now" | The page is opened via `file://`. Host it over `https://` (see section 3) — camera access is blocked otherwise, often silently. |
| Camera permission denied | Check your browser's site settings for the hosted URL and allow camera access, then reload. |
| No sound | Some browsers require a user gesture before audio starts — make sure you tapped "play now" yourself. Check your device isn't muted. |
| Laggy tracking | Close other tabs/apps using the camera or CPU; try a smaller browser window. |

---

## 6. Customizing

Everything lives inside `gesture_synth.html`:

- **Colors** — CSS variables at the top of the `<style>` block (`--violet`, `--pink`, `--bg`, …).
- **Scale / chord logic** — `SCALE`, `chordForDegree()` in the `<script>` block.
- **Synth tones** — `buildSynth()`.
- **Fonts** — the Google Fonts `@import` line (`Fredoka` / `Quicksand`).#
