# System Architecture
<div align="center">

<img src="./assets/diagram.png" alt="System Architecture" width="900">

<br>

<em>Overall UAV system architecture showing the relationship between the Holybro X500 V2 UAV platform, Jetson Nano onboard AI unit, RTSP-based video and detection stream, and the ground control station.</em>

</div>
This document describes the overall system architecture of the AI-powered UAV system developed for rapid human detection in search-and-rescue scenarios.

The system is designed as a manually operated UAV platform with an independent onboard AI perception subsystem. The AI subsystem provides real-time visual decision support to the operator but does not control the UAV.

## High-Level Architecture

```text
IMX477 RGB Camera
        │
        ▼
NVIDIA Jetson Nano 4GB
        │
        ├── YOLOv11n human detection
        ├── ONNX / TensorRT deployment workflow
        ├── DeepStream-based video processing
        └── RTSP stream output
        │
        ▼
Ground Station
        │
        ├── VLC Player for video monitoring
        └── QGroundControl for flight telemetry
```

The flight-control system operates independently:

```text
RC Operator
        │
        ▼
FrSky Taranis QX7 ACCESS
        │
        ▼
FrSky XM+ Receiver
        │
        ▼
Pixhawk 6C Flight Controller
        │
        ▼
ESCs + Motors
```

## Design Principle

The most important design decision in this project is the separation of:

1. **Flight control**
2. **AI-based perception**

The Jetson Nano does not send control commands to the Pixhawk 6C. This separation ensures that the AI detection pipeline cannot interfere with flight safety.

The AI system only detects candidate human targets and sends the annotated video stream to the ground station. The final decision remains with the human operator.

## Subsystems

## 1. UAV Flight Platform

The UAV platform is based on the Holybro X500 V2 quadcopter frame.

Main flight-related components:

| Component | Role |
|---|---|
| Holybro X500 V2 | Main UAV frame |
| Pixhawk 6C | Flight stabilization and motor control |
| PX4 firmware | Flight-control software |
| FrSky Taranis QX7 ACCESS | Manual RC control |
| FrSky XM+ | RC receiver |
| M10 GPS | Positioning support |
| 433 MHz telemetry | Telemetry communication |
| QGroundControl | Flight monitoring and configuration |

The UAV is manually operated by the pilot. Autonomous navigation was not included in the scope of this repository.

## 2. Onboard AI Perception Subsystem

The onboard AI subsystem is responsible for real-time human detection.

Main AI-related components:

| Component | Role |
|---|---|
| NVIDIA Jetson Nano 4GB Developer Kit | Onboard inference device |
| Waveshare carrier board | Jetson Nano carrier interface |
| IMX477 camera | RGB image acquisition |
| YOLOv11n | Human detection model |
| TensorRT | Inference optimization on Jetson |
| DeepStream | Video processing and streaming pipeline |
| RTSP | Video transmission to ground station |

The camera stream is processed on the Jetson Nano. The trained YOLOv11n model detects humans and produces bounding boxes with confidence scores.

## 3. Ground Station

The ground station is used for both UAV monitoring and AI output monitoring.

| Tool | Purpose |
|---|---|
| QGroundControl | Flight telemetry and UAV configuration |
| VLC Player | RTSP video stream monitoring |

The annotated video stream is viewed through VLC Player over RTSP.

## Data Flow

The perception data flow is:

```text
Camera frame capture
        │
        ▼
Jetson Nano image processing
        │
        ▼
YOLOv11n human detection
        │
        ▼
Bounding box and confidence overlay
        │
        ▼
RTSP output
        │
        ▼
Ground station monitoring
```

The flight-control data flow is:

```text
RC transmitter
        │
        ▼
RC receiver
        │
        ▼
Pixhawk 6C
        │
        ▼
ESCs
        │
        ▼
Motors
```

## AI and Flight-Control Separation

The AI subsystem is intentionally isolated from the flight-control loop.

```text
Jetson Nano  ─X─>  Pixhawk control commands
```

There is no direct command authority from the Jetson Nano to the Pixhawk 6C.

This architecture was selected to:

- Preserve manual flight safety
- Keep the AI system modular
- Prevent perception errors from affecting flight behavior
- Allow the operator to remain responsible for mission decisions
- Support future upgrades without modifying the flight-control system

## Deployment Workflow

The final YOLOv11n model was trained in Google Colab and deployed on Jetson Nano.

```text
Google Colab training
        │
        ▼
best.pt
        │
        ▼
ONNX export
        │
        ▼
TensorRT engine generation on Jetson Nano
        │
        ▼
DeepStream-based processing
        │
        ▼
RTSP stream to ground station
```

The TensorRT engine was generated on the Jetson Nano deployment environment.

## Field Validation

The system was tested using real UAV flight footage. Field tests included different altitude and visibility conditions.

The goal of field validation was to observe whether the trained model could detect humans in realistic aerial scenes and provide useful visual feedback to the operator.

Formal FPS or end-to-end latency measurements were not recorded. Therefore, this repository does not report a numerical FPS or latency value.

## Scope of This Repository

This repository focuses on:

- Dataset preparation documentation
- YOLOv8n and YOLOv11n model comparison
- Final YOLOv11n training setup
- UAV hardware architecture
- Jetson Nano deployment notes
- Field test documentation
- RTSP-based monitoring workflow

This repository does not currently include the original DeepStream configuration files.
