# Model Weights

The final model used in this project is:

```text
best.pt
```

This model corresponds to the YOLOv11n detector trained for the `human` class on the curated PROJECT dataset.

The trained model weights are **not included in this repository by default**. They may be shared upon reasonable academic request.

Contact:

```text
muali.yldrm@gmail.com
```

## Available Model Formats

| Format | Status |
|---|---|
| PyTorch `.pt` | Available upon reasonable academic request |
| ONNX `.onnx` | Exported, not included in this repository by default |
| TensorRT `.engine` | Generated on the Jetson Nano deployment environment |

## Notes

The TensorRT engine was generated on the Jetson Nano deployment environment.

TensorRT engine files are highly dependent on the target hardware, JetPack version, CUDA version, TensorRT version, and DeepStream environment. For this reason, the `.engine` file is not included in this repository.

Users who want to reproduce the deployment should generate the TensorRT engine on their own Jetson device.

This model was trained using Ultralytics YOLO tooling. Usage of the trained model may be subject to Ultralytics licensing terms depending on the intended use case.
