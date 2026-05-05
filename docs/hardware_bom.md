# Hardware Bill of Materials

This document lists the main hardware components used in the AI-powered UAV system for search-and-rescue human detection.

The system was designed as a manually operated UAV platform with an independent onboard AI perception subsystem. The flight-control system and the AI system are separated from each other for safety and modularity.

## UAV Platform and Flight Control

| Component | Model / Specification | Quantity | Role |
|---|---|---:|---|
| UAV frame | Holybro X500 V2 | 1 | Main quadcopter platform |
| Flight controller | Pixhawk 6C | 1 | Flight stabilization and motor control |
| Firmware | PX4 | 1 | Flight-control firmware |
| Ground control software | QGroundControl | 1 | Flight telemetry and manual operation interface |
| GPS module | M10 GPS | 1 | Positioning and navigation support |
| Telemetry radio | 433 MHz telemetry module | 1 set | UAV-ground station telemetry communication |

## Propulsion System

| Component | Model / Specification | Quantity | Role |
|---|---|---:|---|
| Brushless motor | Holybro 2216 KV920 | 4 | Propulsion |
| ESC | BLHeli_S 20A | 4 | Motor speed control |
| Power distribution board | PDB | 1 | Power distribution to ESCs |
| Propellers | CW/CCW propellers | 4 | Lift generation |

## Onboard AI and Imaging System

| Component | Model / Specification | Quantity | Role |
|---|---|---:|---|
| Edge AI computer | NVIDIA Jetson Nano 4GB Developer Kit | 1 | Onboard AI inference |
| Carrier board | Waveshare carrier board | 1 | Jetson Nano carrier interface |
| Camera | IMX477 | 1 | RGB image acquisition |
| AI model | YOLOv11n | 1 | Human detection model |

## Power System

| Component | Model / Specification | Quantity | Role |
|---|---|---:|---|
| Main battery | Profuse 8000 mAh 65C 4S LiPo | 1 | Main power source |
| Power module | Holybro PM02 | 1 | Pixhawk power and battery monitoring |
| Voltage regulator | 5A UBEC | 1 | Dedicated regulated power supply for Jetson Nano |

## RC Communication System

| Component | Model / Specification | Quantity | Role |
|---|---|---:|---|
| RC transmitter | FrSky Taranis QX7 ACCESS | 1 | Manual UAV control |
| RC receiver | FrSky XM+ | 1 | SBUS command input to Pixhawk |
| RC protocol | SBUS | 1 | Receiver-to-flight-controller communication |

## Ground Station

| Component | Model / Specification | Role |
|---|---|---|
| Ground station computer | Laptop / PC | Monitoring and control |
| Flight monitoring software | QGroundControl | UAV telemetry and flight status monitoring |
| Video monitoring software | VLC Player | RTSP stream viewing |

## System-Level Notes

- The UAV is manually operated by the RC pilot.
- The Jetson Nano AI subsystem does not send control commands to the Pixhawk flight controller.
- The AI subsystem is used only for real-time human detection and operator decision support.
- The processed video stream was monitored on the ground station via RTSP using VLC Player.
- The Jetson Nano was powered through a dedicated 5A UBEC to reduce the risk of voltage instability during inference.
