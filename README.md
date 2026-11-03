# STURM-Flood: Deep Learning-Based Flood Extent Mapping Using Satellite Imagery

A research project focused on satellite-based flood detection and segmentation using Sentinel-1 SAR and Sentinel-2 optical imagery. This project builds upon the STURM-Flood dataset and pretrained U-Net models, with the goal of exploring improved flood segmentation, self-supervised learning, temporal-aware training, and multi-sensor analysis.

## Overview

Flood mapping is an important application of remote sensing and deep learning. Accurate identification of flooded regions from satellite imagery can support disaster monitoring, damage assessment, and emergency response.

This project uses the STURM-Flood dataset to investigate deep learning approaches for flood extent mapping. We first establish a Sentinel-1 U-Net baseline and compare its performance with the original research paper. Further experiments will explore improvements to the complete flood mapping pipeline.

## Objectives

- Implement and evaluate the original STURM-Flood U-Net baseline.
- Perform flood segmentation using Sentinel-1 SAR imagery.
- Reproduce and evaluate Sentinel-2 baseline performance.
- Compare model performance with the original STURM-Flood research paper.
- Explore self-supervised learning for satellite image representation.
- Investigate temporal-aware learning to account for acquisition-time differences.
- Explore Sentinel-1 and Sentinel-2 multi-sensor fusion.
- Develop a framework for visualizing and analysing flood extent predictions.

## Dataset

This project uses the **STURM-Flood dataset**, which contains satellite imagery and corresponding flood masks.

| Dataset property | Details |
|---|---|
| Sentinel-1 tiles | 21,602 |
| Sentinel-2 tiles | 2,675 |
| Image dimensions | 128 × 128 pixels |
| Spatial resolution | 10 metres |
| Flood events | 60 |
| Data type | Satellite imagery and flood masks |

### Data Sources

- [STURM-Flood GitHub Repository](https://github.com/STURM-WEO/STURM-Flood)
- [STURM-Flood Dataset](https://doi.org/10.5281/zenodo.12748982)
- [Sentinel-1 Pretrained Model](https://doi.org/10.5281/zenodo.15189664)
- [Sentinel-2 Pretrained Model](https://doi.org/10.5281/zenodo.15189633)

## Methodology

### 1. Data Preprocessing

- Load Sentinel-1 satellite images and corresponding flood masks.
- Match image and mask files using filenames.
- Handle missing and invalid raster data.
- Prepare image and mask pairs for model training.
- Convert water-related mask classes into binary flood segmentation labels.

### 2. Sentinel-1 Baseline Implementation

An initial Sentinel-1 U-Net baseline has been implemented.

**Model configuration:**

| Parameter | Configuration |
|---|---|
| Input channels | 2 (VV and VH) |
| Input dimensions | 128 × 128 |
| Output classes | 2 |
| Architecture | U-Net |
| Initial filters | 32 |
| Encoder/decoder blocks | 5 |
| Optimizer | Adam |
| Learning rate | 0.001 |
| Batch size | 4 |
| Epochs | 20 |
| Loss function | Categorical Focal Loss |

### 3. Baseline Evaluation

The current Sentinel-1 model was evaluated using a held-out test split.

| Metric | Our Model | Original Paper |
|---|---:|---:|
| Accuracy | 84.17% | 83.61% |
| Weighted F1-score | 83.50% | 83.27% |
| Water Precision | 76.96% | 74.65% |
| Water Recall | 60.01% | 65.53% |
| Water F1-score | 67.43% | 69.79% |

**Note:** These results are not a strict reproduction comparison. Our implementation used 5,927 valid image-mask pairs and a smaller U-Net architecture than the paper's tuned model. Differences in preprocessing, filtering, and data splitting must be considered when interpreting the results.

## Proposed Research Improvements

The following directions are planned for further experimentation.

### 1. Self-Supervised Learning (SSL)

Explore self-supervised representation learning to improve feature extraction from unlabeled satellite imagery.

Potential approaches:
- MAE-style masked image reconstruction.
- SimCLR-style contrastive learning.
- Transfer of pretrained encoder weights to the U-Net segmentation model.

### 2. Temporal-Aware Learning

Satellite images and reference flood masks may have different acquisition times. We plan to investigate temporal confidence weighting to account for possible changes in flood conditions.

Potential approach:
- Calculate the time difference between satellite acquisition and flood-map acquisition.
- Estimate temporal confidence weights.
- Incorporate confidence weights into the segmentation loss.
- Analyse model performance across different temporal-gap groups.

### 3. Multi-Sensor Fusion

Investigate combining Sentinel-1 SAR and Sentinel-2 optical information to improve flood extent mapping.

Potential areas:
- Feature-level fusion.
- Multi-modal representation learning.
- Comparative evaluation of individual sensor models and fused models.

### 4. Uncertainty and Boundary Analysis

Explore methods to improve the reliability of predictions.

Potential areas:
- Prediction uncertainty estimation.
- Flood boundary refinement.
- Analysis of false positives and false negatives.
- Visual comparison of ground-truth and predicted masks.

### 5. Flood Monitoring and Visualization

A future extension is to develop an interactive interface for:
- Satellite image upload.
- Flood segmentation visualization.
- Flooded-area estimation.
- Geographical flood extent mapping.
- Comparison of predictions across acquisition dates.
- Downloadable prediction results.

## Evaluation Metrics

The project uses or plans to investigate the following evaluation metrics:

- Accuracy
- Precision
- Recall
- F1-score
- Intersection over Union (IoU)
- Dice coefficient
- Boundary F1-score
- Inference time and model complexity

## Technology Stack

- **Programming Language:** Python
- **Deep Learning:** TensorFlow / Keras
- **Data Processing:** NumPy, Pandas
- **Geospatial Processing:** Rasterio
- **Machine Learning:** Scikit-learn
- **Visualization:** Matplotlib
- **Environment:** Google Colab / Jupyter Notebook
- **Version Control:** Git and GitHub

## Project Status

| Component | Status |
|---|---|
| STURM-Flood dataset preparation | Initial implementation completed |
| Sentinel-1 baseline | Implemented and evaluated |
| Original paper comparison | Completed for initial baseline |
| Sentinel-2 baseline | Pending |
| Self-supervised learning | Planned |
| Temporal-aware learning | Planned |
| Multi-sensor fusion | Planned |
| Uncertainty analysis | Planned |
| Interactive dashboard | Future extension |

## Future Scope

The long-term goal is to develop a multi-sensor, self-supervised, and temporal-aware flood extent mapping framework capable of analysing satellite imagery and producing reliable flood segmentation results.

The project aims to move beyond individual image segmentation towards a more comprehensive flood monitoring and analysis system.

## Reference

Notarangelo et al. (2025). *STURM-Flood: A curated dataset for deep learning-based flood extent mapping leveraging Sentinel-1 and Sentinel-2 imagery.*

Big Earth Data.

[Research Paper DOI](https://doi.org/10.1080/20964471.2025.2458714)

---

**Disclaimer:** This repository is an ongoing research implementation based on the STURM-Flood dataset and original work. Proposed improvements are experimental directions and will be reported only after implementation and evaluation.
