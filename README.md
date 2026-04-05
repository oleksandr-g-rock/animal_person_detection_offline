# 👁 Camera Detection Zone

![JavaScript](https://img.shields.io/badge/JavaScript-ES2020-f7df1e?style=flat-square&logo=javascript&logoColor=black)
![Single File](https://img.shields.io/badge/app-single%20file-4f46e5?style=flat-square)
![MediaPipe](https://img.shields.io/badge/MediaPipe-DeepLabV3-00897b?style=flat-square)
![Mobile Ready](https://img.shields.io/badge/mobile-ready-22c55e?style=flat-square)
![No Dependencies](https://img.shields.io/badge/dependencies-none-lightgrey?style=flat-square)
![License](https://img.shields.io/badge/license-AS%20IS-red?style=flat-square)

A single-file web app that uses the device camera and pixel-level segmentation (DeepLabV3) to detect people and animals inside a user-defined zone.
https://oleksandr-g-rock.github.io/animal_person_detection_offline/

> **UI language:** Ukrainian. Button labels are in Ukrainian — see the [Usage](#usage) section for a translation.

---

## Features

| Feature | Description |
|---|---|
| 🎯 **Pixel segmentation** | Per-pixel mask for people and animals — no bounding boxes |
| 📦 **Detection zone** | Drag and resize the zone directly on screen |
| 💾 **Auto-save** | Zone position is persisted in `localStorage` |
| 🔊 **Audio alert** | Beep sound when a target enters the zone |
| 📳 **Vibration** | Phone vibrates on alert (mobile only) |
| 🔒 **Wake Lock** | Screen stays on while the app is running |
| ⚡ **Throttling** | Inference runs every 4th frame to save battery |
| ⏱ **Stats** | Uptime, alert count, and live FPS display |
| 📜 **History log** | Timestamped log of each detection event with duration |

---

## Setup

### Option 1: Open directly in Chrome

Double-click `index.html` or drag it into Chrome. An internet connection is required on the **first launch** to download the MediaPipe WASM runtime and the DeepLabV3 model (~8 MB total). Both are cached by the browser afterwards.

> Camera access requires a [secure context](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts). Opening via `file://` works in Chrome. For other browsers, use Option 2.

### Option 2: Local HTTP server (recommended for phones)

```bash
cd person-detection
python3 -m http.server 8000
```

Then open on your phone (same Wi-Fi network):

```
http://<your-computer-IP>:8000
```

To find your IP: `ipconfig getifaddr en0` (macOS) or `ip route get 1` (Linux).

### Option 3: HTTPS via ngrok (for camera on non-Chrome browsers)

```bash
ngrok http 8000
```

Open the HTTPS link from ngrok on your phone.

### First launch checklist

1. Open the page with an internet connection — model downloads and caches automatically
2. Accept the disclaimer
3. Allow camera access
4. Done

---

## Usage

| Button (Ukrainian) | Action |
|---|---|
| **Зона** | Toggle zone editing — drag to move, drag corners/edges to resize |
| **Лог** | Toggle the history log panel |
| **Скинути** | Reset zone to default position |

---

## Detected classes

| Class | Icon |
|---|---|
| Person | 🧑 |
| Bird | 🐾 |
| Cat | 🐾 |
| Cow | 🐾 |
| Dog | 🐾 |
| Horse | 🐾 |
| Sheep | 🐾 |

Classes are based on the Pascal VOC label set used by DeepLabV3.

---

## Tech stack

| Technology | Role |
|---|---|
| [MediaPipe Tasks Vision](https://ai.google.dev/edge/mediapipe/solutions/vision/image_segmenter) | WASM-based on-device inference |
| DeepLabV3 (float32, Pascal VOC) | Semantic segmentation model |
| Web Audio API | Alert beep synthesis |
| Screen Wake Lock API | Prevents display sleep |
| Canvas 2D | Mask rendering onto video overlay |

---

## File structure

```
person-detection/
├── index.html   ← Entire app — UI, logic, styles in one file
└── README.md    ← This file
```

---

## ⚠️ Legal disclaimer

**THIS APP IS AN EXPERIMENTAL PROTOTYPE.**

It is intended solely for testing, educational, and demonstration purposes.

### Limitation of liability

1. **NOT A CERTIFIED SAFETY SYSTEM.** This app has not undergone any certification, testing, or validation as a safety system, driver-assistance system (ADAS), or collision-prevention system.

2. **DOES NOT REPLACE DRIVER ATTENTION.** Use of this app in no way relieves the driver of the obligation to monitor road conditions. The driver bears full responsibility for road safety at all times.

3. **DOES NOT GUARANTEE DETECTION.** The machine learning model may:
   - Miss objects (false negatives)
   - Trigger incorrectly (false positives)
   - Perform with latency or inaccurately in poor lighting, during motion, or under vibration

4. **NOT DESIGNED FOR REAL ROAD CONDITIONS.** The app has not been tested for and is not intended for use during actual driving or in any situation where human safety may depend on it.

5. **USE AT YOUR OWN RISK.** The developer accepts no liability for:
   - Injury or loss of life
   - Property damage
   - Traffic violations
   - Any other consequences arising from use of this app

6. **LEGAL COMPLIANCE.** Using a phone camera while driving may be prohibited by law in your country. Ensure compliance with local regulations before use.

### License

This prototype is provided "AS IS" without any warranty, express or implied.

---

*Prototype. Not for production use.*
