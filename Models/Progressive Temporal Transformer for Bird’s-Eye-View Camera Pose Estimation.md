# Abstract of "Progressive Temporal Transformer for Bird’s-Eye-View Camera Pose Estimation"

![PTFormer Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/bird.png)

## Problem Statement

Visual relocalization is a crucial technique used in visual odometry and SLAM to predict the 6-DoF camera pose of a query image. Existing works mainly focus on ground view in indoor or outdoor scenes. However, camera relocalization on unmanned aerial vehicles (UAVs) is less focused. Frequent view changes and large depths of field make this more challenging.

## Proposed Solution

This paper establishes a Bird’s-Eye-View (BEV) dataset for camera relocalization, containing four distinct scenes: roof, farmland, bare ground, and urban area. The dataset includes 177,242 images, posing challenges such as frequent view changes, repetitive or weak textures, and large depths of fields. The authors also propose a Progressive Temporal Transformer (PTFormer) as a baseline model. PTFormer is a sequence-based transformer with a designed progressive temporal aggregation module for temporal correlation exploitation and a parallel absolute and relative prediction head for implicitly modeling the temporal constraint.

## Model Structure

The PTFormer model consists of several key components:

### 1. Initial Feature Extraction

- Uses a pre-trained CNN to extract visual features from given images.

### 2. Transformer Encoder

- Augments spatial features using a Transformer encoder integrated with an inner attention module.

### 3. Temporal Aggregation Module (TAM)

- Applies two layers of temporal aggregation to exploit temporal correlation among features of a sequence of frames.

### 4. Pose Regression Heads

- **Absolute Pose Regression (APR) Head:** Predicts the camera pose of each frame.
- **Relative Pose Regression (RPR) Head:** Predicts the relative pose of all frame pairs, imposing temporal constraints on augmented features.

## Key Contributions

1. **BEV Dataset:** Establishes a challenging BEV dataset with 177,242 images collected by UAVs for camera relocalization.
2. **PTFormer Model:** Proposes PTFormer with temporal aggregation and parallel pose regression heads to handle large view changes and depths of field in BEV images.
3. **State-of-the-Art Performance:** Demonstrates robustness and accuracy on the BEV dataset, 7Scenes, and Cambridge Landmarks datasets.

## Results

- **Datasets:** Evaluated on the BEV dataset, 7Scenes, and Cambridge Landmarks datasets.
- **Performance:** Achieves the best performance on the BEV dataset and comparable results with state-of-the-art approaches on 7Scenes and Cambridge Landmarks datasets.

## Conclusion

PTFormer offers a robust and accurate solution for BEV camera pose estimation, handling challenges such as large view changes and variable textures. The proposed BEV dataset and PTFormer model set a new benchmark for future research in UAV-based camera relocalization.

## Detailed Structure of PTFormer Model

### 1. Initial Feature Extraction

- **CNN Backbone:** Extracts visual features from input images.

### 2. Sequential Representation

- Converts the activation map to a sequential representation using 1x1 convolutions and flattening.
- Adds positional embeddings for the X and Y axes.

### 3. Transformer Encoder

- Integrates inner attention within the Transformer encoder to enhance feature interaction.

### 4. Temporal Aggregation Module (TAM)

- Coarse and fine temporal aggregation to exploit temporal correlation in sequence features.

### 5. Pose Regression Heads

- **APR Head:** Regresses the absolute camera pose of each frame.
- **RPR Head:** Predicts relative camera poses to impose temporal constraints.

## Training and Implementation

### Optimization

- **Optimizer:** Adam optimizer with initial learning rate of $(1 \times 10^{-4}\)$.
- **Training:** Conducted for 600 epochs with a batch size of 8.

### Data Augmentation

- Includes rescaling, cropping, and normalization of input images.

### Hardware

- **Implementation:** Developed in PyTorch, trained on a single NVIDIA Tesla A100 GPU.

By leveraging temporal aggregation and inner attention mechanisms, PTFormer effectively improves the accuracy of BEV camera pose estimation, setting a new benchmark for the field.
