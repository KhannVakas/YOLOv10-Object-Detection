# YOLOv10-Object-Detection

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-Optimized-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Kaggle](https://img.shields.io/badge/Environment-Kaggle%20%7C%20Jupyter-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)

A streamlined, end-to-end pipeline for executing state-of-the-art YOLOv10 object detection within Kaggle or Jupyter Notebook environments. This repository automates the environment setup, multi-scale weight acquisition, and inference execution for rapid prototyping and computer vision research.

## 📑 Table of Contents
- [Project Overview](#-project-overview)
- [Features](#-features)
- [Installation & Setup](#-installation--setup)
- [Usage Guide](#-usage-guide)
- [Model Scales Reference](#-model-scales-reference)
- [Author](#-author)

## 🚀 Project Overview

This project provides a plug-and-play solution for testing and deploying YOLOv10 models. It handles everything from cloning the official repository and installing dependencies to circumventing strict PyTorch checkpoint loading policies and visualizing bounding box predictions inline. 

It is highly suitable for researchers and developers looking to quickly evaluate YOLOv10's performance on custom images without manual configuration overhead.

## ✨ Features
*   **Automated Environment Setup:** Clones the official `THU-MIG/yolov10` repository and installs requirements silently.
*   **Multi-Scale Model Acquisition:** A modular Python script downloads pre-trained weights for all YOLOv10 variants (Nano to Extra-Large) directly from GitHub releases.
*   **Seamless Data Ingestion:** Utilizes `gdown` for direct image fetching from external cloud storage (e.g., Google Drive).
*   **Safe Checkpoint Loading:** Configures PyTorch environment variables (`TORCH_FORCE_NO_WEIGHTS_ONLY_LOAD=1`) to ensure smooth model execution and bypass security blocks.
*   **Instant Visualization:** Renders detection results inline via IPython for immediate evaluation.

## 🛠️ Installation & Setup

This pipeline is designed to be executed sequentially in a Jupyter/Kaggle notebook with GPU acceleration enabled.

### 1. Clone & Install Dependencies
First, clone the core architecture and install the required packages:

```bash
!git clone [https://github.com/THU-MIG/yolov10.git](https://github.com/THU-MIG/yolov10.git)
%cd yolov10
!pip install -q .
```

### 📩 Download Pre-trained Weights

Run the following Python script to automatically create a weights directory and fetch all model scales for comparative testing:

```bash
import os
import urllib.request

weights_dir = os.path.join(os.getcwd(), "weights")
os.makedirs(weights_dir, exist_ok=True)

urls = [
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10n.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10n.pt)",
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10s.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10s.pt)",
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10m.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10m.pt)",
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10b.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10b.pt)",
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10x.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10x.pt)",
    "[https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10l.pt](https://github.com/THU-MIG/yolov10/releases/download/v1.1/yolov10l.pt)"
]

for url in urls:
    file_name = os.path.join(weights_dir, os.path.basename(url))
    urllib.request.urlretrieve(url, file_name)
    print(f"Downloaded {file_name}")
```

### 🎯 Usage Guide

Fetch Test Data
Download your target image into the working directory. (Replace the file ID with your own if testing different images).

```bash
!gdown "10Rz_Ww_v8D_O4pG1q6xP_6s_v9C0oK72" -O image1.jpg
```

Run Inference
Configure PyTorch settings and execute the prediction via the CLI. The example below uses the highly accurate Extra-Large (yolov10x.pt) model:

```bash
%env TORCH_FORCE_NO_WEIGHTS_ONLY_LOAD=1
!yolo predict model=/kaggle/working/yolov10/weights/yolov10x.pt source=/kaggle/working/yolov10/image1.jpg save=True
```

Visualize Results
Display the processed image with bounding boxes directly in the notebook:

```bash
import IPython
IPython.display.Image("runs/detect/predict/image1.jpg", width=600)

```

### 📊 Model Scales Reference

This repository downloads all standard model sizes to allow testing the trade-off between inference speed and precision.

* N (Nano): Fastest inference, designed for resource-constrained edge devices.
* S (Small) / M (Medium): Excellent balance of speed and accuracy for standard applications.
* B (Base) / L (Large): High accuracy tailored for server-side processing and complex datasets.
* X (Extra-Large): Maximum precision and feature extraction capability; ideal for robust academic research and benchmarking.

### 👨‍💻 Author
**Waqas Ahmad**
Artificial Intelligence Researcher
Focusing on Medical Computer Vision, Explainable AI (XAI), and Deep Learning architectures.

