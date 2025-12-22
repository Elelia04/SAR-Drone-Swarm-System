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
