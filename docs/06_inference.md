# Inference

## Overview

`inference.py` allows you to classify **any image** not in the training dataset. It uses the trained ConvNeXt checkpoint and the same preprocessing pipeline as validation/test (no augmentation).

## Supported Input Formats

`.jpg` `.jpeg` `.png` `.bmp` `.tiff` `.tif` `.webp`

## Input Modes

| Mode | Command |
|------|---------|
| Single image | `python inference.py --image sample.jpg` |
| Multiple images | `python inference.py --image img1.jpg img2.jpg img3.jpg` |
| Entire folder | `python inference.py --folder my_images/` |
| Custom checkpoint | add `--checkpoint path/to/model.pth` to any of the above |

## How to Run (CLI)

```bash
# Single image
python scripts/inference.py --image test_sample.jpg

# Folder of images
python scripts/inference.py --folder my_test_images/

# With a tuned checkpoint
python scripts/inference.py --folder my_test_images/ --checkpoint tuning_results/phase_3/trial_2/best_model.pth

# Change output directory
python scripts/inference.py --folder my_test_images/ --output-dir results/

# Change grid columns (default: 4)
python scripts/inference.py --folder my_test_images/ --grid-cols 3
```

---

## Interactive Web UI (Flask)

The project includes a modern, dark-themed web interface for easier classification and explainability analysis.

### Features
- **Single/Batch Upload**: Process one or many images at once.
- **Grad-CAM Visualization**: View side-by-side explainability heatmaps for every prediction.
- **Probability Charts**: Interactive charts showing confidence across all classes.
- **History Gallery**: Browse previously processed images and their results.

### How to Run
```bash
python app.py
```
Then visit `http://localhost:5000` in your browser.

---

## Output Files (CLI)

| File | Content |
|------|---------|
| `outputs/inference_results.csv` | All predictions: filename, predicted class, confidence, per-class probability |
| `outputs/inference_grid.png` | Visual montage of images with predicted label and confidence overlaid |

---

## Checkpoint Auto-Detection

The checkpoint stores the model variant and image size used during training. `scripts/inference.py` reads these automatically — no manual config changes required even if you switch between `convnext_tiny` and `convnext_base` checkpoints.

## Key Files

| File | Role |
|------|------|
| `scripts/inference.py` | Main CLI inference script |
| `app.py` | Flask Web Application |
| `outputs/best_model.pth` | Default checkpoint (from `train.py`) |
| `tuning_results/phase_N/trial_X/best_model.pth` | Alternative checkpoints (from `tune.py`) |
