# Abstract of "CoVisPose: Co-visibility Pose Transformer for Wide-Baseline Relative Pose Estimation in 360° Indoor Panoramas"

![CoVisPose Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/CoVisPose.png)

## Problem Statement

Accurate camera pose estimation in 360° indoor panoramas is essential for applications such as virtual tours, AR/VR, and indoor navigation. Traditional methods, such as feature-based Structure-from-Motion (SfM), struggle with wide baselines, occlusion, and repetitive textures in indoor environments. Deep learning methods offer potential improvements but often require dense data and specialized hardware, making them impractical for real-world scenarios with sparse captures and low visual overlap.

## Proposed Solution

CoVisPose introduces a novel transformer-based architecture to estimate relative camera poses in wide-baseline 360° indoor panoramas. The method learns dense bidirectional visual overlap, angular correspondence, and layout geometry to create robust representations for direct pose regression. CoVisPose operates over image-column feature sequences, leveraging transformers to capture global context and provide accurate pose estimates even in challenging scenarios.

## Model Structure

CoVisPose consists of several key components:

### 1. Initial Feature Extraction

- Uses a ResNet50 backbone followed by a height compression module (HCM) to extract image-column feature sequences from 360° panoramas.

### 2. CoVis Transformer

- Applies a transformer over concatenated image-column features from both panoramas, adding positional encodings and segment embeddings to maintain spatial and image membership information.
- The transformer comprises 6 encoder layers with 8 heads of self-attention, processing feature sequences to generate rich embeddings.

### 3. Decoders

- **Co-visibility, Angular Correspondence, and Floor-Wall Boundary (CCF) Decoder:**
  - Maps transformer embeddings to column-wise outputs, predicting visual overlap, angular correspondence, and floor-wall boundary angles for each image column.
- **Pose Decoder:**
  - Applies a 6-layer 1D CNN to the transformer embeddings, followed by a fully connected layer to regress the relative pose.

### 4. Loss Function

- Combines L1 loss for angular predictions, binary cross-entropy for co-visibility, and mean-squared error for relative pose, with scaling parameters to balance the components.

## Key Contributions

### 1. Transformer-Based Architecture

- Utilizes transformers for global attention across image columns, enhancing robustness to wide baselines and low visual overlap.

### 2. Dense Column-Wise Representations

- Jointly learns visual overlap, correspondence, and layout geometry, providing strong priors for pose regression.

### 3. RANSAC Integration

- Supports pose estimation through RANSAC-based rigid registration of predicted corresponding boundary points, improving accuracy for challenging cases.

## Results

- Evaluated on the Zillow Indoor Dataset (ZInD), demonstrating state-of-the-art performance with significant reductions in rotation and translation errors compared to baseline methods.
- Achieves robust pose estimation in scenarios with minimal visual overlap and wide baselines, outperforming both classical SfM and deep feature matching approaches.

## Detailed Structure of CoVisPose Model

### 1. Initial Feature Extraction

- ResNet50 backbone followed by HCM to produce feature sequences for each panorama, maintaining spatial and layout information.

### 2. CoVis Transformer

- Concatenates image-column features, applies positional and segment encodings, and processes through transformer layers for global context aggregation.

### 3. Decoders

- **CCF Decoder:** Outputs column-wise predictions for visual overlap, angular correspondence, and floor-wall boundary angles.
- **Pose Decoder:** Regresses relative pose from transformer embeddings using a 1D CNN and fully connected layer.

### 4. Loss Function

- Balances L1 loss, binary cross-entropy, and mean-squared error for accurate prediction of column-wise outputs and relative pose.

## Training and Implementation

- Trained in PyTorch on NVIDIA Tesla V100 GPUs, with random rotational augmentation and panorama pair order swapping.
- Uses Adam optimizer with a learning rate of 0.0001, and selects the best model based on validation loss.


