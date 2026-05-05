# Training

This document summarizes the training setup used for the final YOLOv11n model in this project.

The final model was trained in **Google Colab** using an **NVIDIA A100 GPU**.

## Environment

| Component | Version / Status |
|---|---|
| Python | 3.12.12 |
| PyTorch | 2.8.0+cu126 |
| Ultralytics | 8.3.0 |
| OpenCV | 4.12 |
| Albumentations | 2.0.8 |
| Roboflow | Not used |
| Training platform | Google Colab |
| GPU | NVIDIA A100 |

## Final Model

The final selected model architecture is:

```text
YOLOv11n
```

The final trained model file is:

```text
best.pt
```

The model was trained for a single detection class:

```text
0: human
```

## Training Code

```python
from ultralytics import YOLO
import os

os.environ["WANDB_MODE"] = "disabled"

model = YOLO("yolov11n.pt")

results = model.train(
    data=str(yaml_path),
    epochs=100,
    imgsz=640,
    batch=32,
    patience=20,
    optimizer="SGD",
    lr0=0.01,
    lrf=0.01,
    weight_decay=0.0005,
    device=0,
    workers=2,
    cache=True,
    hsv_h=0.015,
    hsv_s=0.7,
    hsv_v=0.4,
    flipud=0.0,
    fliplr=0.5,
    mosaic=1.0,
    mixup=0.1,
    label_smoothing=0.0,
)
```

## Training Configuration

| Parameter | Value |
|---|---|
| Model | YOLOv11n |
| Epochs | 100 |
| Image size | 640 |
| Batch size | 32 |
| Patience | 20 |
| Optimizer | SGD |
| Initial learning rate `lr0` | 0.01 |
| Final learning rate factor `lrf` | 0.01 |
| Weight decay | 0.0005 |
| Device | GPU `0` |
| Workers | 2 |
| Cache | Enabled |
| Horizontal flip | 0.5 |
| Vertical flip | 0.0 |
| Mosaic | 1.0 |
| MixUp | 0.1 |
| Label smoothing | 0.0 |

## Final Model Performance on PROJECT Dataset

| Model | Precision | Recall | mAP@0.5 | mAP@0.5:0.95 |
|---|---:|---:|---:|---:|
| YOLOv8n | 0.8997 | 0.7953 | 0.8433 | 0.4013 |
| YOLOv11n | 0.9109 | 0.8065 | 0.8694 | 0.4481 |

## Notes

YOLOv11n was selected as the final model because it achieved higher performance than YOLOv8n on the curated PROJECT dataset.

The trained `best.pt` file is not included in this repository by default. It may be shared upon reasonable academic request.
