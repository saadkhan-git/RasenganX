<div align="center">

# Naruto Rasengan Creation Using Hand Detection

**Bring a little chakra to your webcam: raise an open palm and summon a glowing Rasengan.**

[![JavaScript](https://img.shields.io/badge/JavaScript-ES6%2B-F7DF1E?logo=javascript&logoColor=000)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-static%20web%20app-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![MediaPipe Hands](https://img.shields.io/badge/Hand%20tracking-MediaPipe-0097A7?logo=google&logoColor=white)](https://developers.google.com/mediapipe)

</div>

---

## Project Preview

The repository includes the Rasengan effect clip used by the app. Open the MP4 to preview that effect:

**[▶ View the Rasengan effect clip](assets/rasengan.mp4)**

<!-- TODO: Add a screenshot of the running webcam experience when one is available. -->

> **Screenshots:** No application screenshots or animated demo are currently included in the repository. The MP4 above is the effect asset, not a recording of the complete application.

## About the Project

Naruto Rasengan Creation Using Hand Detection is a small, browser-based computer-vision experience. It combines a live webcam feed with MediaPipe hand tracking, a glowing hand-landmark overlay, and a bundled Rasengan video effect.

When the app recognizes an open palm, it gradually reveals the effect above that hand. The effect follows the hand as it moves; closing or moving the hand out of view fades it away. Up to two hands can be tracked independently, each with its own orb state and skeleton colors.

The page runs without a project backend or build step. Camera frames are passed to MediaPipe in the browser; the app source contains no upload or server-side processing logic. MediaPipe scripts and model files are loaded from jsDelivr, so an internet connection is needed when using the app.

## Features

- **Live webcam input** displayed as a full-window, mirrored video layer.
- **Two-hand tracking** using MediaPipe Hands.
- **21-landmark hand skeleton** drawn on a canvas with glowing bones and joints.
- **Open-palm interaction** that triggers the Rasengan when at least three tracked fingers meet the app's extension check.
- **Independent effects per hand**, with distinct warm and cool skeleton palettes.
- **Smooth effect fade** based on per-hand charge state.
- **Hand-following placement** that positions the effect relative to hand landmarks and adjusts its height above the palm based on hand size.
- **Static, no-build setup** using browser APIs and scripts loaded from a CDN.

## How It Works

1. **Capture:** MediaPipe `Camera` requests a 1280 × 720 webcam stream and supplies frames to the hand model.
2. **Detect:** MediaPipe Hands is configured for up to two hands, with model complexity `1` and detection/tracking confidence thresholds of `0.65`.
3. **Track:** For each detected hand, the app receives 21 normalized landmarks and a left/right label. The landmarks are drawn on a canvas using MediaPipe drawing utilities.
4. **Recognize a gesture:** The app compares each of four fingertip distances from the wrist with the corresponding PIP-joint distances. Three or more fingertips farther from the wrist count as an open palm.
5. **Update the effect:** Each hand has its own charge value. An open palm increases opacity; a closed or unseen hand decreases it. On the transition to an open palm, the corresponding Rasengan video restarts.
6. **Place and display:** The effect is positioned above the hand using the wrist and middle-finger base landmarks. The webcam, skeleton, vignette, and effect layers are composited in the browser in real time.

## Screenshots & Media

The project currently contains one visual asset, the Rasengan effect video. It does not include screenshots of hand detection, tracking, or the complete app output.

### Bundled Rasengan effect

[Open the Rasengan effect clip (MP4)](assets/rasengan.mp4)

<!-- TODO: Add separate, verified screenshots for hand detection, hand tracking, and the final webcam output when available. -->

## Technologies Used

| Technology | Role |
|---|---|
| HTML5 | Defines the page, webcam video, canvas, and effect video elements. |
| CSS | Layers and mirrors the webcam view, positions the effect, applies screen blending, and adds a vignette. |
| JavaScript | Implements camera setup, per-frame tracking, gesture evaluation, skeleton drawing, and effect positioning/fading. |
| [MediaPipe Hands](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker) | Detects hands and provides landmarks and handedness through the MediaPipe Hands JavaScript solution. |
| `@mediapipe/camera_utils` | Connects the webcam stream to the per-frame processing callback. |
| `@mediapipe/drawing_utils` | Draws the hand connections on the canvas. |
| Canvas 2D API | Renders landmark joints and the glowing hand skeleton. |
| `getUserMedia` (through MediaPipe Camera) | Provides browser webcam access. |
| jsDelivr | Serves the MediaPipe JavaScript files and model resources referenced by the page. |

## Installation & Setup

### Requirements

- A modern browser with webcam access.
- A webcam, with permission granted to the site.
- Python 3 (or another local static HTTP server).
- An internet connection to load MediaPipe resources from jsDelivr.

### Run locally

1. Download or clone the project and open a terminal in its root directory (the directory containing `index.html`).
2. Start a local HTTP server:

   ```bash
   python -m http.server 8000
   ```

   On Windows, if the `python` command is unavailable but the Python launcher is installed, use:

   ```powershell
   py -m http.server 8000
   ```

3. Open [http://localhost:8000](http://localhost:8000) in your browser and allow camera access.
4. Hold one or both hands in view and open your palm to trigger the effect.

The application is a static page: there is no `npm install`, package manifest, or build command in this repository. Use `localhost` (or HTTPS) rather than opening `index.html` directly with `file://`, since browsers restrict webcam access on insecure origins.

## Project Structure

```text
.
├── assets/
│   └── rasengan.mp4   # Video used for the on-hand visual effect
├── .gitignore         # Ignores .DS_Store files
├── index.html         # Complete app: markup, styles, and JavaScript
└── README.md          # Project documentation
```

## Future Improvements

- Add screenshots or a short capture of the complete webcam experience.
- Offer adjustable gesture sensitivity and effect positioning.
- Add on-screen setup guidance and camera/permission error feedback.
- Make the effect asset and visual settings easier to customize.
- Evaluate options for reducing reliance on CDN-hosted runtime resources.

## Learning Outcomes

- Applying computer vision in a browser.
- Processing webcam frames in real time.
- Working with hand landmarks, handedness, and gesture heuristics.
- Compositing canvas and video layers to create an interactive visual effect.

## Author & Credits

- **Author:** Mohammad Saad Khan
- **Project:** Naruto Rasengan Creation Using Hand Detection
- **Hand tracking and drawing utilities:** [MediaPipe](https://developers.google.com/mediapipe)

The source repository does not identify the creator or usage license of `assets/rasengan.mp4`. Confirm the asset's rights and attribution requirements before redistributing the project.
