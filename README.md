# Gesture Volume Control 🎛️✋

Control your Windows system volume using only your hand gestures and a webcam.

<img width="634" height="502" alt="Στιγμιότυπο οθόνης 2026-06-08 173710" src="https://github.com/user-attachments/assets/21dde49c-3b28-43dd-83e0-24ac0ab6f798" />

This project uses **OpenCV**, **MediaPipe**, and **Pycaw** to track your hand in real-time and adjust the system volume based on the distance between your **thumb** and **index finger**.

## Features

* 🎥 Real-time hand tracking
* 🔊 System volume control using gestures
* ⚡ Adjustable sensitivity multiplier
* 📊 On-screen volume percentage display
* 🖥️ Works with any standard webcam
* 🤖 Powered by MediaPipe hand landmarks

## How It Works

1. The webcam captures video frames.
2. MediaPipe detects and tracks hand landmarks.
3. The distance between the thumb tip and index finger tip is calculated.
4. The distance is mapped to the Windows volume range.
5. The system volume updates instantly.

**Close fingers → Lower volume**

**Move fingers apart → Higher volume**

## Technologies Used

* Python
* OpenCV
* MediaPipe
* NumPy
* Pycaw
* Tkinter

## Installation

> **Note:** Volume control relies on [Pycaw](https://github.com/AndreMiras/pycaw), which wraps the
> Windows Core Audio API. This project only runs on **Windows**.

Clone the repository:

```bash
git clone https://github.com/mariospapadimas/gesture-volume-control.git
cd gesture-volume-control
```

Install dependencies:

```bash
python -m pip install "mediapipe==0.10.21" "numpy<2" "opencv-contrib-python<4.12" pycaw comtypes
```

### Dependency compatibility

Use a fresh virtual environment with 64-bit Python 3.11. The code uses MediaPipe's
legacy `mediapipe.python.solutions` API, so the install command pins MediaPipe
0.10.21 and compatible NumPy/OpenCV versions. `opencv-contrib-python` provides
the `cv2` module and is also required by MediaPipe; do not install a second
OpenCV wheel alongside it in the same environment. Migration to the newer
[MediaPipe Tasks API](https://developers.google.com/mediapipe/solutions/vision/hand_landmarker)
would require separate code changes.

Tkinter is part of the Windows Python installer when Tcl/Tk is selected. Pycaw
and comtypes are Windows-specific dependencies. This repository currently lists
its dependencies in this README rather than a requirements or lock file.

## Project Structure

```
gesture-volume-control/
├── main.py           # Entry point: captures webcam feed and drives volume control
├── hand_detector.py  # Reusable HandDetector class (MediaPipe hand landmarks, finger state, distance)
├── README.md
└── LICENSE           # Existing Apache License 2.0
```

`hand_detector.py` wraps MediaPipe's hand-tracking solution in a `HandDetector` class with helper
methods (`findHands`, `findPosition`, `fingersUp`, `Distance`) that can be reused in other
hand-tracking projects, independent of the volume-control logic in `main.py`.

## Usage

Run the application:

```bash
python main.py
```

A dialog box will appear asking for a sensitivity multiplier:

* The multiplier scales the measured finger distance before mapping it to volume.
* A larger positive value reaches higher volume at a smaller finger spacing.
* A smaller positive value maps the same spacing to a lower volume; it does not add smoothing.

After selecting a value:

* Show your hand to the webcam
* Move your thumb and index finger closer or farther apart
* Watch the volume change in real time

Press **ESC** to exit.

## Controls

| Gesture                             | Action           |
| ----------------------------------- | ---------------- |
| Thumb + Index Finger Close Together | Lower Volume     |
| Thumb + Index Finger Far Apart      | Increase Volume  |
| ESC Key                             | Exit Application |

## Requirements

* Windows 10/11
* 64-bit Python 3.11 (verified with 3.11.9), including Tcl/Tk
* A working webcam with camera permission enabled for desktop applications
* An available Windows audio output device

## Future Improvements

* Multiple gesture support
* Mute gesture
* Brightness control
* Custom gesture mapping
* Cross-platform audio support

## Demo

See the screenshot above for a preview. A GIF or video demonstrating the live gesture control
would be a great addition here — contributions welcome!

## License

This project is open source and available under the Apache License Version 2.0 .
