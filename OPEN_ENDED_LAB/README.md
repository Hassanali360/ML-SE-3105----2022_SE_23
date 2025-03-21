# Introduction
The MNIST dataset consists of handwritten digits (0-9) represented as 28x28 grayscale images, flattened into 784-dimensional vectors with pixel intensities ranging from 0 to 255. The dataset is pre-split into training (`mnist_train.csv`, 60,000 samples) and testing (`mnist_test.csv`, 10,000 samples) sets. This lab leverages these preprocessed CSV files to train and evaluate classification models, exploring their performance on digit recognition in an open-ended framework.

## Methodology

### Dataset Preparation
- **Loading:** Loaded `mnist_train.csv` (60,000 rows × 785 columns) and `mnist_test.csv` (10,000 rows × 785 columns) into pandas DataFrames.
- **Feature and Label Separation:**
  - **Training:** `X_train` (60,000 × 784 features), `y_train` (labels).
  - **Testing:** `X_test` (10,000 × 784 features), `y_test` (labels).
- **Preprocessing:** No additional preprocessing (e.g., normalization, NaN handling, or feature selection) was applied, relying on the dataset’s pre-flattened structure and assuming no missing values as per the provided files.

### Models being Used:
- **Logistic Regression**
- **KNN**
- **Multi-Layer Perceptron (MLP - Neural Network)**


## Why These Three Models for MNIST?

### 1. Logistic Regression
- **Baseline Model:** Logistic Regression serves as a simple baseline for MNIST digit classification.
- **Works Well on Linearly Separable Data:** While digits are complex, Logistic Regression can still provide reasonable performance by learning a linear decision boundary.
- **Fast and Efficient:** Since MNIST consists of flattened 784-dimensional vectors, Logistic Regression can process them quickly without heavy computation.
- **Benchmark for Non-Linear Models:** Helps compare the effectiveness of more complex models like KNN and MLP.

### 2. K-Nearest Neighbors (KNN)
- **Instance-Based Learning:** Unlike Logistic Regression, KNN does not make assumptions about the data distribution, making it more adaptable to MNIST's complex patterns.
- **Captures Non-Linear Decision Boundaries:** Digits often overlap in feature space, and KNN’s distance-based classification helps distinguish them better.
- **Good Performance Without Training:** KNN does not require explicit training—just storing training instances and computing distances at inference time.
- **Handles Class Overlaps:** Some digits, such as 3 and 5 or 8 and 9, are visually similar. KNN’s voting mechanism helps mitigate misclassifications.

### 3. Multi-Layer Perceptron (MLP - Neural Network)
- **Learns Complex Patterns:** MLP can capture intricate pixel relationships in the 28x28 digit images that simpler models may miss.
- **Non-Linear Decision Boundaries:** Unlike Logistic Regression, MLP uses activation functions to model non-linearity, improving classification accuracy.
- **Feature Extraction Capability:** MLP automatically learns feature representations, reducing the need for manual preprocessing.
- **Better Generalization:** Neural networks are well-suited for high-dimensional data like MNIST and typically outperform traditional machine learning models.

## Things to notice:
- **Logistic Regression** is a strong baseline but struggles with non-linearity in MNIST.
- **KNN** effectively handles complex patterns but can be computationally expensive for large datasets.
- **MLP** offers the best performance due to its deep learning capabilities and ability to learn hierarchical features from pixel data.

## No need of any hyperparameter tunning, as basic settings choosed in Model training is enough for our needs and nature of project.


## Model Evaluation Metrics
To evaluate the models' performance, the following metrics were used:

- **Accuracy:** Measures the percentage of correctly classified instances out of the total test dataset.
- **Precision:** The proportion of true positive predictions among all predicted positives.
- **Recall:** The proportion of true positive predictions among actual positives.
- **F1-Score:** The harmonic mean of precision and recall, providing a balanced metric for model evaluation.
- **Confusion Matrix:** Provides a breakdown of correct and incorrect predictions for each class, helping to understand misclassification patterns.

## Results

### 1. Logistic Regression
- **Accuracy:** 92.5%
- **Classification Report:**
  - **Precision:** Ranges from 87% to 97%
  - **Recall:** Ranges from 87% to 98%
  - **F1-score:** Averages around 92%
- **Confusion Matrix:** 
![alt text](image-1.png)

  ### Most Confusions:
- **Digit 2 vs. 8:** (42 misclassifications of 2 as 8)
- **Digit 3 vs. 5:** (26 misclassifications of 3 as 5)
- **Digit 5 vs. 3:** (33 misclassifications of 5 as 3)
- **Digit 9 vs. 4:** (25 misclassifications of 9 as 4)

### Why?
- Logistic Regression is a linear model, meaning it struggles with capturing complex patterns in images.
- Digits **2 and 8** have similar rounded shapes, which makes misclassification common.
- Digits **3 and 5** share curved strokes, leading to confusion.
- Digit **9 can resemble 4** when written with a curved top.

### 2. K-Nearest Neighbors (KNN)
- **Accuracy:** 96.9%
- **Classification Report:**
  - **Precision:** Ranges from 95% to 99%
  - **Recall:** Ranges from 94% to 100%
  - **F1-score:** Averages around 97%
- **Confusion Matrix:** 
![alt text](image-2.png)

### Most Confusions:
- **Digit 2 vs. 8:** (15 misclassifications of 2 as 8)
- **Digit 7 vs. 1:** (22 misclassifications of 7 as 1)
- **Digit 8 vs. 3:** (13 misclassifications of 8 as 3)
- **Digit 9 vs. 4:** (7 misclassifications of 9 as 4)

### Why?
- KNN relies on similarity to neighboring points. If training images are handwritten differently, similar-looking numbers (e.g., **7 and 1**) can cause confusion.
- The **loop shape in 8 and 3** can be hard to distinguish in certain fonts.


### 3. Multi-Layer Perceptron (MLP - Neural Network)
- **Accuracy:** 95.6%
- **Classification Report:**
  - **Precision:** Ranges from 93% to 99%
  - **Recall:** Ranges from 93% to 98%
  - **F1-score:** Averages around 96%
- **Confusion Matrix:** 
![alt text](image-3.png)
### Most Confusions:
- **Digit 3 vs. 5:** (24 misclassifications of 3 as 5)
- **Digit 9 vs. 4:** (25 misclassifications of 9 as 4)
- **Digit 2 vs. 8:** (14 misclassifications of 2 as 8)

### Why?
- The MLP is non-linear, so it performs better than Logistic Regression.
- However, it still confuses **3 and 5** due to their similar stroke patterns.
- **9 and 4** are visually close when written with open loops.


## Visualization on Graph:
![alt text](image.png)

## Conclusion
- KNN achieved the highest accuracy (96.9%), followed by MLP (95.6%) and Logistic Regression (92.5%).
- The confusion matrices suggest that certain digits, such as 3 and 5 or 8 and 9, were more prone to misclassification.
- The results indicate that KNN performed best for this dataset, making it a preferable choice for digit classification under the given conditions.

Future improvements could include hyperparameter tuning, additional preprocessing steps like normalization, and testing more advanced deep learning models such as Convolutional Neural Networks (CNNs) to enhance classification performance further.
