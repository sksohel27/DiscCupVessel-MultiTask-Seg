# DiscCupVessel-MultiTask-Seg
Deep Learning Pipeline: A U-Net–based system for glaucoma detection using fundus images. Tasks: • Vessel segmentation (256×256 patches ×4/image) → vessel density. • Optic disc (OD) segmentation → CDR computation. Data: ~12K multi-modal images with age, IOP, VCDR. Tech: PyTorch/Keras, Pandas, Matplotlib; supports hybrid vision+clinical models.
DiscCupVessel-MultiTask-Seg
Optic Disc & Optic Cup Segmentation for Automated Glaucoma Screening
MobileNetV2 + Lightweight U-Net | Multi-Task Learning | End-to-End CDR Estimation
Open In Colab
License: MIT
Python 3.10+
TensorFlow 2.x
A clean, efficient pipeline for simultaneous segmentation of the Optic Disc (OD) and Optic Cup (OC) from color fundus photographs — the core step for calculating the Cup-to-Disc Ratio (CDR), a primary biomarker for glaucoma detection and progression monitoring.
OD & OC Segmentation Result

What This Repository Does (Current Focus)

Accurate joint segmentation of Optic Disc and Optic Cup using a single multi-task model
2-channel output: Channel 0 = OD mask | Channel 1 = OC mask
Enables direct vertical/horizontal CDR computation for glaucoma risk scoring
Designed for real-world clinical deployment and large-scale screening


Key Features

















































FeatureDescriptionBackboneMobileNetV2 (ImageNet pre-trained) – lightweight & powerfulArchitectureCustom U-Net decoder with skip connections and separable convolutionsMulti-Task OutputSingle model predicts both OD and OC simultaneouslyPreprocessingCLAHE in LAB color space → dramatically improves disc/cup visibilityLoss FunctionBinary Cross Entropy + (1 – Dice) → sharp, high-overlap boundariesMetricsDice Coefficient & IoU per class + averageTraining EnhancementsOn-the-fly augmentation, live prediction plotting every epochSmart CheckpointingSaves every 5 epochs, deletes previous → minimal storage usageResume SupportAutomatically continues from latest checkpointInference VisualizationBeautiful 4-panel plot with overlay (Green = OD, Blue = OC)

Results (Validation Set – Final Model)

























StructureDice ScoreIoUOptic Disc0.9540.915Optic Cup0.8770.783Average0.9150.849
These scores are competitive with state-of-the-art on public benchmarks (REFUGE, Drishti-GS, etc.) while using a much lighter backbone.

How to Use

Open the provided Google Colab notebook (link above)
Upload or mount your dataset following the expected folder structure
Run all cells → training starts automatically (resumes if checkpoints exist)
Use the built-in inference function at the end to test on any fundus image

No local installation needed – everything runs in Colab (free GPU/TPU supported)

Dataset Format Expected
Your dataset should contain:

Color fundus images (any resolution, will be resized to 256×256)
Grayscale OD segmentation masks
Grayscale OC segmentation masks
A CSV file (metadata - standardized.csv) mapping each image to its OD and OC mask paths

The Colab notebook includes full data validation and path-fixing logic.

Project Files (in Colab)

Fundus_OD_OC_Segmentation.ipynb → Complete pipeline (data check → training → inference)
Model/ folder (auto-created) → Saved .keras checkpoints + final model
assets/ → Sample results and demo images


Future Extensions (Planned)

Add automated CDR measurement (vertical & horizontal)
Hybrid model: combine image features + clinical data (age, IOP, family history)
Export to TensorFlow Lite for mobile/edge deployment
Gradio web demo for instant upload-and-predict
