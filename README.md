# A YOLO-Based Deep Learning Model for Localizing Exterior Vehicle Damage by Vehicle-Part Location

This repository contains the official code, configuration, and trained model weights for the IEEE conference paper: **"A YOLO-Based Deep Learning Model for Localizing Exterior Vehicle Damage by Vehicle-Part Location"** by Somkiat Laowajeesart, Pakaket Wattuya, and Soontharee Koompairojn (Department of Computer Science, Kasetsart University, Bangkok, Thailand).

---

## 1. Overview
This study presents a lightweight YOLO-based object detection framework for localizing exterior vehicle damage across **13 vehicle-part classes** (`Front Windscreen`, `Head Light`, `Back Windscreen`, `Side Mirror`, `Tail Light`, `Bonnet`, `Boot`, `Door`, `Front Fender`, `Front Bumper`, `Back Fender`, `Back Bumper`, and `Roof`).

Among all evaluated configurations (`YOLOv11n` and `YOLOv12n`, with and without class-balancing data augmentation and CBAM), **YOLOv12n trained with class-balancing data augmentation (without CBAM)** achieved the highest overall test performance across three random seeds (`0`, `123`, and `456`):

| Metric | Score (Mean $\pm$ Std) |
| :--- | :--- |
| **Precision** | $0.799 \pm 0.024$ |
| **Recall** | $0.736 \pm 0.009$ |
| **F1-Score** | $0.767 \pm 0.012$ |
| **mAP50** | $0.794 \pm 0.012$ |
| **mAP@50:95** | $0.407 \pm 0.010$ |
| **Inference Latency** | $54.74\text{ ms/frame}$ ($18.27\text{ FPS}$) |

---

## 2. Repository Structure
```text
LocalizingExteriorVehicleDamage/
├── code/
│   ├── yolov12n_balancing_nocbam_seed_0.ipynb        # Training and Test evaluation and latency measurement script/logs for YOLOv12n,Balancing,No CBAM,Seed 0
│   ├── yolov12n_balancing_nocbam_seed_123.ipynb      # Training and Test evaluation and latency measurement script/logs for YOLOv12n,Balancing,No CBAM,Seed 123
│   └── yolov12n_balancing_nocbam_seed_456.ipynb      # Training and Test evaluation and latency measurement script/logs for YOLOv12n,Balancing,No CBAM,Seed 456
├── weights/
│   ├── yolov12n_balancing_nocbam_seed_0_best.pt      # Best validation mAP checkpoint (YOLOv12n,Balancing,No CBAM,Seed 0)
│   ├── yolov12n_balancing_nocbam_seed_123_best.pt    # Best validation mAP checkpoint (YOLOv12n,Balancing,No CBAM,Seed 123)
│   └── yolov12n_balancing_nocbam_seed_456_best.pt    # Best validation mAP checkpoint (YOLOv12n,Balancing,No CBAM,Seed 456)
├── dataset.yaml                                      # Ultralytics YOLO 13-class configuration
├── LICENSE                                           # License
└── README.md                                         # Documentation and licensing notes
```

---

## 3. Experimental & Evaluation Configuration
All models were trained and evaluated on $640 \times 640$-pixel images (resized with aspect-ratio-preserving white padding) on an Intel Core i3-12100F CPU, 32 GB DDR4 RAM, and an NVIDIA GeForce RTX 4060 GPU (8 GB VRAM) using the **Ultralytics** framework (`pip install ultralytics`):

* **Training Hyperparameters:** `lr0 = 0.0055`, `box = 9.6`, `cls = 2.0`, `dfl = 1.5`, `epochs = 200`, `batch = 16`
* **Random Seeds:** `0`, `123`, and `456`
* **Evaluation / NMS Settings:** `conf = 0.25`, `iou = 0.6`
* **Model Selection:** The checkpoint achieving the highest validation mAP@50:95 across 200 epochs was selected for held-out test set evaluation.

---

## 4. Dataset & Licensing Note
The dataset used in this study (1,757 images and 3,540 annotated objects split 70%/20%/10% into training, validation, and test sets) was compiled and refined from six publicly available repositories (cited as References [16]–[21] in the paper):
1. [car-damage-detecting-MaskRCNN by E. Kaushik (GitHub)](https://github.com/EashanKaushik/car-damage-detecting-MaskRCNN/)
2. [Kaggle Datasets by hongkyuryu](https://www.kaggle.com/datasets/hongkyuryu)
3. [Car Damage Dataset by V. Jose (Kaggle)](https://www.kaggle.com/datasets/vinayjose/car-damage-dataset/)
4. [Damaged Cars Dataset by Z. Zhakhangershaidullov (Kaggle)](https://www.kaggle.com/datasets/zhakhangershaidullov/damaged-cars-dataset/)
5. [CarDamageDetection Dataset (Roboflow)](https://app.roboflow.com/cardamagedetection-uemxz-rfagg/)
6. [Damaged Car Parts Dataset by ZIALQ (Roboflow)](https://app.roboflow.com/damaged-car-parts-zialq/)

**Note:** In compliance with third-party source licensing restrictions, raw dataset images and bounding-box annotations are excluded from this repository.
