# EffLoc: Lightweight Vision Transformer for Efficient 6-DOF Camera Relocalization

![PTFormer Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/EffLoc.png)

## Problem Statement

Camera relocalization is pivotal in computer vision, with applications in augmented reality (AR), robotics, and autonomous driving. It involves estimating the 3D camera position and orientation (6-DoF) from images. Traditional methods like SLAM are accurate but computationally intensive, making them impractical for real-time applications. Recent advances in deep learning provide direct end-to-end pose estimation, but these methods often struggle with efficiency and robustness.

## Proposed Solution

This paper introduces EffLoc, a novel efficient Vision Transformer for single-image camera relocalization. EffLoc’s hierarchical layout, memory-bound self-attention, and feed-forward layers boost memory efficiency and inter-channel communication. The introduced Sequential Group Attention (SGA) module enhances computational efficiency by diversifying input features, reducing redundancy, and expanding model capacity. EffLoc excels in efficiency and accuracy, outperforming prior methods, such as AtLoc and MapNet.

## Model Structure

The EffLoc framework consists of several key components:

### 1. Initial Feature Extraction

- An EfficientNet-B0 convolutional backbone extracts activation maps at two different resolutions for position and orientation regression.

### 2. Transformer Encoders

- Separate encoders for positional and orientational features process the flattened activation maps with positional encodings to maintain spatial information.

### 3. Transformer Decoders

- Decoders generate latent pose representations for each scene, with outputs classified to select the respective scene embeddings for pose regression.

### 4. Loss Function

- Combines position and orientation loss with a Negative Log Likelihood (NLL) loss term for scene classification, balancing the errors with learned parameters.

## Key Contributions

### 1. Multi-Scene Transformer Architecture

- Applies transformers to aggregate task-specific features and embed multiple scenes, improving pose estimation accuracy across diverse environments.

### 2. Positional and Orientational Encoders

- Uses separate transformers for position and orientation, enhancing the extraction of informative image cues.

### 3. State-of-the-Art Performance

- Achieves superior accuracy for both multi-scene and single-scene APRs on benchmark datasets, demonstrating robustness and efficiency.

## Results

- Evaluated on Cambridge Landmarks and 7Scenes datasets.
- Outperforms MSPN and other APRs in terms of median position and orientation errors.
- Demonstrates strong performance across indoor and outdoor localization challenges.

## Detailed Structure of EffLoc Model

### 1. Initial Feature Extraction

EfficientNet-B0 extracts activation maps at resolutions $(14 \times 14 \times 112\)$ and $(28 \times 28 \times 40\)$ for position and orientation transformers, respectively.

### 2. Transformer Encoders

Flatten activation maps, add positional encodings, and process them through multi-head attention and MLP layers.

### 3. Transformer Decoders

Use self-attention and encoder-decoder attention to generate latent embeddings for each scene.
Scene classification selects the appropriate embeddings for pose regression.

### 4. Loss Function

Combines position loss $(\( L_x \))$, orientation loss $(\( L_q \))$, and NLL loss for scene classification.
Loss parameters are optimized to balance the different error components.

## Training and Implementation

- Optimization: Adam optimizer with an initial learning rate of $( 10^{-4} \)$.
- Data Augmentation: Includes rescaling, cropping, and normalization.
- Hardware: Implemented in PyTorch, trained on an Nvidia GeForce GTX 1080 GPU.

