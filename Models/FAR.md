# Abstract of "FAR: Flexible, Accurate and Robust 6DoF Relative Camera Pose Estimation"

![Model Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/FAR.png)

### Problem Statement

Relative camera pose estimation between images is a central problem in computer vision, critical for applications like augmented reality, robotics, and autonomous driving. Traditional methods that find correspondences and solve for the fundamental matrix offer high precision but struggle with large view changes and cannot infer absolute translation scale. Conversely, neural network-based methods predicting pose directly are more robust to limited overlap and can infer translation scale but at the expense of reduced precision.

### Proposed Solution

This paper presents FAR, a novel approach that combines the precision of traditional correspondence-based methods with the robustness of learning-based methods for 6DoF relative pose estimation. FAR utilizes a Transformer to balance between solved and learned pose estimations, providing a prior to guide a solver. This approach yields results that are both precise and robust while accurately inferring translation scales.

### Model Structure

FAR consists of several key components:

**1. Initial Feature Extraction:**

- Dense features are extracted from input images using various feature estimation methods.

**2. Pose Transformer:**

- A Transformer processes the dense features to predict the 6DoF pose and a relative weight for combining with solver estimates.
- Combines the predicted pose with solver estimates using learned weights to produce the final output.

**3. Prior-Guided Robust Pose Estimator:**

- Uses the predicted pose to influence the search and scoring functions of a classical solver, improving performance in data-scarce scenarios.

### Key Contributions

**1. Hybrid Approach:**

- Integrates learned pose estimation with classical solver methods to leverage the strengths of both.

**2. Transformer-Based Architecture:**

- Utilizes a Transformer for global attention across dense feature inputs, improving robustness and precision.

**3. Robustness to Poor Correspondences:**

- Demonstrates significant robustness to noise and outliers in correspondence estimation.

### Results

- Evaluated on Matterport3D, InteriorNet, StreetLearn, and Map-free Relocalization datasets.
- Achieves state-of-the-art performance, significantly reducing translation and rotation errors compared to existing methods.
- Demonstrates flexibility across different feature extraction and correspondence estimation methods.

### Detailed Structure of the FAR Model

**1. Initial Feature Extraction:**

- Utilizes pre-trained CNNs and other methods for dense feature extraction from input images.

**2. Pose Transformer:**

- Processes dense features with self-attention and multi-head attention layers to predict pose and relative weight.

**3. Prior-Guided Robust Pose Estimator:**

- Incorporates the predicted pose as a prior for the classical solver, modifying the search and scoring functions for improved robustness.

### Training and Implementation

- **Optimization:** Trained with the Adam optimizer and a geometrically annealed learning rate.
- **Data Augmentation:** Includes rescaling, cropping, and normalization of input images.
- **Hardware:** Implemented in PyTorch, trained on Nvidia GPUs.

By combining the strengths of learned and classical methods, FAR offers a robust, efficient, and accurate solution for relative camera pose estimation in diverse computer vision applications.
