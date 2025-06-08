COMPARISON TABLE

| Model | Test Accuracy(in %) |
| --- | --- |
| 8 layer CNN | 69.71 |
| 12 layer CNN | 86.84 |
| 14 layer CNN | 67.29 |
| 19 layer CNN | 10.00 |
| 5 layer ANN(simple ANN) | 59.00 |
| 10 layer ANN | 58.00 |
| VGG16 | 92.00 |
| VGG19 | 75.39 |
| Resnet50 | 94.00 |
| Resnet152 | 95.00 |
| AlexNet | 91.10 |
| LeNet | 63.00 |
SUMMARY REPORT

VGG models

It is a typical deep Convolutional Neural Network (CNN) design with numerous layers, and the abbreviation VGG stands for Visual Geometry Group. The term “deep” describes the number of layers, with VGG-16 or VGG-19 having 16 or 19 convolutional layers, respectively.

1. VGG16 model

VGG16 is a type of CNN that is considered to be one of the best computer vision models to date. The creators of this model evaluated the networks and increased the depth using an architecture with very small (3 × 3) convolution filters, which showed a significant improvement on the prior-art configurations. They pushed the depth to 16–19 weight layers making it approx — 138 trainable parameters.

- An accuracy of 92% was achieved by the model after training on the CIFAR-10 dataset.

