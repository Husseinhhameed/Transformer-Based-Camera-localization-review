# Abstract of "MCAPR: Multi-modality Cross Attention for Camera Absolute Pose Regression"

![PAE Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/MCapr.png)

## Problem Statement

Absolute camera pose regression typically estimates the position and orientation of a camera solely based on the captured image, trained with a convolutional backbone with multilayer perceptron heads for a single reference scene only. Traditional methods often struggle with feature mismatching due to ambiguous patterns caused by visual similarity, leading to errors in visual localization.

## Proposed Solution

This paper proposes MCAPR, a novel approach using cross-attention Transformers to learn multi-scene absolute camera pose regression. Cross-attention modules aggregate activation maps with self-attention from different data modalities and convert latent features and scene indices into candidate pose predictions. This mechanism allows the model to focus more on general localization features.

## Model Structure

The proposed model comprises several key components:

### 1. Initial Feature Extraction

- Utilizes separate extractors for RGB and depth feature extraction using a ResNet-50 model for RGB images and a pre-trained PointNet for point clouds.

### 2. Cross-Attention Transformer Modules

- Applies cross-attention transformers to fuse visual and depth information, transforming the encoded scene index into a latent pose representation.
- Uses separate cross-attention modules for position and orientation estimation.

### 3. Pose Regression

- Performs scene classification and regresses the position and orientation feature vectors.

### 4. Loss Function

- Combines position and orientation errors with a Negative Log Likelihood (NLL) loss term for scene classification.

## Key Contributions

1. **Multi-modality Fusion:** Proposes a novel architecture for fusing data from different sensors and performing multi-scene APR using cross-attention transformers.
2. **Cross-Attention Mechanism:** Demonstrates that self-attention and cross-attention can aggregate position and rotation image features.
3. **Improved Performance:** Shows that rotation accuracy is significantly improved using the proposed method compared to existing multi-scene APR methods.

## Results

- **Datasets:** Evaluated on the 7-Scenes dataset.
- **Performance:** Achieves state-of-the-art rotation accuracy and slightly improved position accuracy compared to existing methods.

## Conclusion

MCAPR presents a robust and efficient solution for multi-scene absolute pose regression by leveraging cross-attention transformers. This approach effectively fuses multi-modality information, enhancing localization accuracy in challenging indoor environments.

## Detailed Structure of MCAPR Model

### 1. Initial Feature Extraction

- **RGB Feature Extraction:** Uses a ResNet-50 model to extract features from RGB images.
- **Point Cloud Feature Extraction:** Uses a pre-trained PointNet to extract features from point clouds.

### 2. Cross-Attention Transformer Modules

- **Self-Attention:** Models intra-modal relationships within RGB and depth features.
- **Cross-Attention:** Models inter-modal relationships between RGB and depth features.

### 3. Pose Regression

- **Scene Classification:** Uses concatenated features for scene classification.
- **Feature Vector Regression:** Regresses position and orientation feature vectors using MLP heads.

### 4. Loss Function

- **Position Error:** $( L_x = \| x_{gt} - x \|_2 \)$
- **Orientation Error:** $( L_q = \left\| q_{gt} - \frac{q}{\|q\|} \right\|_2 \)$
- **Combined Loss:** $( L_p = L_x \exp(-\alpha) + \alpha + L_q \exp(-\beta) + \beta + \text{NLL}(s, s_{gt}) \)$

## Training and Implementation

### Optimization

- **Optimizer:** Adam optimizer with an initial learning rate of \(10^{-6}\).
- **Training:** 900 epochs with a batch size of 4.

### Data Augmentation

- **Augmentation Techniques:** Includes rescaling, cropping, and normalization of input images.

### Hardware

- **Implementation:** Developed in PyTorch, trained on a 40GB NVIDIA A100 GPU.

By leveraging cross-attention transformers and multi-modality data fusion, MCAPR provides a robust, efficient, and accurate solution for indoor visual localization in multiple scenes.
