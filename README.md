<div align="center">

# 🎯 AI-Powered Target Recognition System

**A high-performance, real-time object and weapon detection application designed for security and surveillance.**

[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)](https://opencv.org/)
[![YOLO](https://img.shields.io/badge/YOLO-v5%2Fv8-00FFFF?style=for-the-badge&logo=ultralytics&logoColor=black)](https://ultralytics.com/)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org/)

</div>

---

## 📖 Overview

The **AI-Powered Target Recognition System** leverages state-of-the-art computer vision to detect objects and potential threats in live video streams. Utilizing the YOLO (You Only Look Once) deep learning model via Ultralytics, it provides lightning-fast inference on both local and IP cameras.

Designed with security in mind, the system automatically highlights dangerous objects (like knives and guns) and permanently logs these incidents into a local SQLite database. It features a responsive graphical user interface (GUI) built with Tkinter, enabling operators to seamlessly switch cameras, apply pseudo-thermal imaging, adjust detection confidence thresholds, and record video evidence.

---

## ✨ Key Features

- 🕵️ **Real-Time Threat Detection**: Identifies objects rapidly and highlights weapons (guns, knives) with specialized red bounding boxes.
- 📹 **Multi-Camera Support**: Seamlessly toggle between local webcams and external IP camera streams.
- 🌡️ **Pseudo-Thermal Imaging**: Apply a thermal-like JET colormap to the video stream for enhanced visibility in certain conditions.
- 💾 **Automated Logging**: Persists critical detection data (timestamps, object class, confidence score) into an SQLite database (`detections.db`).
- 📼 **Evidence Recording**: Easily record the processed live feed (with bounding boxes) and save it directly to your machine.
- 🎛️ **Interactive Dashboard**: Adjust the confidence threshold on the fly, and view live statistics such as FPS, total detections, and weapon counts.

---

## 🏗️ Architecture & Workflow

1. **Input Layer**: `cv2.VideoCapture` captures frames from the selected camera feed.
2. **Background Processing**: A dedicated Python daemon thread ingests frames into a thread-safe queue, preventing UI freezing.
3. **AI Engine**: Ultralytics YOLO models process the resized frames, leveraging CUDA/GPU acceleration when available.
4. **Analysis & Storage**: The system parses the bounding boxes and confidence scores. Threats are flagged, painted red, and written to SQLite.
5. **Presentation**: The processed frames are converted back via PIL and rendered on the Tkinter canvas, alongside real-time analytical metrics.

---

## 💻 Tech Stack

- **Frontend / GUI**: Tkinter, `ttk`
- **Computer Vision**: OpenCV (`opencv-python`), Pillow (PIL)
- **AI / Deep Learning**: Ultralytics (YOLOv5, YOLOv8)
- **Data Persistence**: SQLite3
- **Data Processing**: NumPy

---

## 🚀 Getting Started

Follow these instructions to set up the project locally.

### Prerequisites

- Python 3.8 or higher installed on your system.
- (Optional but recommended) A CUDA-enabled NVIDIA GPU for accelerated AI inference.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/AI-Powered-Target-Recognition-System.git
   cd AI-Powered-Target-Recognition-System
   ```

2. **Install the required dependencies:**
   ```bash
   pip install -r Requirement.txt
   ```

3. **Configure the YOLO Models:**
   Ensure your YOLO weights (e.g., `yolov5x6u.pt` or `yolov8n.pt`) are placed securely in the `models/` directory.

### Running the Application

Execute the main script to launch the dashboard:

```bash
python scripts/target_recognition.py
```

---

## 📂 Project Structure

```text
📦 AI-Powered-Target-Recognition-System
├── 📁 scripts/
│   └── 📄 target_recognition.py   # Main application and GUI logic
├── 📁 models/
│   ├── 📄 yolov8n.pt              # YOLOv8 Nano model weights
│   └── 📄 yolo11l.pt              # YOLO11 Large model weights
├── 📁 output/                     # Auto-generated video recordings (.avi)
├── 📄 Requirement.txt             # Project dependencies
├── 📄 detections.db               # SQLite log database (auto-generated)
├── 📄 error.log                   # Runtime error logging
└── 📄 README.md                   # Project documentation
```

---

## 🛡️ License

This project is licensed under the MIT License - see the LICENSE file for details.
