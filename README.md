# Automatic Number Plate Recognition (ANPR) System

A lightweight, CPU-friendly Automatic Number Plate Recognition system built with OpenCV and Tesseract OCR. This project implements a complete pipeline for detecting, aligning, reading, and logging vehicle number plates from live camera feed.

## 📋 Pipeline Overview

The system follows a strict three-stage pipeline with additional validation and persistence layers:

Camera → Detection → Alignment → OCR → Validation → Temporal Confirmation → CSV Logging

### Pipeline Stages

1. **Detection** (`detect.py`) - Locates plate-like regions using contour analysis and geometric filtering
2. **Alignment** (`align.py`) - Corrects perspective distortion and normalizes plate to fixed size (450×140)
3. **OCR** (`ocr.py`) - Extracts text using Tesseract with character whitelist
4. **Validation** (`validate.py`) - Validates extracted text against Rwanda plate pattern (AAA999A)
5. **Temporal Confirmation** (`temporal.py`) - Confirms plate across multiple frames using majority voting
6. **Logging** - Saves confirmed plates to CSV with timestamps

## 🚀 Getting Started

### Prerequisites

- Python 3.6+
- Tesseract OCR engine
- Webcam

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/amani-patrick/CarNumber_Plate_detection
   cd CarNumber_Plate_detection
   ```

2. **Create and activate virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Install Tesseract OCR**

   _macOS:_

   ```bash
   brew install tesseract
   ```

   _Ubuntu/Debian:_

   ```bash
   sudo apt update
   sudo apt install tesseract-ocr
   ```

   _Windows:_
   Download from https://github.com/UB-Mannheim/tesseract/wiki

5. **Verify camera works**

   ```bash
   python src/camera.py
   ```

   Press 'q' to quit the camera preview.

## 📁 Project Structure

```
anpr-project/
│
├── src/
│   ├── camera.py
│   ├── detect.py
│   ├── align.py
│   ├── ocr.py
│   ├── validate.py
│   └── temporal.py
│
├── data/
│   └── plates.csv
│
├── requirements.txt
└── README.md
```

## 🎯 Usage

Run each module incrementally:

1. **Test detection**

   ```bash
   python src/detect.py
   ```

2. **Test alignment**

   ```bash
   python src/align.py
   ```

3. **Test OCR**

   ```bash
   python src/ocr.py
   ```

4. **Test validation**

   ```bash
   python src/validate.py
   ```

5. **Run full pipeline**

   ```bash
   python src/temporal.py
   ```

Press 'q' to quit any script.

View logs:

```bash
cat data/plates.csv
```

## 🔧 Configuration

| Parameter   | Value | Description              |
| ----------- | ----- | ------------------------ |
| MIN_AREA    | 600   | Minimum contour area     |
| AR_MIN      | 2.0   | Min aspect ratio         |
| AR_MAX      | 8.0   | Max aspect ratio         |
| W_OUT       | 450   | Output width             |
| H_OUT       | 140   | Output height            |
| BUFFER_SIZE | 5     | Frame buffer             |
| COOLDOWN    | 10    | Seconds before re-saving |

## 🧪 Testing

- Rwanda plates (AAA999A)
- Different lighting conditions
- Various angles
- Multiple vehicle types

## 📝 Requirements

```
opencv-python==4.8.1.78
numpy==1.24.3
pytesseract==0.3.10
pandas==2.0.3
```
