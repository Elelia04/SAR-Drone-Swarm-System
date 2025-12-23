# Autonomous UAV Swarm for Wilderness Search and Rescue (WiSAR)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![YOLO](https://img.shields.io/badge/YOLO-v8%2Fv11-green)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Research_Prototype-orange)

## Project Overview
This project proposes an integrated system for detection and rescue in wilderness environments using autonomous drone swarms. It addresses the critical challenge of detecting small human targets in highly unbalanced datasets. The system is composed of three integrated computational modules:

### 1. Vision Baseline: Optimized for Recall
* **Goal:** Maximize sensitivity to ensure no victim is missed (False Negative avoidance).
* **Method:** Utilizes **YOLOv8s** trained on the HERIDAL dataset.
* **Key Techniques:** Implements **Tiling** to handle high-resolution aerial imagery and **Test Time Augmentation (TTA)** to boost operational recall.

### 2. Vision Enriched: Data & Model Scaling
* **Goal:** Maximize precision and generalization capability.
* **Method:** **Maximizing Feature Variance:** Integrated the **SARD dataset** to introduce diverse human poses (standing, walking) compared to the static (lying) victims of HERIDAL. This prevents the model from overfitting to specific terrain textures.
* **Architecture Benchmarking:** Evaluated the next-generation **YOLO11** architecture to leverage improved feature extraction capabilities on this enriched dataset.

### 3. Navigation: Deterministic Coverage
* **Goal:** Efficiently scan the search area with a drone swarm.
* **Method:** Implements a **Collaborative Greedy Search** algorithm.
* **Guarantee:** Ensures **100% area coverage** within battery constraints by using a shared "visited map" matrix for collision avoidance and path planning.

## Key Results & Benchmarking

We conducted a two-stage evaluation: first against the literature benchmark (validation Set), and second in a realistic "stress test" scenario (Test Set with high class imbalance).

### 1. Validation Set: Beating the State-of-the-Art
We compared our models against the reference paper results. Both our strategies surpassed the benchmark.

| Model Strategy | Precision | Recall | mAP@50 | mAP@50-95 |
| :--- | :---: | :---: | :---: | :---: |
| **Reference Paper [1]** | 0.842 | 0.743 | 0.802 | 0.388 |
| **YOLOv8s (Ours)** | 0.838 | 0.747 | **0.826** | **0.497** |
| **SARD + YOLO11m (Ours)**| **0.915** | **0.816** | **0.884** | **0.555** |

> **Analysis:** The Enriched strategy (YOLO11m) achieves the best overall metrics in a controlled environment, significantly outperforming the literature (+7.9% mAP).

### 2. Operational Test Set: The Reality Check
In the final operational simulation (unbalanced test set), we prioritized **recall** (finding missing persons) over recision.

| Model Strategy | Precision | Recall (Sensitivity) | mAP@50 |
| :--- | :---: | :---: | :---: |
| **YOLOv8s (Baseline)** | 0.649 | **0.681** | 0.672 |
| SARD + YOLO8n | 0.673 | 0.625 | 0.661 |
| SARD + YOLO11m | 0.635 | 0.646 | 0.659 |

## How to Run

This project is optimized for GPU environments (Kaggle / Google Colab).

### 1. Vision Module (Baseline)
The training and validation pipeline is contained in `vision_module_baseline/yolov8s-training.ipynb`.

**Steps:**
1.  Open the notebook in **Kaggle** (recommended for GPU access).
2.  Add the **HERIDAL** dataset to the input directory (downloadable from yolov8s-training.ipynb).
3.  Install dependencies (automatically handled in the first cell):
4.  Run all cells to execute:
    * **Tiling:** Preprocessing 4K images into 640x640 patches.
    * **Training:** Fine-tuning YOLOv8s.
    * **Validation:** Generating metrics and confusion matrices.

### 2. Navigation Module (Simulation)

## Authors

* **Eleonora Liani**
    * *Role:* Vision Baseline Strategy.
    * *Contribution:* Developed the YOLOv8s pipeline, implemented Image Tiling, optimized Recall via Test Time Augmentation (TTA).

* **Marianna Esposito**
    * *Role:* Vision Enriched Strategy.
    * *Contribution:* Managed SARD dataset integration, conducted benchmarking on YOLOv8n, YOLO11n, and YOLO11m.

* **Andrea De Marco**
    * *Role:* Autonomous Navigation.
    * *Contribution:* Developed the Collaborative Greedy Search algorithm and swarm coverage logic.

---

## References

---

## Repository Structure

The codebase is organized by module. 

```text
SAR-Drone-Swarm-System/
│
├── vision_module_baseline/     
│   ├── yolov8s-training.ipynb  # Training pipeline (HERIDAL + TTA)
│   ├── best.pt                 # Best model weights
│   └── validation_plots/       # Confusion matrix & PR curves
│
├── vision_module_enriched/     
│   ├── yolov11_experiments/    # SARD Dataset enrichment & YOLO11 comparisons
│   └── ...
│
└── navigation_module/          
    ├── swarm_logic/            # Greedy search & collision avoidance logic
    └── ...
