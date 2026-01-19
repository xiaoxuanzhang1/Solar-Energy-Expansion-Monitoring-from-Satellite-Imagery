# Solar Energy Expansion Monitoring from Satellite Imagery

This repository presents a deep learning project that applies **Convolutional Neural Networks (CNNs)** to detect utility-scale solar panel installations from satellite imagery. The project combines computer vision, geospatial data, and policy analysis to study patterns of renewable energy deployment across regions.

The main objective of this project is to:
- Automatically detect utility-scale solar farms from satellite imagery
- Evaluate how well a CNN trained in one region generalizes to other regions
- Use model performance as an analytical lens to understand **policy-driven differences** in solar deployment patterns

By linking machine learning performance with regional energy policy contexts, the project demonstrates how data-driven methods can inform infrastructure monitoring and policy research.

## Key Skills Demonstrated

- Deep learning for image classification (CNNs)
- Satellite imagery processing
- Geospatial data integration (OSM + satellite data)
- Cross-regional model evaluation and generalization analysis
- Interpretation of ML results in a **policy and socioeconomic context**
- Reproducible research and scientific reporting

## Data Sources

- **Solar installation data**:  
  OpenStreetMap (OSM), queried via the Overpass API  
  (utility-scale, ground-mounted solar farms only)

- **Satellite imagery**:  
  Sentinel-2 Surface Reflectance data accessed via **Google Earth Engine (GEE)**  
  - RGB bands (B4, B3, B2)
  - Median composite (April–October 2022)
  - Image patches of 256 × 256 pixels

- **Study regions**:
  - Germany (training and validation)
  - European Union (Spain, Italy, Switzerland)
  - United States (California, Texas, Arizona)

## Methodology

### 1. Dataset Construction
- Integrated OSM point data with Sentinel-2 imagery
- Created a balanced binary classification dataset:
  - Positive samples: utility-scale solar farms
  - Negative samples: random locations with spatial buffers to avoid contamination

### 2. Deep Learning Model
- Lightweight CNN implemented in **PyTorch**
- Architecture:
  - Stacked 3×3 convolutional layers with ReLU
  - Max pooling and dropout
  - Adaptive average pooling
  - Fully connected classification layer
- Training strategy:
  - Adam optimizer
  - Cross-entropy loss
  - Data augmentation (cropping, flipping, color jitter)
  - Early stopping based on validation loss

### 3. Model Evaluation
- Train/validation/test split: 60 / 20 / 20 (Germany)
- Cross-regional testing on EU and US datasets **without retraining**
- Evaluation metrics:
  - Accuracy
  - Precision, recall, F1-score
  - Confusion matrices

## 📊 Key Results

- **Germany (in-domain)**:
  - Accuracy above 90%
  - High recall for utility-scale solar farms

- **European Union (cross-region)**:
  - Moderate performance drop
  - Errors linked to heterogeneous solar layouts (e.g. agrivoltaics, industrial sites)

- **United States (cross-region)**:
  - Severe performance degradation
  - Extremely low recall for utility-scale installations
  - Strong evidence of **covariate shift** due to differences in scale, environment, and policy-driven infrastructure design

These results show that model performance itself can serve as a signal of structural differences in renewable energy deployment.

## Policy & Research Insight

The project demonstrates that:
- Solar infrastructure is not visually uniform across countries
- National and regional **energy policies directly shape physical deployment patterns**
- A “one-size-fits-all” machine learning model is insufficient for global monitoring

This highlights the importance of **diverse, representative training data** for earth observation applications and opens avenues for policy-sensitive ML research.


