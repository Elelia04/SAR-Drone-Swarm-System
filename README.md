# Autonomous UAV Swarm for Wilderness Search and Rescue (WiSAR)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![YOLO](https://img.shields.io/badge/YOLO-v8%2Fv11-green)
![Status](https://img.shields.io/badge/Status-Research_Prototype-orange)

## Project Overview
This project proposes an integrated system for detection and rescue in wilderness environments using autonomous drone swarms. It addresses the critical challenge of detecting small human targets in highly unbalanced datasets (HERIDAL/SARD).

The system is composed of three main modules:
1.  **Vision Baseline:** Optimized for maximum Recall (Sensitivity) using YOLOv8s and Tiling.
2.  **Vision Enriched:** Optimized for Precision using Data Enrichment (SARD) and YOLO11.
3.  **Navigation:** A Collaborative Greedy Search algorithm ensuring 100% area coverage.

---

## Repository Structure

The codebase is organized by module. 

```text
SAR-Drone-Swarm-System/
│
├── vision_module_baseline/     <-- [AVAILABLE]
│   ├── yolov8s-training.ipynb  # Training pipeline (HERIDAL + TTA)
│   ├── best.pt                 # Best Model Weights
│   └── validation_plots/       # Confusion Matrix & PR Curves
│
├── vision_module_enriched/     <-- [PENDING UPLOAD by Colleague Name]
│   ├── yolov11_experiments/    # SARD Dataset enrichment & YOLO11 comparisons
│   └── ...
│
└── navigation_module/          <-- [PENDING UPLOAD by Colleague Name]
    ├── swarm_logic/            # Greedy Search & Collision Avoidance logic
    └── ...
