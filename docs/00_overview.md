# Project Overview

A PyTorch-based multiclass image classification system to identify parasite eggs in microscopy images using **ConvNeXt** (transfer learning).

## Problem Statement

Classify microscopy images of parasite eggs into 3 classes:

| Class | Label |
|-------|-------|
| *Ascaris lumbricoides* | 0 |
| *Hookworm* | 1 |
| *Trichuris trichiura* | 2 |

## Dataset Summary

| Split | Ascaris | Hookworm | Trichuris | Total |
|-------|---------|----------|-----------|-------|
| Train | 100 | 100 | 100 | 300 |
| Val   | 100 | 100 | 100 | 300 |
| Test  | 78  | 100 | 67  | 245  |

All images are `.jpg`. Manifest text files (`train_set.txt`, `val_set.txt`, `test_set.txt`) list relative paths without file extensions.

## Target Hardware

| Component | Spec |
|-----------|------|
| CPU | AMD Ryzen 7 7700 |
| RAM | 32 GB |
| GPU | NVIDIA RTX 5060 Ti 16 GB |
| OS | Windows |

## Project File Structure

```
Thesis-MultiClass-Image-Classification/
├── data/               # Dataset manifests (train/val/test lists)
│   ├── train_set.txt
│   ├── val_set.txt
│   └── test_set.txt
├── src/                # Core Logic (Config, Model, Dataset, Utils)
│   ├── config.py       # Configuration and hyperparameters
│   ├── dataset.py      # PyTorch Dataset and Dataloader
│   ├── model.py        # ConvNeXt model architecture
│   ├── utils.py        # Helper functions and metrics
│   └── visualize_cam.py # Grad-CAM implementation
├── scripts/            # CLI Tools (Train, Eval, Tune, Analysis)
│   ├── train.py        # Main training script
│   ├── evaluate.py     # Evaluation on test set
│   ├── tune.py         # Hyperparameter tuning
│   ├── analysis.py     # ROC, t-SNE, and cost analysis
│   └── inference.py    # CLI image inference
├── templates/          # Modern Web UI (HTML/CSS)
├── outputs/            # Model checkpoints, logs, and plots
├── app.py              # Flask Web Application
├── Dockerfile          # Container configuration
├── docker-compose.yml  # Docker multi-container setup
├── requirements.txt    # Python dependencies
├── .gitignore          # Git ignore file
└── DOCUMENTATION.md    # Complete technical documentation
```

## Quick Start (on PC)

```bash
# 1. Install dependencies
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124
pip install timm Pillow numpy pandas matplotlib seaborn scikit-learn tqdm thop flask opencv-python

# 2. Train (single seed)
python scripts/train.py

# 2b. Train with 5 seeds for academic mean ± std reporting
python scripts/train.py --seeds 42,123,456,789,1234

# 3. Evaluate on test set
python scripts/evaluate.py

# 4. Academic analysis (ROC/AUC, t-SNE, cost report)
python scripts/analysis.py --all

# 5. Run inference on unseen images (CLI)
python scripts/inference.py --folder my_unseen_images/

# 6. Run Web UI
python app.py

# 7. (Optional) Hyperparameter tuning
python scripts/tune.py --phase 1    # Learning rate
python scripts/tune.py --phase 2    # Batch size + weight decay
python scripts/tune.py --phase 3    # Dropout + label smoothing
# ... and so on
python scripts/compare_results.py   # Final comparison + best_config.json
```
