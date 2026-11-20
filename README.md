# Well Monitor

Real-time human, animal, and bird detector with a simple, high-performance local web dashboard powered by YOLO11n.

## Features

- **Pretrained YOLO11n Detection**: Automatically classifies and bounds:
  - **Human**: (COCO class 0)
  - **Animal**: Cats, dogs, horses, sheep, cows, elephants, bears, zebras, giraffes (COCO classes 15–23)
  - **Bird**: (COCO class 14)
- **Smooth Background Inference**: Multi-threaded capture and inference loop to keep video latency low without backlog accumulation.
- **Hardware Camera Port Discovery & Dynamic Switching**: Scans all available USB camera ports and lets you switch between built-in, external, or IP/RTSP streams live from the dashboard.
- **Automated Snapshots & Cooldown Alerts**: Automatically saves annotated snapshot images to `alerts/` when an enabled category is detected and prints alert logs to the console.
- **Local Web Dashboard**:
  - Live MJPEG video stream with bounding boxes and confidence scores.
  - Category presence count cards that illuminate red in real time.
  - Interactive settings sliders for detection confidence (0.1–0.9) and alert cooldown (1–120s).
  - Toggles for human, animal, and bird tracking.
  - Recent alerts gallery with instant image zoom modal and "Clear all" capability.
  - Light and Dark mode auto-switching via `prefers-color-scheme`.
  - Zero external dependencies: 100% offline-ready (no CDNs, no remote fonts/scripts).

---

## Project Structure

```text
WELLDETECT/
├── .gitignore
├── README.md
└── well-monitor/
    ├── app.py                  # Detector engine + Flask web application
    ├── requirements.txt        # Python package dependencies
    ├── templates/
    │   └── index.html          # Dashboard UI (HTML, CSS, JS)
    └── alerts/                 # Saved snapshot images
```

---

## Getting Started

### 1. Requirements

- Python 3.9+
- Webcam or external USB camera

### 2. Setup Virtual Environment

```powershell
cd well-monitor
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Run the Application

**Quick Start (Windows 1-Click):**
Simply double-click `well-monitor/start.bat`. It will automatically set up the virtual environment, install requirements if missing, launch the server, and open your browser!

**Manual Start:**
```powershell
python app.py
```

Open your browser and navigate to:
```
http://127.0.0.1:5000
```

### 4. Network Access (Phone / Other Devices on Same Wi-Fi)

To view the dashboard from other devices on your local network:
1. In `app.py`, set:
   ```python
   HOST = "0.0.0.0"
   ```
2. Find your local IP address (`ipconfig` on Windows, e.g. `192.168.1.50`).
3. Open `http://<YOUR_IP>:5000` on your phone or tablet.
