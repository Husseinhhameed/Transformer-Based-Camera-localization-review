## NeuMap: Neural Coordinate Mapping by Auto-Transdecoder for Camera Localization

![MSFA-T Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/NeuMap.png

### Problem Statement
Visual localization, which determines camera position and orientation based on image observations, is critical for applications such as VR/AR and self-driving cars. Existing methods, especially those relying on large databases of keypoints and 3D point clouds, face challenges in terms of storage size and performance under high compression rates. These methods also struggle with large viewpoint and illumination changes, leading to reduced robustness and accuracy.

### Proposed Solution
This paper introduces NeuMap, a novel end-to-end neural mapping method for camera localization. NeuMap encodes a scene into a compact grid of latent codes, which are used by a Transformer-based auto-decoder to regress the 3D coordinates of query pixels. This approach significantly reduces the storage requirements while maintaining high localization accuracy. NeuMap leverages learnable latent codes and a scene-agnostic Transformer-based auto-decoder to achieve robust and efficient camera localization.

### Model Structure
The NeuMap framework consists of several key components:

1. **Scene Representation and Feature Extraction:**
   - The scene is represented by a set of latent codes stored in a sparse grid of voxels.
   - A shared CNN extracts robust features from images, which are used to regress 3D scene coordinates.

2. **Auto-Transdecoder:**
   - A Transformer-based auto-decoder regresses 3D coordinates of query pixels by cross-attending to the latent codes.
   - The auto-transdecoder consists of multiple transformer blocks that refine the features and improve coordinate regression accuracy.

3. **Coordinate Regression and Voxel Pruning:**
   - Scene coordinate regression is performed on sparse features extracted from query images.
   - Redundant codes are pruned to reduce the representation size without sacrificing performance.

### Key Contributions
1. **Neural Coordinate Mapping (NeuMap):**
   - Proposes a novel neural mapping method using a Transformer-based auto-decoder for efficient camera localization.
   - Encodes scenes into compact latent codes, significantly reducing storage requirements while maintaining high accuracy.

2. **Robust Feature Extraction:**
   - Utilizes a shared CNN to extract robust features from images, enabling effective regression of 3D coordinates.

3. **Efficient Scene Representation:**
   - Demonstrates the effectiveness of NeuMap in compressing scene representations by up to 1000 times without performance drop.

4. **State-of-the-Art Performance:**
   - Outperforms existing coordinate regression methods and achieves competitive results with feature matching methods on benchmark datasets.

### Results
**Datasets:** Evaluated on five benchmarks: 7scenes, ScanNet, Cambridge Landmarks, Aachen Day & Night, and NAVER LABS.

**Performance:**
- Achieves state-of-the-art results in camera localization with significantly smaller scene representation sizes.
- NeuMap demonstrates superior performance, especially in large-scale and high-compression scenarios.

### Detailed Structure of NeuMap Model
1. **Scene Representation and Feature Extraction:**
   - The scene is divided into sub-regions, each represented by latent codes stored in a sparse voxel grid.
   - A shared CNN extracts image features, which are then used by the auto-transdecoder to regress 3D coordinates.

2. **Auto-Transdecoder:**
   - The auto-transdecoder consists of multiple transformer blocks that refine features through cross-attention with latent codes.
   - Final scene coordinates and confidence scores are computed using a multi-layer perceptron (MLP).

3. **Voxel Pruning:**
   - Redundant codes are pruned using a sparsity factor, significantly reducing the data size without sacrificing performance.


