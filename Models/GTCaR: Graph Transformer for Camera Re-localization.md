# Abstract of "GTCaR: Graph Transformer for Camera Re-localization"

![GTCaR Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/Gtcr.png)

## Problem Statement

Camera re-localization, or absolute pose regression (APR), is essential in various computer vision tasks such as visual odometry, structure from motion (SfM), and SLAM. Traditional methods, reliant on photometric consistency and geometric constraints, are computationally demanding and struggle in complex environments. Deep learning approaches, especially those using Convolutional Neural Networks (CNNs) and Graph Neural Networks (GNNs), have shown promise but often fall short in efficiency and robustness.

## Proposed Solution

This paper introduces GTCaR (Graph Transformer for Camera Re-localization), a novel neural network framework with a graph transformer backbone. GTCaR effectively integrates image features, camera pose information, and inter-frame relative camera motions into graph attributes. By employing graph transformer layers with edge features and an adjacency tensor, GTCaR dynamically captures global attention, significantly enhancing computational efficiency, robustness, and accuracy. The model also includes optional temporal transformer layers to improve spatiotemporal relations for sequential inputs.

## Model Structure

GTCaR comprises several key components:

### 1. Initial Feature Extraction

- RGB images are processed through a pre-trained CNN to extract feature maps.
- These feature maps form the initial view-graph with nodes representing images and edges encoding inter-frame correlations.

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

### 2. Adjacency Tensor

- Efficiently encodes and updates node and edge attributes, facilitating robust feature matching and graph evolution.

### 3. State-of-the-Art Performance

- Demonstrates significant improvements over existing methods on various benchmarks, including indoor and outdoor datasets.

## Results

- **Datasets:** Evaluated on 7-Scenes, Cambridge Landmarks, and Oxford RobotCar datasets.
- **Performance:** Outperforms state-of-the-art methods in terms of translation and rotation errors, showing robust performance in challenging environments.

## Detailed Structure of GTCaR Model

### 1. Initial Feature Extraction

- The pre-trained CNN extracts feature maps from input images.

### 2. Graph Embedding

- **Node Attributes:** Feature vector from CNN and 6-DoF camera pose vector.
- **Edge Attributes:** Relative camera motions.
- **Adjacency Tensor:** Encodes feature correspondences and normalized aggregated values, updated dynamically during training.

### 3. Graph Transformer Encoder

- **Message Passing:** Aggregates neighboring node features.
- **Self-Attention Mechanism:** Multi-head self-attention with edge features captures spatiotemporal relations.
- **Temporal Transformer Layers (optional):** Enhance temporal dependencies for sequential inputs.

### 4. Loss Function

- Combines consistency loss for graph structure and prediction accuracy for camera poses.

## Training and Implementation

### Optimization

- Standard SGD optimizer with a geometrically annealed learning rate.

### Data Augmentation

- Rescaling, cropping, and normalization of input images.

### Hardware

- Implemented in PyTorch, trained on a machine with Intel i7 processor and Nvidia GeForce GPU.

By leveraging graph transformer layers and a dynamic adjacency tensor, GTCaR effectively addresses the challenges in camera re-localization, offering a robust, efficient, and accurate solution for various computer vision applications.
