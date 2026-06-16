# 🎵 Gesture Volume Control

Control your system volume in real-time using hand gestures — no keyboard, no mouse, just your fingers.

Built with Python, OpenCV, and MediaPipe.

---

## 📸 Demo

![Demo](test%20project.PNG)

---

## 🚀 How It Works

1. Webcam captures live video feed
2. **MediaPipe Hands** detects 21 hand landmarks in real-time
3. Euclidean distance between **thumb tip (landmark 4)** and **index finger tip (landmark 8)** is calculated
4. Distance is mapped to system volume range using `numpy.interp`
5. **Pycaw** sets the master volume level on Windows audio endpoint

```
Finger distance: 30px  → Volume: 0%
Finger distance: 350px → Volume: 100%
```

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `opencv-python` | Video capture & frame rendering |
| `mediapipe` | Hand landmark detection |
| `pycaw` | Windows audio endpoint control |
| `numpy` | Distance-to-volume interpolation |
| `comtypes` | COM interface for audio API |

---

## ⚙️ Installation

**Requirements:** Python 3.8+, Windows OS (Pycaw is Windows-only)

```bash
git clone https://github.com/vohuynhdatpy/GESTURE-VOLUME-CONTROL.git
cd GESTURE-VOLUME-CONTROL
pip install opencv-python mediapipe pycaw numpy comtypes
```

---

## ▶️ Usage

```bash
python "Gesture Volume Control.py"
```

- **Pinch fingers together** → Volume decreases
- **Spread fingers apart** → Volume increases
- A real-time volume bar appears on screen showing current level
- Press **Spacebar** to exit

---

## 📁 Project Structure

```
GESTURE-VOLUME-CONTROL/
├── Gesture Volume Control.py   # Main application
├── here.py                     # Hand tracking module (MediaPipe wrapper)
├── introduc.py                 # Introduction / demo script
├── test project.PNG            # Demo screenshot
└── note.txt                    # Development notes
```

---

## 📊 Performance

| Metric | Value |
|---|---|
| FPS | 20–25 FPS on standard laptop |
| Latency | < 100ms end-to-end |
| Gesture accuracy | ~92% under standard lighting |
| Hand range | 30px – 350px finger distance |

---

## 🔑 Key Implementation Details

```python
# Landmark indices used
THUMB_TIP  = 4
INDEX_TIP  = 8

# Distance → Volume mapping
length = hypot(x2 - x1, y2 - y1)
vol = np.interp(length, [30, 350], [volMin, volMax])

# Set system volume via Pycaw
volume.SetMasterVolumeLevel(vol, None)
```

---

## 📌 Limitations

- Currently **Windows only** (Pycaw dependency)
- Requires good lighting for stable hand detection
- Single hand only; designed for right-hand use

---

## 👤 Author

**Võ Huỳnh Đạt**
- GitHub: [@vohuynhdatpy](https://github.com/vohuynhdatpy)
- LinkedIn: [linkedin.com/in/nimbid](https://www.linkedin.com/in/nimbid/)

---

## 📄 License

MIT License — free to use and modify.
