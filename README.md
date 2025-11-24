# Thermal Human Detection using YOLOv5n 🌡️🚶‍♂️

![Status](https://img.shields.io/badge/Status-Completed-success)
![Model](https://img.shields.io/badge/Model-YOLOv5n-blue)
![Domain](https://img.shields.io/badge/Domain-Computer_Vision-orange)

> **University Project - Computer Vision**

## 📖 Overview

This project focuses on **detecting humans in thermal imagery** using the **YOLOv5n (Nano)** model. Thermal imaging is essential for scenarios where visible light is insufficient, such as nighttime surveillance, search and rescue (SAR) missions in smoke or harsh weather, and driver assistance systems.

We trained a lightweight object detection model to achieve high accuracy suitable for resource-constrained environments like Google Colab or embedded systems.

📄 **[Read the Full Project Report (PDF)](./compvi_final-report.pdf)**

## 📊 Key Results

Our model demonstrates superior performance, even outperforming comparable YOLOv8 benchmarks from related studies.

| Metric | Value |
| :--- | :--- |
| **Precision** | **99.1%** |
| **Recall** | **99.1%** |
| **mAP@0.5** | **99.4%** |
| **mAP@0.5-0.95** | **66.2%** |
| **Inference Time** | **0.123s / image** (Mean) |

**Test Set Performance (1,201 images):**
* **F1-score:** 0.9983
* **Accuracy:** 99.8%
* **Precision (Human class):** 1.00

## 📂 Dataset & Preprocessing

* **Source:** Inspired by the **UNIRI-TID** dataset (University of Rijeka Thermal Image Dataset).
* **Format:** Grayscale thermal images simulating real-world conditions (fog, rain, night).
* **Preprocessing Pipeline:**
    1.  Mount data and clean corrupted images/labels.
    2.  Integrity checks for valid labels.
    3.  **Split Ratio:** 70% Training / 20% Validation / 10% Testing.
    4.  Generate `data.yaml` configuration.

## 🛠️ Model & Training Configuration

We utilized **YOLOv5n**, the smallest and fastest variant in the YOLOv5 family.

### Training Hyperparameters
The model was trained for **60 epochs** with a batch size of **16** on **640x640** images.

| Parameter | Value | Reason |
| :--- | :--- | :--- |
| **Optimizer** | SGD | Momentum = 0.937 |
| **Learning Rate** | lr0=0.01, lrf=0.1 | Standard for lightweight training |
| **IoU Threshold** | 0.2 | Helps detect small/distant human figures |
| **Anchor Threshold** | 4.0 | Loose anchor assignment for diverse object sizes |
| **Warmup Epochs** | 3.0 | Prevents gradient instability early in training |

### Data Augmentation Strategy
We employed robust augmentations to improve generalization, contrasting with the lighter augmentations used in related YOLOv8 studies.

* **Mosaic (1.0) & Mixup (0.1):** Combines images to increase scene diversity.
* **Copy-Paste (0.1):** Simulates occlusion.
* **Perspective (0.0005):** Adds slight geometric distortion.
* **HSV Adjustments:** Simulates sensor noise and lighting variations.

## 📈 Performance Analysis

### Comparison with State-of-the-Art (YOLOv8)
We compared our YOLOv5n model against Rizk & Bayad's YOLOv8 models trained on the same domain. Despite being an older architecture, our tuned **YOLOv5n outperformed YOLOv8n, YOLOv8m, and even YOLOv8x** in mAP50 metrics on similar tasks.

* **Our YOLOv5n:** mAP50 = **0.994**
* *YOLOv8n (Reference):* mAP50 = 0.913
* *YOLOv8x (Reference):* mAP50 = 0.946

### Confusion Matrix
The model achieved a **perfect separation** between the "human" class and the background, with 0 False Positives and 0 False Negatives on the validation set.

---
*This repository contains the project report, dataset configuration, and parameter files used for the study.*
