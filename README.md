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

import os
import urllib.request

weights_dir = os.path.join(os.getcwd(), "weights")
os.makedirs(weights_dir, exist_ok=True)

urls = [
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10n.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10n.pt)",
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10s.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10s.pt)",
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10m.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10m.pt)",
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10b.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10b.pt)",
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10x.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10x.pt)",
    "[https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10l.pt](https://github.com/jameslahm/yolov10/releases/download/v1.0/yolov10l.pt)"
]

for url in urls:
    file_name = os.path.join(weights_dir, os.path.basename(url))
    urllib.request.urlretrieve(url, file_name)
    print(f"Downloaded {file_name}")
