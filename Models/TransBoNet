# TransBoNet: Learning Camera Localization with Transformer Bottleneck and Attention

![PTFormer Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/Transbonet.png)

### Problem Statement

Estimating the pose of a camera from a single image is crucial for various applications such as augmented reality, autonomous driving, and indoor navigation. Traditional 3D structure-based methods or image retrieval approaches are often sensitive to viewpoint changes, illumination variations, and dynamic objects, making them less robust in unconstrained environments. Deep neural networks (DNNs) have shown potential for camera localization but still struggle with robustness in dynamic settings.

### Proposed Solution

This paper proposes TransBoNet, a framework that integrates a hybrid attention mechanism to enhance the robustness of CNN-based pose regressors. The core component is the novel Transformer Bottleneck (TBo) block, which includes convolution, channel attention, and a position-aware self-attention mechanism. This block captures long-term dependencies between pixels, allowing the network to extract more geometrically robust features. Additionally, a shuffle attention (SA) module is introduced before the pose regressor to integrate feature information in both spatial and channel dimensions.

### Model Structure

The proposed model comprises several key components:

#### 1. Initial Feature Extraction

- Uses a ResNet50 backbone followed by a height compression module (HCM) to extract image-column feature sequences from 360° panoramas.

#### 2. Transformer Bottleneck Block

- **Convolutional Layer:** Extracts local features from the input image.
- **Channel Attention Module:** Evaluates the importance of each channel, retaining the most significant information.
- **Position-aware Multi-Head Self-Attention (MHSA):** Captures global context and relative position information.

#### 3. Shuffle Attention Module

- **Channel Attention Branch:** Generates attention feature maps by analyzing inter-channel relationships.
- **Spatial Attention Branch:** Generates spatial attention maps by analyzing spatial location relationships.

#### 4. Pose Regressor

- **MLP Head:** Maps the attention-guided features to the camera pose, including 3D location and 4D orientation (quaternion).

### Key Contributions

#### 1. Transformer Bottleneck Block

- Introduces self-attention and channel attention to improve fine-grained feature extraction for accurate localization.

#### 2. Hybrid Attention Network

- Improves the accuracy and robustness of camera localization, especially in dynamic scenes.

#### 3. Extensive Experimental Validation

- Demonstrates superior performance on indoor (7Scenes) and outdoor (Oxford RobotCar) datasets, outperforming contemporary pose regressors.

### Results

#### - Indoor Localization (7Scenes):

- TransBoNet achieves the best positional error in five of the seven scenes, with significant improvements in scenes with texture-less regions and repetitive textures.

#### - Outdoor Localization (Oxford RobotCar):

- Shows robust performance in complex environments, significantly reducing position and rotation errors.

### Detailed Structure of TransBoNet Model

#### 1. Feature Encoder

- **Architecture:** ResNet50 with embedded SE layers in each residual block.
- **Modifications:** Replaces the final classification layer with a 2048-dimensional fully-connected layer.

#### 2. Transformer Bottleneck Block

- **Channel Attention:** Uses scalars to represent the importance of each channel.
- **Position-aware MHSA:** Incorporates 2D relative position self-attention for visual localization tasks.

#### 3. Shuffle Attention Module

- **Channel Attention Branch:** Generates channel attention feature maps.
- **Spatial Attention Branch:** Generates spatial attention maps.

#### 4. Pose Regressor

- **Structure:** MLP head that maps attention-guided features to the 3D position and 4D orientation (quaternion).
- **Loss Function:** Combines L1 loss for position and orientation, with learnable parameters controlling the balance between the losses.

### Training and Implementation

- **Optimization:** Adam optimizer with an initial learning rate of $( 5 \times 10^{-5} \)$.
- **Data Augmentation:** Includes rescaling, cropping, and normalization.
- **Hardware:** Implemented in PyTorch, trained on a NVIDIA GeForce RTX 2070 GPU.

