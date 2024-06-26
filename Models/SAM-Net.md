# Abstract of "SAM-Net: Semantic probabilistic and attention mechanisms of dynamic objects for self-supervised depth and camera pose estimation in visual odometry applications"

![SAM-Net Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/SAM.png)

## Problem Statement

3D scene understanding is an essential research topic in the field of Visual Odometry (VO). VO is usually built under the assumption of a static environment, which does not always hold in real scenarios. Existing works fail to consider the dynamic objects, leading to poor performance.

## Proposed Solution

To tackle the aforementioned issues, we propose a self-supervised learning-based VO framework with Semantic probabilistic and Attention Mechanism, SAM-Net, which can jointly learn the single view depth, the ego motion of the camera, and object detection. For depth estimation, a semantic probabilistic fusion mechanism is employed to detect the dynamic objects and generate the semantic probability map as a prior before feeding it to the network to generate a more refined depth map. An attention mechanism is explored to enhance perception ability in the spatial and channel view. For pose estimation, we present a novel PoseNet with atrous separable convolution to expand the receptive field. The photometric consistency loss is employed to alleviate the impact of large rotations.

## Model Structure

The proposed model comprises several key components:

### 1. Semantic Probabilistic Fusion Mechanism (SPFM)

- Employs image semantic information for geometric estimation.
- Detects dynamic objects and generates a semantic probability map as a prior.
- Produces a more refined depth map.

### 2. Attention Mechanism (AM)

- Ensures the network focuses more on significant areas during training.
- Enhances perception ability in spatial and channel view.

### 3. PoseNet with Atrous Separable Convolution

- Expands the receptive field.
- Reduces data uncertainty.
- Strengthens the assumption of photometric consistency.
- Makes photometric consistency loss more robust to large rotations.

### 4. Loss Function

- Uses photometric consistency loss to improve robustness to large rotations.

## Key Contributions

### 1. Semantic Probabilistic Fusion Mechanism (SPFM)

- Uses semantic information for better geometric estimation.
- Makes the network focus more on static pixels rather than dynamic ones.

### 2. Attention Mechanism (AM)

- Ensures the network emphasizes significant areas during training.

### 3. PoseNet with Atrous Separable Convolution

- Novel pose estimation network.
- Expands receptive field and reduces uncertainty.
- Enhances robustness to large rotations.

## Results

- **Datasets:** Evaluated on the KITTI dataset.
- **Performance:** Achieves excellent pose and depth accuracy, competitive with state-of-the-art approaches.
- **PoseNet:** Capable of accurately predicting pose from input images.
- **SPFM and AM:** Significantly improve the quality of the disparity map.

## Conclusion

SAM-Net presents a robust and efficient solution for self-supervised depth and camera pose estimation by incorporating semantic probabilistic and attention mechanisms. It addresses the limitations of traditional VO methods by jointly estimating depth and pose while considering dynamic objects and enhancing spatial perception.

## Detailed Structure of SAM-Net Model

### 1. Semantic Probabilistic Fusion Mechanism (SPFM)

- **Image Semantic Information:** Used for geometric estimation.
- **Dynamic Object Detection:** Generates a semantic probability map.
- **Refined Depth Map:** Produced using the semantic probability map.

### 2. Attention Mechanism (AM)

- **Spatial and Channel View:** Enhances perception ability.
- **Significant Area Focus:** Ensures network focuses on key areas during training.

### 3. PoseNet with Atrous Separable Convolution

- **Expanded Receptive Field:** Improves pose estimation.
- **Reduced Uncertainty:** Enhances data reliability.
- **Photometric Consistency:** Strengthens loss function's robustness to large rotations.

### 4. Loss Function

- **Photometric Consistency Loss:** Enhances robustness to large rotations.

## Training and Implementation

### Optimization

- **Optimizer:** Adam optimizer with an initial learning rate of \(0.0001\).
- **Training:** End-to-end training on NVIDIA Tesla V100 GPUs.

### Data Augmentation

- **Augmentation Techniques:** Includes rescaling, cropping, and normalization.

### Hardware

- **Implementation:** Developed in PyTorch, trained on NVIDIA Tesla V100 GPUs.

