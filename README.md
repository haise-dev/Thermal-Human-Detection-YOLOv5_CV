# Thermal Human Detection using YOLOv5n 🌡️🚶‍♂️

![Status](https://img.shields.io/badge/Status-Completed-success)
![Model](https://img.shields.io/badge/Model-YOLOv5n-blue)
![Domain](https://img.shields.io/badge/Domain-Computer_Vision-orange)

> **University Project - Computer Vision**
## 📖 Overview

[cite_start]This project focuses on **detecting humans in thermal imagery** using the **YOLOv5n (Nano)** model[cite: 1973]. [cite_start]Thermal imaging is essential for scenarios where visible light is insufficient, such as nighttime surveillance, search and rescue (SAR) missions in smoke or harsh weather, and driver assistance systems[cite: 1971, 1972].

[cite_start]We trained a lightweight object detection model to achieve high accuracy suitable for resource-constrained environments like Google Colab or embedded systems[cite: 2035].

📄 **[Read the Full Project Report (PDF)](./compvi_final-report.pdf)**

## 📊 Key Results

[cite_start]Our model demonstrates superior performance, even outperforming comparable YOLOv8 benchmarks from related studies[cite: 2119].

| Metric | Value |
| :--- | :--- |
| **Precision** | [cite_start]**99.1%** [cite: 2113] |
| **Recall** | [cite_start]**99.1%** [cite: 2114] |
| **mAP@0.5** | [cite_start]**99.4%** [cite: 2115] |
| **mAP@0.5-0.95** | [cite_start]**66.2%** [cite: 2116] |
| **Inference Time** | [cite_start]**0.123s / image** (Mean) [cite: 2135] |

**Test Set Performance (1,201 images):**
* [cite_start]**F1-score:** 0.9983 [cite: 2133]
* [cite_start]**Accuracy:** 99.8% [cite: 2130]
* [cite_start]**Precision (Human class):** 1.00 [cite: 2130]

## 📂 Dataset & Preprocessing

* [cite_start]**Source:** Inspired by the **UNIRI-TID** dataset (University of Rijeka Thermal Image Dataset)[cite: 2000].
* [cite_start]**Format:** Grayscale thermal images simulating real-world conditions (fog, rain, night)[cite: 2001].
* **Preprocessing Pipeline:**
    1.  [cite_start]Mount data and clean corrupted images/labels[cite: 2017, 2018].
    2.  [cite_start]Integrity checks for valid labels[cite: 2019].
    3.  [cite_start]**Split Ratio:** 70% Training / 20% Validation / 10% Testing[cite: 2020].
    4.  [cite_start]Generate `data.yaml` configuration[cite: 2021].

## 🛠️ Model & Training Configuration

[cite_start]We utilized **YOLOv5n**, the smallest and fastest variant in the YOLOv5 family[cite: 2034].

### Training Hyperparameters
[cite_start]The model was trained for **60 epochs** with a batch size of **16** on **640x640** images[cite: 2037].

| Parameter | Value | Reason |
| :--- | :--- | :--- |
| **Optimizer** | SGD | [cite_start]Momentum = 0.937 [cite: 2045] |
| **Learning Rate** | lr0=0.01, lrf=0.1 | [cite_start]Standard for lightweight training [cite: 2045] |
| **IoU Threshold** | 0.2 | [cite_start]Helps detect small/distant human figures [cite: 2045, 2051] |
| **Anchor Threshold** | 4.0 | [cite_start]Loose anchor assignment for diverse object sizes [cite: 2045] |
| **Warmup Epochs** | 3.0 | [cite_start]Prevents gradient instability early in training [cite: 2045] |

### Data Augmentation Strategy
[cite_start]We employed robust augmentations to improve generalization, contrasting with the lighter augmentations used in related YOLOv8 studies[cite: 2068].

* [cite_start]**Mosaic (1.0) & Mixup (0.1):** Combines images to increase scene diversity[cite: 2065].
* [cite_start]**Copy-Paste (0.1):** Simulates occlusion[cite: 2065].
* [cite_start]**Perspective (0.0005):** Adds slight geometric distortion[cite: 2065].
* [cite_start]**HSV Adjustments:** Simulates sensor noise and lighting variations[cite: 2065].

## 📈 Performance Analysis

### Comparison with State-of-the-Art (YOLOv8)
We compared our YOLOv5n model against Rizk & Bayad's YOLOv8 models trained on the same domain. [cite_start]Despite being an older architecture, our tuned **YOLOv5n outperformed YOLOv8n, YOLOv8m, and even YOLOv8x** in mAP50 metrics on similar tasks[cite: 2118, 2119].

* [cite_start]**Our YOLOv5n:** mAP50 = **0.994** [cite: 2115]
* [cite_start]*YOLOv8n (Reference):* mAP50 = 0.913 [cite: 2119]
* [cite_start]*YOLOv8x (Reference):* mAP50 = 0.946 [cite: 2119]

### Confusion Matrix
[cite_start]The model achieved a **perfect separation** between the "human" class and the background, with 0 False Positives and 0 False Negatives on the validation set[cite: 2172, 2173].

---
*This repository contains the project report, and parameter files used for the study.*
