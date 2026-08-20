# AI-Powered Target Recognition System

## 📝 Project Description
The **AI-Powered Target Recognition System** is a real-time object and weapon detection application. Built with Python, it utilizes the YOLO (You Only Look Once) deep learning model through the Ultralytics library to detect objects in live video streams. The system is designed to provide high-performance computer vision capabilities, featuring a graphical user interface (GUI) for easy interaction, multiple camera support, pseudo-thermal imaging, and automated incident logging into a SQLite database. 

It is specifically tailored to identify potential threats (like knives and guns), highlight them, and securely log the detection events for security and surveillance purposes.

---

## 🏗️ Workflow & Architecture

The application is structured to handle video processing and UI rendering concurrently to maintain a smooth user experience.

1. **User Interface (UI) Layer**: Built using Tkinter, it provides the main dashboard. It displays the live video feed, real-time statistics (FPS, total detections, weapon detections, average confidence), and controls (Threshold slider, Camera switch, Thermal mode toggle, Recording).
2. **Video Capture & Processing**: OpenCV captures frames from either the local webcam or an IP camera. The frames are placed into a thread-safe queue.
3. **AI Inference Engine (YOLO)**: A background worker thread consumes frames from the queue, resizes them, and passes them to the YOLO model (running on CUDA/GPU if available) for object detection.
4. **Threat Detection & Highlighting**: Bounding boxes are drawn around detected objects. If a weapon (e.g., "gun", "knife") is detected, the bounding box is colored red and a warning is logged.
5. **Data Persistence**: When an object is detected, relevant metadata (timestamp, camera index, object class, confidence score, weapon flag) is saved into a local SQLite database (`detections.db`).
6. **Video Recording & Effects**: The system can apply a pseudo-thermal (JET colormap) effect to the video stream and optionally record the processed output to an `.avi` file in the `output/` directory.

---

## 🛠️ Technology Stack

- **Programming Language**: Python 3
- **Computer Vision**: OpenCV (`opencv-python`)
- **Deep Learning Model**: Ultralytics YOLOv5 / YOLOv8
- **GUI Framework**: Tkinter & `ttk`
- **Image Processing**: Pillow (PIL)
- **Database**: SQLite3 (built-in Python library)
- **Numerical Computing**: NumPy

---

## 🚀 Features

- **Real-time Object Detection**: Uses state-of-the-art YOLO models for fast and accurate inference.
- **Weapon Identification**: Specifically highlights weapons and logs them securely.
- **Multi-Camera Support**: Seamlessly switch between built-in webcams and network IP cameras.
- **Pseudo-Thermal Mode**: Applies a thermal-like colormap for different viewing perspectives.
- **Video Recording**: Record and save the processed video feed with bounding boxes.
- **Interactive UI**: Adjust detection confidence thresholds on the fly and monitor FPS and detection statistics.
- **SQLite Logging**: Keeps a persistent record of all detections with timestamps and confidence scores.

---

## ⚙️ Installation & Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/AI-Powered-Target-Recognition-System.git
   cd AI-Powered-Target-Recognition-System
   ```

2. **Install dependencies**:
   Make sure you have Python 3.8+ installed. Run the following command to install required packages:
   ```bash
   pip install -r Requirement.txt
   ```

3. **Download YOLO Models**:
   Ensure you have a YOLO model (e.g., `yolov5x6u.pt` or `yolov8n.pt`) placed inside the `models/` directory.

4. **Run the Application**:
   ```bash
   python scripts/target_recognition.py
   ```

---

## 📂 Project Structure

```text
AI-Powered-Target-Recognition-System/
├── scripts/
│   └── target_recognition.py   # Main application script
├── models/
│   ├── yolov8n.pt              # YOLOv8 Nano model weights
│   └── yolo11l.pt              # YOLO11 Large model weights
├── Documentations/             # Additional project docs
├── output/                     # Saved video recordings (auto-generated)
├── Requirement.txt             # Python dependencies
├── detections.db               # SQLite database (auto-generated)
├── error.log                   # System error logs
└── README.md                   # Project documentation
```

---

## 🛡️ License

This project is open-source and available under the MIT License.
