# Dataset

This project uses a curated dataset referred to as the **PROJECT dataset**.

The PROJECT dataset was created by selecting, filtering, cleaning, and reorganizing samples from two publicly available search-and-rescue-oriented datasets:

| Dataset | Link |
|---|---|
| SARD — Search and Rescue Dataset | https://www.kaggle.com/datasets/nikolasgegenava/sard-search-and-rescue |
| WiSARD — Wilderness Search and Rescue Dataset | https://sites.google.com/uw.edu/wisard/ |
| WiSARD Paper | https://arxiv.org/abs/2309.04453 |

## PROJECT Dataset

The PROJECT dataset is not a separate dataset collected from scratch. It is a task-specific curated dataset created for this UAV-based search-and-rescue human detection system.

The original SARD and WiSARD datasets are publicly available from their official sources. In this project, relevant RGB images were selected from these datasets and reorganized according to the target search-and-rescue scenario.

The curated PROJECT dataset is not directly redistributed in this repository. However, researchers or students who would like to reproduce the experiments or examine the curated version can contact the author.

Contact:

```text
muali.yldrm@gmail.com
```

## Dataset Split

| Split | Images |
|---|---:|
| Train | 13,856 |
| Validation | 3,959 |
| Test | 1,979 |
| Total | 19,794 |

## Class Definition

The dataset uses a single detection class:

```text
0: human
```

## Dataset Preparation Summary

The dataset preparation process included:

- Combining SARD and selected WiSARD RGB samples
- Excluding thermal/LWIR images because the deployed UAV system uses an RGB camera
- Selecting images relevant to aerial search-and-rescue scenarios
- Filtering samples according to target visibility and scenario relevance
- Checking image-label matching
- Validating YOLO-format annotations
- Removing invalid or unsuitable samples
- Creating train, validation, and test splits
- Applying augmentation only during the training process

## Notes

The dataset was prepared for a real-time UAV-based human detection system using an onboard RGB camera. Therefore, thermal images from WiSARD were not included in the final PROJECT dataset.

The purpose of the PROJECT dataset is to improve model generalization under aerial search-and-rescue conditions such as altitude variation, background complexity, small target scale, and partial visibility.
