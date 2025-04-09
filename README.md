# <p align="center">ML4SCI_25</p>
# Foundation Models for End-to-End Event Reconstruction

---

## Common Task 1: Electron/Photon Classification

This section evaluates four ResNet-15-based classification models trained using different configurations of the calorimeter data (time and energy channels).

### Implemented Approaches

1.  **Time-Only Classification**: Uses only the time channel as input to ResNet-15.
2.  **Energy-Only Classification**: Uses only the energy channel as input to ResNet-15.
3.  **Dual-Stream Feature Concatenation**: Dual-Stream ResNet-15 Feature Fusion: Two independent ResNet-15 branches are used to extract features separately from time and energy channels. The resulting feature vectors are concatenated before passing through a final linear layer for binary classification.
4.  **Two-Channel Input Model**: Both time and energy fed as a 2-channel input into a single ResNet-15 model.

---

### Results (Task 1)

| Approach                          | Test Accuracy | Test ROC-AUC | ROC Curve Plot                                                                                                |
| --------------------------------- | ------------- | ------------ | ------------------------------------------------------------------------------------------------------------- |
| Channel2-Only Classification      | 62.25%        | 0.6665       | <img src="https://github.com/user-attachments/assets/b14d5f24-0cce-4d5f-87ca-5494d7e6c4b8" width="400" alt="Channel 2 ROC Curve">   |
| Channel1-Only Classification      | 74.45%        | 0.8158       | <img src="https://github.com/user-attachments/assets/7467ebcb-5410-4670-aded-5a027b3e8076" width="400" alt="Channel 1 ROC Curve">   |
| Dual-Stream Feature Concatenation | 74.36%        | 0.8142       | <img src="https://github.com/user-attachments/assets/ca01ed4f-6153-485b-8366-3af1421aa129" width="400" alt="Dual Stream ROC Curve"> |
| Two-Channel Input Model           | 74.35%        | 0.8136       | <img src="https://github.com/user-attachments/assets/0650e36e-742a-4e3a-9b4c-871f305fe844" width="400" alt="Two Channel ROC Curve"> |

---

## Specific Task 2i: Self-Supervised Foundation Models for Event Reconstruction

This task involved building foundation models using Self-Supervised Learning (SSL) for end-to-end event reconstruction, including particle classification and property regression.

### Implementation Details

1.  **Foundation Model Pre-training:**
    * A SimCLR-style self-supervised learning (SSL) pipeline was implemented to learn high-quality representations from unlabeled calorimeter images. Two backbone encoders were evaluated:

    | Model Name          | Description                                                                 |
    | :------------------ | :-------------------------------------------------------------------------- |
    | **ResNetSSL** | Modified ResNet-18 with 8 input channels and a SimCLR projection head.      |
    | **ParticleTransformer**| Hybrid CNN-Transformer encoder with learned positional encoding and mean pooling. |

2.  **Downstream Task Implementation:**
    * Latent vectors were extracted from the labeled dataset using each pretrained encoder. These vectors were then used to train **shallow downstream models** for:
        * **Classification (logit y)** using a **single hidden-layer MLP** with ReLU activation and sigmoid output.
        * **Regression (pT, m)** using a **shallow MLP** with one hidden layer, batch normalization, ReLU activation, dropout, and a linear output layer.

---

### Classification Results (Logit y)

| Encoder             | Accuracy | ROC-AUC | ROC Curve Plot                                                                                                |
| :------------------ | :------- | :------ | :------------------------------------------------------------------------------------------------------------ |
| ResNetSSL           | 86.33%   | 0.9357  | <img src="https://github.com/user-attachments/assets/4add51e7-1ed1-4105-9a89-5be21e0e5732" width="400" alt="ResNetSSL Classification ROC Curve">   |
| ParticleTransformer | 84.60%   | 0.9247  | <img src="https://github.com/user-attachments/assets/d3cc602d-35fb-4ea5-b7ba-5221f0523081" width="400" alt="ParticleTransformer Classification ROC Curve"> |

### Regression Results

#### Invariant Mass (m)

| Encoder             | MSE     | F1 Score | True vs Predicted Plot                                                                                               |
| :------------------ | :------ | :------- | :------------------------------------------------------------------------------------------------------------------- |
| ResNetSSL           | 884.57  | 0.8822   | <img src="https://github.com/user-attachments/assets/1bbd4eb0-501d-49ad-92f5-3a2a88edb8e0" width="400" alt="ResNetSSL m True vs Predicted Plot">   |
| ParticleTransformer | 980.98  | 0.8490   | <img src="https://github.com/user-attachments/assets/87d3a493-c1f5-4746-aa75-9a6c4901938a" width="400" alt="ParticleTransformer m True vs Predicted Plot"> |

#### Transverse Momentum (pT)

| Encoder             | MSE       | F1 Score | True vs Predicted Plot                                                                                           |
| :------------------ | :-------- | :------- | :--------------------------------------------------------------------------------------------------------------- |
| ResNetSSL           | 10108.98  | 0.6639   | <img src="https://github.com/user-attachments/assets/b31a39fb-05fa-4b14-b848-f815b34485dd" width="400" alt="ResNetSSL pT True vs Predicted Plot">    |
| ParticleTransformer | 9255.75   | 0.6616   | <img src="https://github.com/user-attachments/assets/10031a00-a965-48b8-abbd-bd5a15c309a9" width="400" alt="ParticleTransformer pT True vs Predicted Plot"> |

---
