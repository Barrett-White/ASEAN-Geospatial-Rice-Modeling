# ASEAN Rice Classification Pipeline

This project implements an end-to-end geospatial machine learning pipeline to classify rice vs. non-rice land cover in Southeast Asia using open-access satellite and environmental data. The primary model is a Random Forest trained on engineered tabular features extracted from multi-sensor satellite imagery.

## Project Goal

Accurately identifying rice cultivation is important for food security and agricultural planning in ASEAN countries. Many existing approaches rely on proprietary data or complex deep learning models that are difficult to deploy at scale. This project focuses on a lightweight, interpretable pipeline built entirely on free data and classical machine learning.

## Pipeline Overview

### 1. Sampling and Labels
- Study area: Thailand, split into four macro-regions
- 800 total geospatial sample points (200 per region)
- Binary labels (Rice / Non-Rice) derived from a supervised rice mask
- Sampling and labeling performed in Google Earth Engine

### 2. Feature Extraction
Features are aggregated over the 2019 growing season for each point.

Satellite features:
- Sentinel-1 SAR (VV, VH backscatter)
- Sentinel-2 optical bands
- MODIS vegetation indices (NDVI, EVI)

Environmental features:
- Precipitation (CHIRPS, ERA5)
- Land surface temperature
- Elevation and slope
- Soil properties

Final dataset contains approximately 25 engineered features per location.

## Model

### Random Forest Classifier
The primary model is a Random Forest trained using scikit-learn.

Reasons for selection:
- Handles non-linear feature interactions
- Performs well on small-to-medium tabular datasets
- Resistant to overfitting
- Provides feature importance for interpretability

Training setup:
- 80/20 train-test split
- 5-fold cross-validation
- Optimized for ROC–AUC

## Results

Test set performance:
- Accuracy: 0.85
- ROC–AUC: 0.91
- Rice precision / recall: 0.76 / 0.76
- Non-rice precision / recall: 0.89 / 0.89

Most important features include Sentinel-1 VV and VH backscatter, land surface temperature, and vegetation indices.

