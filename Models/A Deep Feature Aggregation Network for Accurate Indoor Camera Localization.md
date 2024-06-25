# Abstract of "A Deep Feature Aggregation Network for Accurate Indoor Camera Localization"

![Deep Feature Aggregation Network Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/aggrigation.png)

## Problem Statement

As scene coordinate regression (SCoRe) methods become prevalent in the area of visual camera localization, the issue of repetitive or sparse texture scenes continues to be a concern. Specifically, they suffer from performance degeneration due to ambiguous patterns caused by visual similarity. Current methods rely on high-level feature maps, which alone are insufficient to model the regression problem accurately due to ambiguous patterns. Utilizing rich spatial details in low-level feature maps can address this issue.

## Proposed Solution

This paper proposes a novel network for camera localization using a single RGB image. The core components of the network are:

1. **Deep Feature Aggregation Module (DFAM):** Eliminates the difference among different level feature representations and fuses multi-level context information.
2. **CoordConv Scheme:** Improves the discrimination of features in repetitive or sparse texture areas.
3. **Deep Supervision:** Provides low-level feature maps with direct supervision from the ground truth to improve the accuracy of camera localization.
4. **Uncertainty Modeling:** Quantifies prediction errors stemming from intrinsic noise in the data.

## Model Structure

The proposed model comprises several key components:

### 1. Initial Feature Extraction

- Uses a modified ResNet18 to extract features with different receptive fields.
- Two 3x3 convolution layers replace the 7x7 convolution layer, and the last average pooling and fully connected layers are removed.

### 2. CoordConv Scheme

- Enhances the discrimination of each pixel in the image by concatenating two additional channels (u, v) representing pixel coordinates with the RGB image.

### 3. Deep Feature Aggregation Module (DFAM)

- Fuses multi-level context information with several Channel Attention Modules (CAM) to refine feature maps and enhance spatial details of low-level feature maps.

### 4. Regression and Pose Estimation

- Predicts 3D scene coordinates and coordinate uncertainty.
- Uses a RANSAC-based PnP algorithm to calculate the camera pose from predicted dense 2D-3D correspondences.

### 5. Deep Supervision

- Provides additional supervision for the shallow network during training, ensuring rapid and direct learning for low-level features.

### 6. Loss Function

- Combines regression loss and auxiliary loss to improve localization accuracy, balancing the errors with learned parameters.

## Key Contributions

1. **Deep Feature Aggregation Module (DFAM):** Fuses multi-level context information to generate a powerful feature representation.
2. **CoordConv Scheme:** Enhances feature discrimination in repetitive or sparse texture areas.
3. **Deep Supervision and Uncertainty Modeling:** Improves localization accuracy by providing direct supervision and quantifying prediction errors.
4. **Lightweight and Efficient Network:** Achieves state-of-the-art performance with competitive accuracy and modest computational cost.

## Results

- **Datasets:** Evaluated on 7-Scenes and 12-Scenes datasets.
- **Performance:** Demonstrates superior accuracy over state-of-the-art methods in terms of median positional and rotational errors, and 5cm-5° accuracy.
- **Visualization:** Predicts accurate camera poses and generates high-quality point clouds, even in challenging conditions.

## Conclusion

The proposed network integrates low-level and high-level feature maps for a more powerful feature representation. The Deep Feature Aggregation Module and CoordConv scheme address the limitations of existing methods, providing a robust and accurate solution for indoor camera localization. The network is designed to be lightweight and efficient, achieving competitive performance on benchmark datasets.

## Detailed Structure of the Model

### 1. Initial Feature Extraction

- Modified ResNet18 with two 3x3 convolution layers and without the last average pooling and fully connected layers.

### 2. CoordConv Scheme

- Constructs two additional channels (u, v) representing pixel coordinates.
- Concatenates these channels with the RGB image.

### 3. Deep Feature Aggregation Module (DFAM)

- Embedded with Channel Attention Modules (CAM) to refine feature maps and enhance spatial details.
- Fuses low-level and high-level feature maps to generate a powerful feature representation.

### 4. Regression and Pose Estimation

- Predicts dense 3D scene coordinates and coordinate uncertainty.
- Uses RANSAC-based PnP algorithm for camera pose estimation.

### 5. Loss Function

- Regression loss: $( L_{reg} = \frac{1}{N} \sum_{i=1}^N \left( 3 \log v_i + \frac{\| c_i - \hat{c}_i \|_2^2}{2 v_i^2} \right) \)$

### 6. Deep Supervision

- Provides additional supervision during training, ensuring rapid and direct learning for low-level features.
- Final loss function: $( L_f = L_r + \alpha L_a \)$

## Training and Implementation

### Optimization

- **Optimizer:** Adam optimizer with an initial learning rate of 0.0002, dropping by 95% every 10 epochs.

### Data Augmentation

- **Augmentation Techniques:** Includes rescaling, cropping, and normalization of input images.

### Hardware

- **Implementation:** Developed in PyTorch, trained on an Intel Core i7-9700K CPU with a single NVIDIA TITAN RTX GPU.

By leveraging the deep feature aggregation module and CoordConv scheme, this network provides a robust, efficient, and accurate solution for indoor camera localization.
