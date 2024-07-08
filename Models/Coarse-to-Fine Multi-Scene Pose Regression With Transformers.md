## Coarse-to-Fine Multi-Scene Pose Regression With Transformers

![CoVisPose Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/Caorsetofine.png)


### Problem Statement
Absolute camera pose regressors, which estimate the position and orientation of a camera given an image, face challenges when learning multiple scenes. Existing methods, typically using a convolutional backbone with a multi-layer perceptron (MLP) head, struggle to embed multiple scenes simultaneously, resulting in suboptimal localization accuracy. The challenge is to extend these methods to handle multiple scenes effectively.

### Proposed Solution
This paper introduces a novel Coarse-to-Fine Multi-Scene Pose Regression framework using Transformers. By leveraging self-attention mechanisms, the proposed method aggregates activation maps to focus on informative features for localization. The framework introduces a mixed classification-regression architecture to improve localization accuracy across multiple scenes.

### Model Structure
The Coarse-to-Fine framework consists of several key components:

1. **Convolutional Backbone:**
   - A convolutional network extracts feature maps from input images.
   - Separate feature maps are extracted for position and orientation estimation tasks.

2. **Transformer Encoders:**
   - Separate encoders for position and orientation aggregate features using self-attention.
   - The encoders adaptively focus on localization-informative image content.

3. **Transformer Decoders:**
   - Decoders transform the encoded features into pose predictions.
   - Each scene is encoded with latent embeddings, which are selected based on the input image.

4. **Coarse-to-Fine Classification-Regression:**
   - Scene classification is performed to identify the relevant scene from which the image was taken.
   - Position and orientation embeddings are refined using residual regression to improve pose estimates.

### Key Contributions
1. **Multi-Scene Pose Regression with Transformers:**
   - Introduces a novel approach to multi-scene absolute pose regression using transformer encoders and decoders.
   - Encodes scene-specific information while aggregating general localization features.

2. **Mixed Classification-Regression Architecture:**
   - Combines classification and regression to handle coarse-to-fine pose estimation.
   - Quantizes position and orientation domains for initial estimates, followed by residual refinement.

3. **State-of-the-Art Performance:**
   - Achieves new state-of-the-art accuracy for both single-scene and multi-scene absolute pose regression.
   - Demonstrates superior performance on benchmark indoor and outdoor datasets.

### Results
**Datasets:** Evaluated on Cambridge Landmarks and 7Scenes datasets.

**Performance:**
- Achieves state-of-the-art results in multi-scene pose regression.
- Outperforms existing methods in both position and orientation accuracy.

### Detailed Structure of Coarse-to-Fine Model
1. **Convolutional Backbone:**
   - EfficientNet-B0 backbone extracts feature maps at two different resolutions for position and orientation tasks.

2. **Transformer Encoders:**
   - Self-attention mechanisms in encoders aggregate positional and orientational features separately.
   - Outputs are further processed to enhance localization accuracy.

3. **Transformer Decoders:**
   - Decoders transform the aggregated features into scene-specific latent embeddings.
   - Scene classification is performed to select the relevant embeddings.

4. **Pose Classification-Regression:**
   - Coarse position and orientation estimates are refined using residual regression.
   - Final pose is obtained by summing the selected centroids and regressed residuals.


