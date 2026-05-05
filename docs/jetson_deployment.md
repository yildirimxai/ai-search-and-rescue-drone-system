# Jetson Nano Deployment Notes

This document summarizes the Jetson Nano deployment environment used for the real-time UAV-based human detection system.

The deployment pipeline was tested on the Jetson Nano environment using the final YOLOv11n model trained for the `human` class.

## Hardware Environment

| Component | Information |
|---|---|
| Edge device | NVIDIA Jetson Nano 4GB Developer Kit |
| Carrier board | Waveshare carrier board |
| Camera | IMX477 |
| UAV platform | Holybro X500 V2 |
| Flight controller | Pixhawk 6C |
| GPS | M10 GPS |
| Battery | Profuse 8000 mAh 65C 4S LiPo |
| Ground station viewer | VLC Player |

## Software Environment

| Component | Version / Status |
|---|---|
| JetPack | 4.6.4 |
| DeepStream SDK | 6.0.1 |
| TensorRT | Exported on the Jetson Nano deployment environment |
| RTSP streaming | Tested |
| FPS / latency measurement | Not formally measured |

## Deployment Workflow

The trained YOLOv11n model was exported and deployed on the Jetson Nano environment.

The deployment workflow was:

```text
YOLOv11n best.pt
        │
        ▼
ONNX export
        │
        ▼
TensorRT engine generation on Jetson Nano
        │
        ▼
DeepStream-based inference pipeline
        │
        ▼
RTSP output
        │
        ▼
Ground station monitoring via VLC Player
```

## RTSP Ground Station Monitoring

The processed video stream was transmitted from the Jetson Nano to the ground station using RTSP.

The ground station stream was viewed using:

```text
VLC Player
```

No formal FPS or end-to-end latency measurement was recorded. Therefore, this repository does not report a numerical FPS or latency value.

## TensorRT Engine Note

The TensorRT `.engine` file was generated directly on the Jetson Nano deployment environment.

TensorRT engine files are highly dependent on:

- Jetson hardware
- JetPack version
- CUDA version
- TensorRT version
- DeepStream version
- Model input size
- Precision mode

For this reason, the TensorRT engine file is not included in this repository by default.

Users who want to reproduce the deployment should generate the TensorRT engine on their own Jetson device.

## Deployment Scope

This repository documents the deployment workflow used in the project.

The original DeepStream configuration files are not included in the current repository version. Therefore, this document should be considered a deployment note rather than a complete plug-and-play DeepStream package.
