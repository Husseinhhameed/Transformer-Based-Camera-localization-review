# Abstract of "EAAINet: An Element-Wise Attention Network With Global Affinity Information for Accurate Indoor Visual Localization"

![EAAINet Architecture](https://github.com/Husseinhhameed/Transformer-Based-Camera-localization-review/blob/main/images/EAAINet.png)

## Problem Statement

Visual localization, a vital component of many visual applications, has been tackled by scene coordinates regression (SCoRe) methods that leverage neural networks to predict scene coordinates, followed by a PnP algorithm to recover camera pose. However, these methods do not consider the relationship between image patches, known as relative features or affinity information, which is instrumental for the network to perform complete scene parsing. Additionally, due to the visual similarity between image patches, these methods are weak in extracting reliable absolute features that represent the context information of the image patches, resulting in inferior localization performance.

## Proposed Solution

This paper introduces EAAINet, based on classical SCoRe approaches and consists of two novel modules: the Global Affinity Aggregation Module (GAAM) and the Element-wise Attention Module (EAM). GAAM employs an interval sampling strategy to sample image patches to construct sparse graph neural networks (GNNs), retrieving global affinity information between image patches. EAM integrates multi-level features to generate reliable absolute features to regress accurate scene coordinates.

## Model Structure

The proposed model comprises several key components:

### 1. Initial Feature Extraction

- Uses a modified ResNet18 to extract multi-level features with varying receptive fields.

### 2. Positional Encoding

- Attaches distinctive positional information to the features to differentiate similar pixels, enhancing the model's ability to handle repetitive texture regions.

### 3. Global Affinity Aggregation Module (GAAM)

- Constructs sparse GNNs to concurrently extract the relationship of similar and dissimilar image patches, generating global affinity information for precise scene parsing.

### 4. Element-wise Attention Module (EAM)

- Predicts element-wise soft attention masks to reconcile multi-level feature maps, allowing efficient feature fusion and distinguishing similar image patches.

### 5. Pose Estimation

- Utilizes a regression layer to predict dense scene coordinates and uncertainties, followed by a RANSAC-based PnP algorithm to calculate 6-DOF camera pose.

### 6. Loss Function

- Maximizes the logarithmic likelihood of the probability density function of the predicted scene coordinates, incorporating uncertainties into the regression.

## Key Contributions

1. **Global Affinity Aggregation Module (GAAM):** Extracts relationships of similar and dissimilar image patches concurrently for complete scene parsing.
2. **Element-wise Attention Module (EAM):** Generates soft attention masks to fuse multi-level features, obtaining reliable absolute features.
3. **State-of-the-Art Performance:** Achieves significant performance improvements on multiple benchmarks with fewer parameters and faster speed.

## Results

- **Datasets:** Evaluated on 7-Scenes and 12-Scenes datasets.
- **Performance:** Outperforms state-of-the-art methods in terms of median positional and rotational errors, achieving higher localization accuracy.

## Conclusion

EAAINet provides a robust and efficient solution for visual localization by integrating GAAM and EAM into a classical SCoRe network. This approach enhances the extraction of discriminative relative and absolute features, resulting in improved scene parsing and localization accuracy.

## Detailed Structure of EAAINet Model

### 1. Initial Feature Extraction

- **Backbone:** Modified ResNet18, retaining the first convolutional layer and four Resblocks, with multi-level features (F1, F2, F3, F4, F5) extracted.

### 2. Positional Encoding

- **2D Positional Encoding:** Attached to F1 to provide unique positional information to all pixels, enhancing feature differentiation.

### 3. Global Affinity Aggregation Module (GAAM)

- **Interval Sampling Strategy:** Extracts similar and dissimilar image patches to construct sparse GNNs, generating global affinity information.

### 4. Element-wise Attention Module (EAM)

- **Soft Attention Masks:** Generated for multi-level feature maps to emphasize vital information and suppress irrelevant messages during feature fusion.

### 5. Pose Estimation

- **Regression Layer:** Fully convolutional structure predicting 3D scene coordinates and uncertainties, followed by a RANSAC-based PnP algorithm for pose calculation.

### 6. Loss Function

- **Regression Loss:** Combines the errors of predicted scene coordinates and uncertainties, maximizing the likelihood of the probability density function.

## Training and Implementation

### Optimization

- **Optimizer:** Adam optimizer with an initial learning rate of $(2 \times 10^{-4}\)$.
- **Training:** Conducted for 400 epochs with a batch size of 4, using data augmentation to prevent overfitting.

### Data Augmentation

- **Techniques:** Includes affine transformations and additive brightness changes.

### Hardware

- **Implementation:** Developed in PyTorch, trained on an Intel Core i7-9700K CPU with a single NVIDIA TITAN RTX GPU.

By leveraging the novel GAAM and EAM modules, EAAINet achieves state-of-the-art visual localization performance with reduced model parameters and faster inference speed, setting a new standard in the field.
