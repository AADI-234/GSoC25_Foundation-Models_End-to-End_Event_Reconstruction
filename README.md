# <p align="center">ML4SCI_24 </p>



## Common Task 1. Electron/Photon Classification

### Project Resources

| Resource Type          | Description                                       | Link                                                                                        |
|------------------------|---------------------------------------------------|---------------------------------------------------------------------------------------------|
| **Directory**          | Complete collection of project files.             | [Common Task 1](Common_Task1)    |
| **Detailed Solution**  | Approach used     | [Approach]() |
| **Jupyter Notebook**   | Code and analysis in a Jupyter Notebook.      | [Open Notebook](Common_Task1/Common_Task1(cms).ipynb) |
| **PDF Version**        | Pdf of the notebook.                 | [PDF](Common_Task1/Common_Task1(cms).pdf) |
| **Model Weights**      | Model weights for replication and testing.    | [Model_Weights](Common_Task1/model_weights_Common_Task_1.pth)       |

### Results and Analysis

I carefully monitored the training progress over 15 epochs, ensuring optimal performance without overfitting. Below is the conclusion of training:

- **VAL Loss**: 0.2678
- **Val ROC-AUC**: 0.805 
- **Validation Accuracy**: 73.56%
- **Test Loss**: 0.5398
- **Test ROC-AUC**: 0.8044
- **Test Accuracy**: 73.46%


#### Below are the Loss, accuracy, and ROC-AUC curves for the architectures, illustrating the point of overfitting and the epoch at which the models were saved.

#

![Loss Curve](https://github.com/AADI-234/ML4SCI-GSoC24/assets/133188867/6fc8ed40-465b-4858-9ca7-c58cecf521c1)
- Monitors the model's convergence during training. A decreasing loss indicates learning progress, while sudden increases may indicate overfitting.


#

![ROC-AUC Curve](https://github.com/AADI-234/ML4SCI-GSoC24/assets/133188867/95c0aae7-6928-4ca5-ade3-4ea9d595f3c0)
- Evaluates the model's ability to distinguish between positive and negative classes in binary classification tasks. Higher AUC scores indicate better discrimination performance.


# 

![Accuracy Curve](https://github.com/AADI-234/ML4SCI-GSoC24/assets/133188867/ab9c590a-2134-4797-8f44-3fd6a5942e14) 
- Tracks the model's performance on the training, validation and test datasets. Helps assess how well the model generalizes to unseen data.
