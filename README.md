# Cross-Scanner-Breast-Adenocarcinoma-Image-Segmentation-With-Deep-Learning-Algorithms


This repository contains the full implementation and experimental pipeline developed for my **Master’s Thesis**:

The work was conducted as part of the **Task 2 COSAS 2024 Challenge (Cross-Scanner Adenocarcinoma Segmentation)** and explores how foundation vision transformers can be fine-tuned for robust histopathological segmentation across different scanners and staining conditions.

---

## Overview

The goal of this project is to build a **scanner-agnostic segmentation framework** that can generalize across multiple acquisition devices without explicit domain adaptation.  
To achieve this, several decoder architectures were implemented and compared:

| Model Variant | Description | Final Weighted Score |
|----------------|-------------|----------------------|
| UNI2-H + DeepLabV3 | Convolutional baseline with Atrous Spatial Pyramid Pooling (ASPP) | 0.8184 |
| UNI2-H + Dual HR/LR Fusion | Dual-path fusion aligning high- and low-resolution features | **0.8217** |
| UNI2-H + PixelFPN + ASPP | Single-pass, explicit multi-scale pyramid with ASPP | 0.8206 |
| UNI2-H + PixelFPN + 1×1 Head | Lightweight pyramid fusion baseline | 0.8130 |
| UNI2-H + PixelFPN + Lite Query | Transformer query decoder with region-level grouping | 0.8176 |

---

## Key Features

- **Foundation model backbone:** UNI2-H (ViT-based histopathology encoder)
- **Multi-scale decoder designs:** convolutional (DeepLab), pyramid-based (PixelFPN), and attention-based (Lite Query)
- **Cross-scanner evaluation:** trained on 3 scanners, tested on 6 (including unseen domains)
- **Loss optimization:** comparative study of BCE, Dice, Tversky, and Focal formulations
- **Post-processing pipeline:** threshold + morphology sweep with Gaussian smoothing and small-object cleanup
- **Memory-efficient training:** 11–19 GB VRAM, single-pass inference (20–25 sec/domain)

---

## Dataset

Experiments were conducted on the **COSAS 2024 Task 2 dataset**:
- **Training:** 180 labeled patches from 3 scanners (3D-Histech 1000, KFBIO 400, Teksqray 600p)
- **Testing:** 90 patches from 6 scanners (including unseen Leica-450, Motic, and 3D-Histech 250)
- Patches size: approximately *1500×1500 px*, H&E stained

---

## Results Summary

- Foundation transformer (UNI2-H) achieved strong cross-domain generalization 
- Dual HR/LR Fusion decoder reached the best overall score (0.8217)  
- PixelFPN-based models offered the best speed/accuracy trade-off 
- Lite Query design improved grouping and boundary sharpness on dense clusters  
- Consistent performance across unseen scanners confirmed robust feature transfer


