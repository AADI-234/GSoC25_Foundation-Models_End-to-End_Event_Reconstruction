# <p align="center">ML4SCI_24</p>
# Foundation Models for End-to-End Event Reconstruction

---

## Common Task 1: Electron/Photon Classification

This section evaluates four ResNet-15-based classification models trained using different configurations of the calorimeter data (time and energy channels).

### Implemented Approaches

1. **Time-Only Classification**: Uses only the time channel as input to ResNet-15.  
2. **Energy-Only Classification**: Uses only the energy channel as input to ResNet-15.  
3. **Dual-Stream Feature Concatenation**: Two independent ResNet-15 branches for time and energy, features concatenated before final classifier.  
4. **Two-Channel Input Model**: Both time and energy fed as a 2-channel input into a single ResNet-15 model.

---

### Results (Task 1)

| Approach                          | Accuracy (%) | ROC-AUC | Notes                                  |
|-----------------------------------|--------------|---------|----------------------------------------|
| Channel1-Only Classification      |    74.45     | 0.8158  | Uses only channel 1                    |
| Channel2-Only Classification      |    62.25     | 0.6665  | Uses only channel 2                    |
| Dual-Stream Feature Concatenation |    74.36     | 0.8142  | Concatenated features from both        |
| Two-Channel Input Model           |    74.35     | 0.8136  | Time & energy as 2-channel input       |

---

## Specific Task 2i: Self-Supervised Foundation Models for Event Reconstruction

This task involved building foundation models using Self-Supervised Learning (SSL) for end-to-end event reconstruction, including particle classification and property regression.

### Implementation Details

1.  **Foundation Model Pre-training:**
    * A SimCLR-style self-supervised learning (SSL) pipeline was implemented to learn high-quality representations from unlabeled calorimeter images. Two backbone encoders were evaluated:
    * The architectures implemented were:
        
        | Model Name          | Description                                                                 |
        |---------------------|-----------------------------------------------------------------------------|
        | **ResNetSSL**       | Modified ResNet-18 with 8 input channels and a SimCLR projection head.      |
        | **ParticleTransformer** | Hybrid CNN-Transformer encoder with learned positional encoding and mean pooling. |
                  
2.  **Downstream Task Implementation:**
    Latent vectors were extracted from the labeled dataset using each pretrained encoder. These vectors were then used to train **shallow downstream models** for:
    
    - **Classification (logit y)** using a **single hidden-layer MLP** with ReLU activation and sigmoid output.
    - **Regression (pT, m)** using a **shallow MLP** with one hidden layer, batch normalization, ReLU activation, dropout, and a linear output layer.


---

### Classification Results (Logit y)

| Encoder             | Accuracy | ROC-AUC |
|---------------------|----------|---------|
| ResNetSSL           | 86.33%   | 93.57%  |
| ParticleTransformer | 84.60%   | 92.48%  |

---

### Regression Results

#### Transverse Momentum (pT)

| Encoder             | MSE      | F1 Score |
|---------------------|----------|----------|
| ResNetSSL           | 10108.98 | 0.6639   |
| ParticleTransformer | 9255.75  | 0.6616   |

#### Invariant Mass (m)

| Encoder             | MSE     | F1 Score |
|---------------------|---------|----------|
| ResNetSSL           | 884.57  | 0.8822   |
| ParticleTransformer | 980.98  | 0.8490   |
