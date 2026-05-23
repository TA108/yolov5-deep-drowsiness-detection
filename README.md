# YOLOv5 Deep Drowsiness Detection

A real-time deep learning–based drowsiness detection system built using YOLOv5, PyTorch, and OpenCV. This project includes dataset collection, image labeling, custom model training, image inference, and real-time webcam detection.

---

## Features

- Real-time drowsiness detection using webcam
- Custom dataset creation (`awake`, `drowsy`)
- Image annotation using LabelImg
- YOLOv5 custom training
- Image testing and webcam inference
- GPU acceleration support using CUDA

---

## Project Structure

```text
yolov5-deep-drowsiness-detection/
│
├── dataset/
│   ├── images/        # Empty folder (add collected images here)
│   └── labels/        # Empty folder (add YOLO labels here)
│
├── environment.yml
│
├── dataset.yml
│
├── object_detection_yolov5.ipynb
│
├── train_drowsiness_detection.ipynb
│
├── realtime_drowsiness_detection.ipynb
│
└── README.md
```

Note:
- `dataset/images` and `dataset/labels` are intentionally kept empty.
- Add your own collected images and generated labels.
- Move `dataset.yml` into the `yolov5/` folder after cloning YOLOv5.

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

Run:

```bash
git clone https://github.com/ultralytics/yolov5
```

Move:

```text
dataset.yml
```

into:

```text
yolov5/
```

Result:

```text
yolov5/
├── dataset.yml
├── train.py
├── ...
```

---

## Notebook Overview

### 1. object_detection_yolov5.ipynb

Use this notebook to verify that YOLOv5 installation is working.

Includes:

- Loading pretrained YOLOv5
- Image inference
- Webcam inference

Run:

```python
model = torch.hub.load(
    'ultralytics/yolov5',
    'yolov5s',
    pretrained=True
)
```

Expected:
- Detect objects on sample image
- Open webcam detection window

---

### 2. train_drowsiness_detection.ipynb

Use this notebook to train a custom drowsiness detection model.

Pipeline:

1. Clone YOLOv5
2. Collect images from webcam
3. Create:
   - `awake`
   - `drowsy`
4. Label images using LabelImg
5. Train YOLOv5
6. Test trained model

Training:

```bash
python train.py \
--img 320 \
--batch 20 \
--epochs 500 \
--data dataset.yml \
--weights yolov5s.pt \
--device 0 \
--workers 2
```

Model output:

```text
yolov5/runs/train/exp*/weights/
```

Update:

```python
path = r"yolov5\runs\train\expX\weights\best.pt"
```

before testing.

---

### 3. realtime_drowsiness_detection.ipynb

Run trained model for live detection.

Before running:

Move trained experiment folder:

```text
yolov5/runs/train/expX
```

to:

```text
project_root/expX
```

Update:

```python
model = torch.hub.load(
    'ultralytics/yolov5',
    'custom',
    path=r'expX\weights\last.pt',
    force_reload=True
)
```

Run notebook to start webcam inference.

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

Directory:

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

This project is for educational and research purposes.