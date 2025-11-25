# DiscCupVessel-MultiTask-Seg  
**Optic Disc & Optic Cup Segmentation for Automated Glaucoma Screening**  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/your-username/DiscCupVessel-MultiTask-Seg/blob/main/Fundus_OD_OC_Segmentation.ipynb) ![Python](https://img.shields.io/badge/python-3.8%2B-blue) ![PyTorch](https://img.shields.io/badge/framework-Keras%20/%20TensorFlow-orange)

A clean, efficient, and lightweight multi-task pipeline for **simultaneous segmentation of Optic Disc (OD) and Optic Cup (OC)** from color fundus photographs — enabling **direct end-to-end Cup-to-Disc Ratio (CDR)** calculation, the primary biomarker for glaucoma detection.

![example](assets/example_result.png)
*Green = Optic Disc | Blue = Optic Cup | Red overlay = Ground truth (for reference)*

## What This Repository Does (Current Focus)
- Accurate **joint segmentation** of Optic Disc and Optic Cup using a **single multi-task model**
- 2-channel output → `Channel 0 = OD mask` | `Channel 1 = OC mask`
- Enables **automatic vertical & horizontal CDR** computation for glaucoma risk scoring
- Designed for **real-world clinical deployment** and **large-scale screening programs**

## Key Features

| Feature                          | Description                                                                                   |
|----------------------------------|-----------------------------------------------------------------------------------------------|
| **Backbone**                     | MobileNetV2 (ImageNet pre-trained) – extremely lightweight yet powerful                      |
| **Architecture**                 | Custom lightweight U-Net decoder with skip connections + depthwise separable convolutions   |
| **Multi-Task Output**            | Single model predicts both OD and OC simultaneously                                          |
| **Preprocessing**                | CLAHE in LAB color space → dramatically improves disc/cup contrast                           |
| **Loss Function**                | BCE + (1 – Dice Coefficient) → sharp boundaries & high overlap                               |
| **Metrics**                      | Dice Coefficient & IoU per class + average                                                   |
| **Training Enhancements**        | On-the-fly augmentation (Albumentations), live prediction plotting every epoch              |
| **Smart Checkpointing**          | Saves every 5 epochs, auto-deletes older ones → minimal storage                              |
| **Resume Support**               | Automatically continues from latest checkpoint                                               |
| **Inference Visualization**      | Beautiful 4-panel plots with overlay (Green = OD, Blue = OC)                                  |

## Results (Validation Set – Final Model)

| Structure     | Dice Score | IoU    |
|---------------|------------|--------|
| Optic Disc    | **0.954**  | 0.915  |
| Optic Cup     | **0.877**  | 0.783  |
| **Average**   | **0.915**  | 0.849  |

These scores are **competitive with state-of-the-art** on public benchmarks (REFUGE, Drishti-GS, GAMMA, etc.) while using a **much lighter backbone** (≈ 2.3M parameters).

## How to Use (Zero Local Setup – Runs Entirely in Colab)

1. Click the **"Open in Colab"** badge above  
2. Upload or mount your dataset (see format below)  
3. Run all cells → training starts automatically (resumes if checkpoints exist)  
4. Use the built-in inference function at the end to test on any fundus image  

**Free GPU/TPU supported** – no installation needed!

### Expected Dataset Format
Your dataset folder should contain:
dataset/
├── images/               # Color fundus images (any resolution → resized to 256×256)
├── masks_od/             # Grayscale Optic Disc masks
├── masks_oc/             # Grayscale Optic Cup masks
└── standardized.csv      # CSV with columns: image_path, od_mask_path, oc_mask_path
text
The notebook includes **full data validation** and automatic path-fixing logic.

## Project Structure
DiscCupVessel-MultiTask-Seg/
├── Fundus_OD_OC_Segmentation.ipynb   ← Complete end-to-end notebook
├── Model/                            ← Auto-created: .keras checkpoints + final model
├── assets/                           ← Sample results & demo images
└── README.md
text

## Future Extensions (Planned)
- [ ] Fully automated vertical/horizontal CDR measurement
- [ ] Hybrid model: fuse image features + clinical data (age, IOP, family history, VCDR)
- [ ] Export to **TensorFlow Lite** for mobile/edge deployment
- [ ] **Gradio / Streamlit** web demo (upload → instant prediction)
- [ ] Vessel segmentation head → vessel density + ISNT rule evaluation

## Citation
If you use this code or model in your research, please cite:
```bibtex
@misc{discupvessel2025,
  author = {Your Name},
  title = {DiscCupVessel-MultiTask-Seg: Lightweight Multi-Task Segmentation of Optic Disc and Cup for Glaucoma Screening},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/your-username/DiscCupVessel-MultiTask-Seg}}
}
