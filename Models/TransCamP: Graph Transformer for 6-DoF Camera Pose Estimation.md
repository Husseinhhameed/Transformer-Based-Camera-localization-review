# Abstract of "TransCamP: Graph Transformer for 6-DoF Camera Pose Estimation"

![TransCamP](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/TransCamP.png)


## Problem Statement

Camera pose estimation or camera relocalization is crucial in computer vision tasks like visual odometry, structure from motion (SfM), and SLAM. Traditional methods, heavily reliant on photometric consistency and geometric constraints, are computationally intensive and prone to errors in challenging environments. Deep learning approaches, particularly those utilizing Convolutional Neural Networks (CNNs) and Graph Neural Networks (GNNs), offer promising alternatives but often struggle with efficiency and robustness in dynamic and noisy conditions.

## Proposed Solution

This paper introduces TransCamP, a novel neural network framework with a graph transformer backbone to address the camera relocalization problem. TransCamP effectively fuses image features, camera pose information, and inter-frame relative motions into encoded graph attributes. It utilizes graph transformer layers with edge features and a tensorized adjacency matrix to dynamically capture global attention, improving computational efficiency, robustness, and accuracy.

## Model Structure

TransCamP comprises several key components:

### 1. Initial Feature Extraction

- RGB images are processed through a pre-trained CNN (ResNet) to extract feature maps.
- These feature maps are embedded in a view-graph where nodes represent images and edges encode inter-frame correlations.

### 2. Graph Embedding

- **Node Attributes:** Each node represents an image with its feature vector and 6-DoF absolute camera pose (quaternion and translation).
- **Edge Attributes:** Edges represent relative camera motions between frames.
- **Adjacency Tensor:** Encodes pixel-wise and image-wise correspondences, dynamically updated during training.

### 3. Graph Transformer Encoder

- **Message Passing:** Aggregates neighboring node features using the adjacency tensor.
- **Self-Attention Mechanism:** Utilizes multi-head self-attention with edge features to capture spatiotemporal relations.
- **Temporal Transformer Layers:** Optional layers enhance temporal dependencies for sequential inputs.

### 4. Graph Loss Function

- Combines graph consistency and pose prediction accuracy, guiding end-to-end training of the network.

## Key Contributions

### 1. Graph Transformer Backbone

- Integrates self-attention mechanisms with graph structures to capture global spatiotemporal dependencies.

### 2. Tensorized Adjacency Matrix

- Efficiently encodes and updates node and edge attributes, facilitating robust feature matching and graph evolution.

### 3. State-of-the-Art Performance

- Demonstrates significant improvements over existing methods on various benchmarks, including indoor and outdoor datasets.

## Results

- **Datasets:** Evaluated on 7Scenes, Cambridge Landmarks, and Oxford RobotCar datasets.
- **Performance:**
  - Outperforms state-of-the-art methods in terms of translation and rotation errors.
  - Shows robust performance in challenging environments with dynamic changes and occlusions.

## Detailed Structure of TransCamP Model

### 1. Initial Feature Extraction

- **CNN Backbone:** ResNet architecture pretrained on ImageNet extracts feature maps from input images.
- **Feature Embedding:** Feature maps are embedded in a view-graph with nodes representing image frames and edges representing inter-frame correlations.

### 2. Graph Embedding

- **Node Attributes:**
  - Feature vector from CNN.
  - 6-DoF camera pose vector (quaternion for orientation and 3D vector for translation).
- **Edge Attributes:**
  - Relative camera motions between frames.
- **Tensorized Adjacency Matrix:**
  - Encodes feature correspondences and normalized aggregated values, updated dynamically during training.

### 3. Graph Transformer Encoder

- **Message Passing:**
  - Aggregates neighboring node features using the adjacency tensor.
- **Self-Attention Mechanism:**
  - Multi-head self-attention with edge features captures spatiotemporal relations.
- **Temporal Transformer Layers (optional):**
  - Enhance temporal dependencies for sequential inputs.

### 4. Loss Function

- Combines consistency loss for graph structure and prediction accuracy for camera poses.
- **Loss Terms:**
  - Position loss $( L_x \)$ and orientation loss $( L_q \)$, balanced with learnable parameters.

## Training and Implementation

- **Optimization:**
  - Standard SGD optimizer with geometrically annealed learning rate.
- **Data Augmentation:**
  - Rescaling, cropping, and normalization of input images.
- **Hardware:** Implemented in PyTorch, trained on a machine with Intel i7 processor and Nvidia GeForce GPU.

By leveraging graph transformer layers and a tensorized adjacency matrix, TransCamP effectively addresses the challenges in 6-DoF camera pose estimation, offering a robust, efficient, and accurate solution for various computer vision applications.