![image](https://github.com/user-attachments/assets/5c150a34-bb50-4771-878b-3cc228e44bb4)


2. VGG19 model

The VGG19 model has the same basic idea as the VGG16 model, with the exception that it supports 19 layers. The numbers “16” and “19” refer to the model’s weight layers. In comparison to VGG16, VGG19 contains three extra convolutional layers.

- An accuracy of 75.39% was achieved by the model after training on the CIFAR-10 dataset


  CNN Models

A Convolutional Neural Network (CNN), also known as ConvNet, is a specialized type of deep learning algorithm mainly designed for tasks that necessitate object recognition, including image classification, detection, and segmentation.

We have used CNN models with different layers – 8, 12, 14 and 19. It was expected that the accuracy would increase on adding more layers but that turned out to be false. At first the accuracy increased from 70.20% in 8-layer to 86.84% in 12-layer since more features are getting extracted. But then it declines to 67.29% in 14-layer and 10% in 19-layer. Due to overfitting, additional stacked layers slow network speed. Specifically the model has reduced training error but larger testing error. As the network depth rises, the accuracy saturates and declines quickly.

CNN 14

![image](https://github.com/user-attachments/assets/e15a53df-423a-479c-8845-aeb482fe294c)

CNN 12

![image](https://github.com/user-attachments/assets/0069001b-1a68-4dd4-aafb-9e3e7d0edf04)

CNN 19

![image](https://github.com/user-attachments/assets/31679d22-aafb-497a-ad2d-b0048763deee)

CNN 8

![image](https://github.com/user-attachments/assets/a175a829-89d6-4878-a473-9c20a944b48c)

ResNet models

ResNet (Residual Network) models are deep convolutional neural networks that leverage residual connections to enable training of very deep networks without vanishing gradients.

ResNet-50

- Depth: 50 layers
- Architecture: Uses bottleneck structures (3-layer blocks) for efficiency.
- Performance: Achieves good accuracy with a balance between depth and computational cost.

![WhatsApp Image 2025-06-09 at 00 19 02_dfe5f684](https://github.com/user-attachments/assets/6ec5bfe2-e524-40cd-a738-13a72d3636b7)


ResNet-152

- Depth: 152 layers
- Architecture: Also uses bottleneck structures for efficiency.
- Performance: Provides higher accuracy, but at the cost of increased computational complexity.
- ResNet-50 is generally faster for inference due to its lower complexity.
- ResNet-152 will have a larger model size due to the additional parameters.

![image](https://github.com/user-attachments/assets/44c0cf24-d3db-459c-a6a9-88aecf3c2a5d)


We achieved an accuracy of **94% on ResNet-50** and **95% on ResNet-152** after training them on the CIFAR-10 dataset.

**CIFAR-10 Classification Report using Fine-Tuned AlexNet**

**1\. Model and Training Setup**

- **Model Used**: Pre-trained AlexNet from torchvision.models
- **Classifier Modification**: Final layers replaced to output 10 classes
- **Input Size**: 224×224 pixels
- **Loss Function**: CrossEntropyLoss
- **Optimizer**: Adam (learning rate = 1e-4)
- **Regularization**: Dropout layers added to the classifier
- **Gradient Clipping**: Max norm of 1.0
- **Learning Rate Adjustment**: Reduced by 10% after epoch 5
- **Epochs**: 10
- **Batch Size**: 32
- **Augmentations**: Horizontal flip applied during training

  **2\. Performance Metrics**

**2.1 Accuracy**

After training for 10 epochs, the model achieved the following performance on the test dataset:

- **Test Accuracy**: 91.10%

**2.2 Classification Report**

Below is the detailed classification report showing precision, recall, and F1-score for each class:

![image](https://github.com/user-attachments/assets/29b9b8eb-d6ac-4d20-af78-1927e2a1c0ba)

**2.3 Confusion Matrix**

The confusion matrix summarizes the model's predictions for each class:

![image](https://github.com/user-attachments/assets/74dbb305-927f-496d-b7e1-16bf4ea1c513)

**2.4 ROC Curve and AUC**

Using a one-vs-rest approach, ROC curves were plotted for each class using the model's predicted probabilities (softmax outputs). The average AUC was also computed.

- **average AUC**: 0.9956

  ![image](https://github.com/user-attachments/assets/4575786e-b4e0-41e1-831d-f786e86f87a9)

**3\. Training and Validation Trends**

Below is the plot showing the trend of training and validation losses over 10 epochs:
![image](https://github.com/user-attachments/assets/8aacc1f4-3b77-4b12-ac75-1e2c83b81797)

**CIFAR-10 Classification Report using ANN (9 hidden layers)**

**1\. Dataset**

- **Dataset Used**: CIFAR-10
- **Number of Classes**: 10
- **Image Dimensions**: 32 × 32 × 3
- **Train/Validation Split**: 80% training, 20% validation (from original training set)
- **Test Set Size**: 10,000 images

**2\. Data Preprocessing and Augmentation**

- **Training Transforms**: Random horizontal flip, random cropping with padding, normalization
- **Test/Validation Transforms**: Normalization only
- **Normalization Parameters**: Mean = (0.5, 0.5, 0.5), Std = (0.5, 0.5, 0.5)

**3\. Model Architecture**

A fully connected deep ANN was implemented with the following characteristics:

- **Input Size**: 3 × 32 × 32 = 3072
- **Hidden Layers**: 9 hidden layers with sizes:  
    2500 → 2000 → 2000 → 1000 → 1000 → 500 → 500 → 250 → 100
- **Activation**: ReLU
- **Batch Normalization**: Applied after each layer
- **Dropout**: Applied progressively (0.2 in early layers, 0.1 in later layers)
- **Output Layer**: Linear layer with 10 outputs (one per class)

**4\. Training Details**

- **Loss Function**: CrossEntropyLoss
- **Optimizer**: Adam (learning rate = 0.001)
- **Learning Rate Scheduler**: StepLR (step_size = 10, gamma = 0.5)
- **Epochs**: 30
- **Batch Size**: 64

**5\. Performance Metrics**

**5.1 Training Progress**

The model was trained for 30 epochs. Training loss, validation loss, and training accuracy were tracked.

![image](https://github.com/user-attachments/assets/43f80f12-daaf-496d-a915-670225236957)
![image](https://github.com/user-attachments/assets/5922f83e-38c0-4810-b436-c283d6a7c70a)

**5.2 Final Evaluation on Test Set**

- **Evaluation Metric**: Accuracy, Precision, Recall, F1-Score
  ![image](https://github.com/user-attachments/assets/fbbfef9b-6d29-4132-a700-0702ac8b4c00)

**Confusion Matrix:**
![image](https://github.com/user-attachments/assets/45099b2d-2ae4-4325-9902-649390ba8eac)

**5.3 ROC Curve and AUC (One-vs-Rest)**

Multi-class ROC analysis was performed using the model's softmax output.

- **Micro-average AUC**: 0.9155

**6\. Observations**

- Batch normalization and dropout improved stability and generalization.
- Training accuracy increased steadily, with validation decreased over epochs.
- Comparatively lower accuracy.

**Report: Artificial Neural Network (ANN) for CIFAR-10 Classification (4 hidden layers)**

**Data Preparation**

- **Dataset**: CIFAR-10 (60,000 images: 50,000 training, 10,000 test)
- **Data Splitting**:
  - Training set further split into 80% training (40,000 images) and 20% validation (10,000 images).
- **Data Augmentation** (Training only):
  - Random horizontal flip
  - Random cropping with padding of 4 pixels
- **Normalization**:
  - All images normalized to mean (0.5, 0.5, 0.5) and standard deviation (0.5, 0.5, 0.5) per channel to scale pixel values to roughly \[-1, 1\].

**Model Architecture**

The Improved ANN consists of:

- **Input layer**: Flattened image vector (3 channels × 32 height × 32 width = 3072 features)
- **Hidden layers**: Four fully connected (Linear) layers with sizes 2500, 2000, 1000, and 500 neurons respectively.
- **Activation**: ReLU non-linearity after each hidden layer
- **Batch Normalization**: After each linear layer to stabilize and accelerate training
- **Dropout**: To reduce overfitting, dropout rates of 0.2 for first two hidden layers and 0.1 for the last two.
- **Output layer**: Fully connected layer with 10 outputs corresponding to the CIFAR-10 classes.

**Training Details**

- **Loss function**: CrossEntropyLoss (suitable for multi-class classification)
- **Optimizer**: Adam optimizer with initial learning rate 0.001
- **Learning rate scheduler**: StepLR reducing learning rate by half every 10 epochs
- **Batch size**: 64
- **Epochs**: 30

**Training Performance**

- The model was trained for 30 epochs.
- Both training and validation losses decreased steadily, indicating effective learning.
- Training accuracy improved consistently, demonstrating the model's ability to fit the training data.
- Dropout and batch normalization helped mitigate overfitting and stabilized training.

**Loss Curves**

![image](https://github.com/user-attachments/assets/c7cbe55a-f9a7-44b2-9a8c-f08e5c1f3d13)

**Training Accuracy Curve**

![image](https://github.com/user-attachments/assets/4d1a9e36-5738-448c-a806-643ec4bc92c4)

**Evaluation on Test Data**

- **Test Accuracy**: The model achieved a test accuracy of 59% on unseen data.
- **Classification Report**:

![image](https://github.com/user-attachments/assets/9b26e721-3f98-4435-8195-7eba4e45869f)

**Confusion Matrix**:

![image](https://github.com/user-attachments/assets/56f35486-49cc-4d97-af48-e314534b579c)

- **ROC Curve and AUC**:
  - One-vs-All ROC curves plotted for each class.
  - Macro-average ROC AUC score: 0.9234

![image](https://github.com/user-attachments/assets/9a98236e-4e19-4997-8b7d-5ad10bb60f23)

**LeNet-5 Performance on CIFAR-10 Dataset**

**1\. Model Architecture**

The LeNet-5 architecture used consists of:

- **Convolutional layers:**
  - Conv1: 3 input channels → 6 output channels, kernel size 5x5
  - Conv2: 6 → 16 channels, kernel size 5x5
  - Conv3: 16 → 120 channels, kernel size 5x5
- **Pooling layers:**
  - Average pooling (2x2) after Conv1 and Conv2 layers
- **Fully connected layers:**
  - FC1: 120 → 84 neurons
  - FC2: 84 → 10 output neurons (classes)

Activation function: ReLU after each convolution and FC layer except the output layer.

**2\. Data Preprocessing and Augmentation**

To improve generalization, several data augmentation techniques were applied during training:

- Random horizontal flipping
- Color jittering (brightness, contrast, saturation adjustments)
- Random cropping with padding of 4 pixels
- Normalization with mean and standard deviation of (0.5, 0.5, 0.5) per channel

The dataset was split into 90% training and 10% validation sets. The test set was kept separate.

**3\. Training Setup**

- **Loss function:** Cross-Entropy Loss
- **Optimizer:** AdamW with initial learning rate 0.001
- **Learning rate scheduler:** StepLR (decays LR by 0.5 every 10 epochs)
- **Batch size:** 32
- **Epochs:** 30

**4\. Results**

**4.1 Training and Validation Loss**

- Training and validation losses decreased steadily over epochs, indicating effective learning.
- The learning rate scheduler helped stabilize training by reducing the learning rate midway, preventing overfitting.

![image](https://github.com/user-attachments/assets/6306a3cc-e38c-4159-a17c-36cc4b98f4c6)

**4.2 Accuracy**

- Final training accuracy reached approximately 65.12% 
- Final validation accuracy reached approximately 63.28**%**

**4.3 Test Set Evaluation**

- The model was evaluated on the CIFAR-10 test set.
- The classification report shows precision, recall, and F1-score for each class.
- The confusion matrix highlights the class-wise performance and misclassification trends.
![image](https://github.com/user-attachments/assets/af915473-d647-4e96-9024-90f887c8bce6)
![image](https://github.com/user-attachments/assets/58be051b-ed96-4b24-9e00-92daed703cb3)

**5\. Detailed Metrics**

**5.1 Classification Report**

**5.2 ROC Curves and AUC**

- Multi-class ROC curves were plotted using one-vs-rest approach.
- Area Under Curve (AUC) values indicate strong discriminative power across classes.
- Most classes achieved AUC > 0.90, with some variation.
![image](https://github.com/user-attachments/assets/c6c1072e-2a57-46b2-a09e-3fe44b68becc)

**5.3 Precision-Recall Curves**

- Precision-Recall (PR) curves were plotted for each class.
- Average precision (AP) scores were computed.

![image](https://github.com/user-attachments/assets/6be9c0d6-5e32-4fb3-80e8-f29d415aa6d0)


