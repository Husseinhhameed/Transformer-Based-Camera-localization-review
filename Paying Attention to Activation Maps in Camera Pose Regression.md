# Abstract of "Paying Attention to Activation Maps in Camera Pose Regression"

![TransPoseNet Framework](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/Activation%20Maps.png)

## Problem Statement

Camera pose regression involves estimating the camera's 3D position and orientation from a single image, which is crucial for applications like augmented reality and autonomous driving. Traditional image retrieval-based localization methods are accurate but require substantial computational resources and real-time connectivity to large databases. Regression-based approaches offer a lightweight and fast alternative but often lack accuracy.

## Proposed Solution

This paper introduces an attention-based approach to camera pose regression. The proposed method uses convolutional activation maps as sequential inputs to Transformer encoders, allowing the network to focus on spatially-varying deep features. Two Transformer heads are used: one for regressing the camera position and another for the camera orientation. This dual encoder setup improves localization accuracy by emphasizing task-specific features in the input image.

## Model Structure

The proposed framework, named TransPoseNet, consists of the following components:

### 1. Convolutional Backbone

- An EfficientNet-B0 architecture is used to extract activation maps at two different resolutions.
- The activation maps are sampled at two reduction levels, \( m_{rdct4} \) and \( m_{rdct3} \), representing different scales.

### 2. Sequential Representations of Activation Maps

- Activation maps are transformed into sequences using 1x1 convolutions and flattened.
- A learned position or orientation token is appended to each sequence for respective tasks.

### 3. Positional and Orientational Encoders

- Two separate Transformer encoders process the sequences for position and orientation estimation.
- Positional encoding is applied to preserve spatial information.

### 4. Transformer Encoder Architecture

- Each encoder consists of multiple blocks, each containing a multi-head self-attention module and an MLP.
- Layer normalization and residual connections are used to stabilize the training.

### 5. MLP Head

- A simple MLP head regresses the camera position and orientation from the encoded representations.

## Key Contributions

### 1. Dual Transformer Encoders

- Utilizes two Transformer encoders to separately process features relevant for position and orientation estimation.
- Demonstrates the effectiveness of focusing on different image features for each task.

### 2. Attention Mechanism

- Visualizes attention weights to show how the network prioritizes spatial features such as corners for position and edges for orientation.

### 3. State-of-the-Art Performance

- Achieves state-of-the-art results on both indoor (7Scenes) and outdoor (Cambridge Landmarks) benchmarks.
- Demonstrates sub-meter average accuracy for outdoor scenes.

## Results

### Datasets

- Evaluated on Cambridge Landmarks (outdoor) and 7Scenes (indoor) datasets.

### Performance

- TransPoseNet outperforms other pose regression methods, achieving lower position and orientation errors.
- The method consistently performs better than image retrieval baselines and other regression-based approaches.

## Detailed Structure of TransPoseNet Model

### 1. Convolutional Backbone

- **Architecture:** EfficientNet-B0, chosen for its efficiency and focus on informative visual features.
- **Activation Maps:**
  - $( m_{rdct4} \in \mathbb{R}^{14 \times 14 \times 112} \)$
  - $( m_{rdct3} \in \mathbb{R}^{28 \times 28 \times 40} \)$

### 2. Sequential Representations of Activation Maps

- **Transformation:**
  - Activation maps are projected to a common depth dimension $( C_t = 256 \)$ using 1x1 convolutions.
  - Flattened into sequences $( \hat{M} \)$.

- **Token Addition:**
  - Learned position/orientation token $( t \in \mathbb{R}^{C_t} \)$ is appended to the sequence.

### 3. Positional Encoding

- **Encoding Vectors:**
  - Separate one-dimensional encodings for X and Y axes.
  - Concatenated to form positional embeddings $( E_{i,j}^{pos} \)$.

### 4. Transformer Encoder

- **Architecture:**
  - Each encoder consists of 6 identical blocks.
  - Each block has a multi-head attention (MHA) module and an MLP with two layers and GELU non-linearity.

- **Normalization and Residuals:**
  - LayerNorm before each module.
  - Residual connections and dropout for stability.

### 5. MLP Head

- **Structure:**
  - Hidden layer expands the dimension from 256 to 1024.
  - Final fully connected layer regresses the output vector (position or orientation).

### 6. Loss Function

- **Position Loss $( L_x \)$:** Euclidean distance between predicted and ground truth positions.
- **Orientation Loss $( L_q \)$:** Euclidean distance between normalized predicted and ground truth quaternions.
- **Combined Loss $( L_p \)$:**
  - Balances position and orientation losses using learned parameters $( s_x \)$ and $( s_q \)$.

## Training and Implementation

### Optimization

- **Adam optimizer** with initial learning rate $( \lambda = 10^{-4} \)$.
- Two-stage training: first minimizing the combined loss $( L_p \)$, then fine-tuning each MLP head separately.

### Augmentation

- Training images are rescaled, randomly cropped, and brightness, contrast, and saturation are jittered.
- At test time, only center cropping after rescaling is applied.

### Hardware

- Models trained on a single NVIDIA Tesla V100 GPU using PyTorch framework.

By leveraging the dual Transformer encoder architecture and attention mechanism, TransPoseNet effectively improves the accuracy of camera pose regression, offering a robust and efficient solution for various computer vision applications.
