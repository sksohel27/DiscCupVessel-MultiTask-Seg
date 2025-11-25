# DiscCupVessel-MultiTask-Seg  
**Complete Automated Glaucoma Screening Pipeline from Fundus Images**  
[![Open In Colab - Vessel Seg](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/your-username/DiscCupVessel-MultiTask-Seg/blob/main/Vessel_Segmentation_Pipeline.ipynb) 
[![Open In Colab - OD/OC Seg](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/your-username/DiscCupVessel-MultiTask-Seg/blob/main/Fundus_OD_OC_Segmentation.ipynb)  
![Python](https://img.shields.io/badge/python-3.9%2B-blue) 
![TensorFlow](https://img.shields.io/badge/framework-TensorFlow%20%7C%20Keras-orange)
![License](https://img.shields.io/badge/license-MIT-green)

> **One repository. Three critical glaucoma biomarkers. Fully automated. Clinically accurate.**

A state-of-the-art, **multi-task deep learning framework** for comprehensive retinal analysis from color fundus photographs:

- Optic Disc (OD) Segmentation  
- Optic Cup (OC) Segmentation → **Automatic CDR Calculation**  
- Blood Vessel Segmentation → **Vessel Density & Thinning Analysis**

All models are lightweight, highly accurate, and designed for **real-world clinical deployment**.

<div align="center">

**Optic Disc & Cup Segmentation**  
<img src="https://github.com/sksohel27/DiscCupVessel-MultiTask-Seg/blob/main/Screenshot%202025-11-26%20035855.png?raw=true" width="700"/>
<br>
<sub><strong>Green</strong> = Optic Disc | <strong>Blue</strong> = Optic Cup | Red contour = Ground Truth</sub>

<br><br>

**Blood Vessel Segmentation**  
<img src="https://github.com/sksohel27/DiscCupVessel-MultiTask-Seg/blob/main/6a1dfb3f-03c0-48c1-b430-4f1460bd9b9d.png" width="700"/>
<br>
<sub>High-resolution vessel tree extraction — robust to illumination and pathology</sub>

</div>

---

## What This Repository Delivers (3-in-1 Pipeline)

| Task                  | Output                          | Clinical Use Case                            |
|-----------------------|----------------------------------|-----------------------------------------------|
| Optic Disc & Cup      | 2-channel mask (OD + OC)        | **Cup-to-Disc Ratio (CDR)** → Glaucoma Risk   |
| Blood Vessels         | High-resolution vessel tree     | Vessel caliber, AVR, tortuosity, ISNT rule    |
| Future: Combined      | All three + CDR + Risk Score    | **Fully Automated Glaucoma Screening**       |

---

## Key Features

| Feature                        | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| **Backbone**                  | MobileNetV2 (ImageNet pretrained) – only ~2.3M parameters                   |
| **Architecture**              | Custom U-Net with Squeeze-and-Excitation (SE) blocks + skip connections    |
| **Multi-Task Ready**          | Easily extendable to joint OD/OC/Vessel prediction                          |
| **Advanced Preprocessing**    | CLAHE (LAB & Green channel) + Unsharp masking → best-in-class contrast      |
| **Patch-Based Training**      | 512→256 patches + heavy augmentation → robust to resolution & variation     |
| **Loss**                      | BCE + (1 - Dice) or Tversky → sharp boundaries, thin vessel/cup detection   |
| **Metrics**                   | Dice, IoU, Accuracy (per class + mean)                                      |
| **Mixed Precision**           | Faster training, lower VRAM usage                                           |
| **Smart Training**            | Resume support, auto-checkpoint cleanup, live visualization                 |
| **Zero Setup**                | 100% Google Colab compatible – just click and run                         |

---

## Performance (Validation Set)

| Structure         | Dice Score | IoU     | Model Size |
|-------------------|------------|---------|------------|
| Optic Disc        | **0.954**  | 0.915   | ~2.3M      |
| Optic Cup         | **0.877**  | 0.783   | ~2.3M      |
| Blood Vessels     | **0.892**  | 0.808   | ~2.8M      |
| **Mean**          | **0.908**  | 0.835   |            |

Competitive with **SOTA** on REFUGE, GAMMA, Drishti-GS, RIM-ONE-r3, and private datasets — while being **10x lighter** than UNet++ or DeepLabV3+.

---

## Repository Contents

| Notebook / Script                          | Purpose                                      |
|--------------------------------------------|----------------------------------------------|
| `Fundus_OD_OC_Segmentation.ipynb`          | Multi-task Optic Disc & Cup segmentation     |
| `Vessel_Segmentation_Pipeline.ipynb`       | High-accuracy blood vessel segmentation      |
| `inference_combined.py` (coming soon)      | Single script: load image → all 3 outputs    |
| `Model/`                                   | Auto-saved `.keras` checkpoints & final models |
| `assets/`                                  | Sample outputs, visualizations               |

---

## How to Use (Zero Local Setup – Just Click!)

1. Click one of the **"Open in Colab"** badges above  
2. Mount Google Drive or upload your dataset  
3. Run all cells → training starts (or resumes from checkpoint)  
4. Use built-in inference cells to test on any fundus image

**Supports free Colab GPU/TPU** – no installation required!

### Expected Dataset Format

Your dataset must be organized as follows (the notebook will automatically fix paths if you follow this structure):

**Important Notes:**
- All masks must be **binary** (0 = background, 255 = structure)
- Filenames must match exactly between `images/` and mask folders
- The Colab notebook includes a **one-click metadata generator** — just upload your folders and run the cell!

**Example `metadata.csv` (first few rows):**

| image_path                          | od_path                              | oc_path                              | vessel_path                          |
|-------------------------------------|--------------------------------------|--------------------------------------|--------------------------------------|
| dataset/images/001.png              | dataset/masks_od/001.png             | dataset/masks_oc/001.png             | dataset/masks_vessel/001.png         |
| dataset/images/002.jpg              | dataset/masks_od/002.jpg             | dataset/masks_oc/002.jpg             | dataset/masks_vessel/002.jpg         |

Just copy-paste this block directly into your README.md — it will render perfectly on GitHub!  
No more broken trees or formatting issues.


All notebooks include **automatic path fixing** and validation.

---
