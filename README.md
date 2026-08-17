# Bangladeshi Vehicle Number Plate Detection using YOLOv10

This repository contains a deep learning project dedicated to detecting Bangladeshi vehicle number plates using the state-of-the-art **YOLOv10** object detection framework. 

---

## Project Overview

Vehicle license plate detection is a key component of Intelligent Transportation Systems (ITS), smart parking management, and automated toll collection. This project leverages the efficiency and accuracy of **YOLOv10** to locate and detect license plates on Bangladeshi vehicles.

### Development Roadmap
- [x] **Phase 1: License Plate Localization/Detection** (Completed)
  - Custom dataset annotation (single class: `License`).
  - Model training using YOLOv10 (specifically YOLOv10n).
  - Model validation and inference on test images.
- [/] **Phase 2: Text Extraction & Integration** (In Progress)
  - Extract Bengali characters and digits from the detected license plate (using OCR tools like EasyOCR, Tesseract, or custom CRNN).
  - Store extracted numbers in a database.
  - Visualize records dynamically on a web dashboard.

---

## Tech Stack & Dependencies

- **Framework**: [THU-MIG YOLOv10](https://github.com/THU-MIG/yolov10)
- **Runtime Environment**: Jupyter Notebook / Google Colab (with GPU support)
- **Deep Learning Library**: PyTorch & Ultralytics
- **Language**: Python 3

---

## Repository Structure

```text
├── README.md               # Project documentation (this file)
├── LICENSE                 # License information
├── data.yaml               # YOLOv10 dataset configuration file
└── yolov10_model_training_from_custom_dataset.ipynb   # Model training & inference pipeline
```

---

##  Dataset Configuration (`data.yaml`)

The dataset is structured with a single class labeled `License`:

```yaml
train: /train/images
val: /val/images
test: /test/images

nc: 1
names: ['License']
```

---

## Step-by-Step Training Pipeline

The entire training workflow is documented in [yolov10_model_training_from_custom_dataset.ipynb](file:///mnt/99629AC904A68FF9/work/vehicle_bangla_number_plate_detection_using_yolo/yolov10_model_training_from_custom_dataset.ipynb):

### 1. Environment Setup
Clone the official YOLOv10 repository and install requirements:
```bash
!git clone https://github.com/THU-MIG/yolov10.git
%cd yolov10
!pip install .
```

### 2. Download Pre-trained Weights
Download the YOLOv10 weight variants from the official assets release:
- YOLOv10 Nano (`yolov10n.pt`)
- YOLOv10 Small (`yolov10s.pt`)
- YOLOv10 Medium (`yolov10m.pt`)
- YOLOv10 Big/Large (`yolov10b.pt`, `yolov10l.pt`, `yolov10x.pt`)

### 3. Model Training
Run the training command using the CLI:
```bash
yolo task=detect mode=train epochs=75 batch=16 patience=10 plots=True model=weights/yolov10n.pt data=data.yaml
```

### 4. Running Inference
To run predictions on a new test image or screenshot:
```bash
yolo task=detect mode=predict model=runs/detect/train2/weights/best.pt conf=0.25 source=path/to/your/image.jpg save=True
```

---

## Future Work
1. **Bengali OCR Engine**: Implementing localized character segmentation and recognition optimized for Bengali fonts and number plate styles.
2. **Database Logger**: Saving recognized vehicle numbers along with timestamps and confidence scores.
3. **Web Dashboard**: Building a clean user interface to query and monitor detected vehicles.
