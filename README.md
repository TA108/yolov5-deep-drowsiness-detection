# YOLOv5 Deep Drowsiness Detection

A real-time deep learning–based drowsiness detection system built using YOLOv5, PyTorch, and OpenCV. This project includes dataset collection, image labeling, custom model training, image inference, and real-time webcam detection.

---

## Features

- Real-time drowsiness detection using webcam
- Custom dataset creation (`awake`, `drowsy`)
- Image annotation using LabelImg
- YOLOv5 custom model training
- Image testing and webcam inference
- GPU acceleration using CUDA

---

## Project Structure

```text
yolov5-deep-drowsiness-detection/
│
├── dataset/
│   ├── images/                # Empty (add collected images)
│   └── labels/                # Empty (add generated YOLO labels)
│
├── environment.yml
├── dataset.yml
│
├── exp7/                      # Optional pre-trained experiment folder
│   └── weights/
│       ├── best.pt
│       └── last.pt
│
├── object_detection_yolov5.ipynb
├── train_drowsiness_detection.ipynb
├── realtime_drowsiness_detection.ipynb
│
└── README.md
```

### Notes

- `dataset/images` and `dataset/labels` are intentionally empty.
- Add your own images and labels before training.
- `dataset.yml` must remain in the project root.
- During training, YOLOv5 reads it using:

```text
../dataset.yml
```

- `exp7` is provided as a pre-trained experiment and can be used directly for testing without retraining.

---

## Installation

Clone repository:

```bash
git clone https://github.com/TA108/yolov5-deep-drowsiness-detection.git
cd yolov5-deep-drowsiness-detection
```

Create environment:

```bash
conda env create -f environment.yml
conda activate <environment_name>
```

---

## Clone YOLOv5

Clone YOLOv5 inside project directory:

```bash
git clone https://github.com/ultralytics/yolov5
```

Result:

```text
yolov5-deep-drowsiness-detection/
│
├── dataset.yml
├── yolov5/
│   ├── train.py
│   └── ...
```

---

# Notebook Overview

## 1. object_detection_yolov5.ipynb

Use this notebook to verify that YOLOv5 installation is working correctly.

Includes:

- Loading pretrained YOLOv5
- Image object detection
- Webcam object detection

Example:

```python
model = torch.hub.load(
    'ultralytics/yolov5',
    'yolov5s',
    pretrained=True
)
```

Expected:

- Detect objects in sample image
- Open live webcam detection

---

## 2. train_drowsiness_detection.ipynb

Train a custom drowsiness detection model.

Pipeline:

### Step 1 — Clone YOLOv5

```bash
git clone https://github.com/ultralytics/yolov5
```

### Step 2 — Collect Images

Collect images for:

```text
awake
drowsy
```

Images are saved to:

```text
dataset/images
```

### Step 3 — Label Images

Install LabelImg:

```bash
git clone https://github.com/HumanSignal/labelImg.git

pip install pyqt5 lxml --upgrade

cd labelImg

pyrcc5 -o libs/resources.py resources.qrc
```

Generate labels and store in:

```text
dataset/labels
```

### Step 4 — Train Model

Move into YOLOv5:

```python
%cd yolov5
```

Run:

```bash
python train.py \
    --img 320 \
    --batch 20 \
    --epochs 500 \
    --data "../dataset.yml" \
    --weights yolov5s.pt \
    --device 0 \
    --workers 2
```

Output:

```text
yolov5/runs/train/exp*/
```

Example:

```text
yolov5/runs/train/exp7/
```

### Step 5 — Test Model

Update path:

```python
path = r"yolov5\runs\train\expX\weights\best.pt"
```

Load:

```python
model = torch.hub.load(
    'ultralytics/yolov5',
    'custom',
    path=path,
    force_reload=True
)
```

---

## 3. realtime_drowsiness_detection.ipynb

Run trained model for real-time webcam detection.

### Option 1 — Use Existing Trained Model

Use provided:

```text
exp7/
```

Load:

```python
model = torch.hub.load(
    'ultralytics/yolov5',
    'custom',
    path=r'exp7\weights\last.pt',
    force_reload=True
)
```

### Option 2 — Use Your Own Training Output

Copy:

```text
yolov5/runs/train/expX
```

to:

```text
project_root/expX
```

Update:

```python
path=r'expX\weights\last.pt'
```

Run notebook.

Controls:

```text
Press Q → Exit
```

---

## Dataset

Classes:

```text
awake
drowsy
```

Structure:

```text
dataset/
├── images/
└── labels/
```

---

## Training Output

Example:

```text
yolov5/
└── runs/
    └── train/
        └── exp7/
            └── weights/
                ├── best.pt
                └── last.pt
```

---

## Technologies

- Python
- PyTorch
- YOLOv5
- OpenCV
- NumPy
- LabelImg
- Matplotlib

---

## License

This project is intended for educational and research purposes.
