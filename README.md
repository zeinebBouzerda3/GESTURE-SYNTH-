# 🎹 Gesture Synth (desktop app)

Play chords with your hands using your webcam — a native Python window, no
browser or hosting required. Purple/pink theme, hand-tracking powered by
MediaPipe, real-time synth audio.

---

## 1. Requirements

- **Python 3.10 – 3.13** (Python 3.14 is too new — `pygame` and `mediapipe`
  don't have installable builds for it yet. If you have several Python
  versions on your machine, see the Windows note below.)
- A webcam and a working audio output.
- An internet connection **the first time you run it** (to download the
  hand-tracking model, ~10 MB, one time only).

---

## 2. Install

Open a terminal in this folder and run:

```
pip install -r requirements.txt
```

### Windows: if you have multiple Python versions installed

Windows often has more than one Python on the system (e.g. one from the
Microsoft Store, one from python.org). If `python main.py` later fails with
`ModuleNotFoundError` even though `pip install` said everything was already
there, it means `pip` and `python` are pointing at **different** installs.

Fix it by always specifying the version explicitly with the `py` launcher:

```
py -0
```
This lists every Python version available (e.g. `3.13`, `3.14`). Pick a
supported one (3.10-3.13) and use it consistently:

```
py -3.13 -m pip install -r requirements.txt
py -3.13 main.py
```

---

## 3. Run

```
python main.py
```
(or `py -3.13 main.py` on Windows if you have multiple versions - see above)

A window opens. Click **play now**, allow camera/microphone access if your OS
prompts you, and start playing. The first launch downloads the hand-tracking
model automatically (`hand_landmarker.task`, saved next to `main.py` so it's
only downloaded once).

---

## 4. How to play

- **Left hand** (screen-left): number of raised fingers (1-7) picks a chord
  from the scale - 1 finger = the **I** chord, 4 fingers = the **IV** chord,
  and so on.
- **Left hand height**: move it up or down to shift the chord an octave.
- **Right hand**: raise it and move it up/down to open or close the filter
  (brighter near the top, darker near the bottom).
- **Top-left buttons**: click to cycle the **key**, the **synth tone**
  (Bright / Warm / Pad), or open the **guide**.
- Press **ESC** or click **stop** to quit.

---

## 5. Troubleshooting

| Problem | Fix |
|---|---|
| `ModuleNotFoundError` after installing | You likely have multiple Python versions - see the Windows note in section 2. Use `py -3.13 ...` consistently for install *and* run. |
| `pygame` fails to build from source | This happens when there's no precompiled wheel for your Python version (usually Python 3.14+). Switch to Python 3.10-3.13. |
| "Couldn't open the webcam" | Close any other app using the camera (Zoom, Teams, etc.). On Windows: Settings -> Privacy -> Camera, allow desktop apps. |
| "Couldn't load the hand-tracking model" | Needs internet on first run to download `hand_landmarker.task`. Check your firewall/proxy isn't blocking `storage.googleapis.com`. |
| No sound | Check your OS's default output device. |
| Choppy video / low FPS | Close other heavy apps - hand tracking is CPU-bound. You can also lower `CAM_W` / `CAM_H` near the top of `main.py`. |
| Hands not detected well | Make sure you have decent, even lighting and both hands are fully in frame. |

---

## 6. Customizing

Everything lives in `main.py`:

- **Colors** - edit the constants near the top (`VIOLET`, `PINK`, `BG_DARK`, ...).
- **Window size** - `WINDOW_W`, `WINDOW_H`.
- **Camera resolution** - `CAM_W`, `CAM_H`.
- **Scale / chord logic** - `SCALE`, `chord_for_degree()`.
- **Synth tones** - `AudioEngine._waveform()` and `SYNTH_TYPES`.
