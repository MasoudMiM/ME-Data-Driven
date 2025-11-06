# In-Class Assignment: Classification with KNN and Logistic Regression


## Dataset: Steel Plates Faults

We'll use the Steel Plates Faults dataset from Semeion Research Center. This dataset contains 27 features describing various characteristics of steel plates, and we'll predict whether a plate has a specific type of fault (binary classification).

**Features include:**
- Geometric measurements (X_Minimum, X_Maximum, Y_Minimum, Y_Maximum)
- Area measurements (Pixels_Areas)
- Perimeter measurements (X_Perimeter, Y_Perimeter)
- Luminosity measurements
- Steel type indicators
- And many more...

---

## Part 1: Data Loading and Exploration

### Task 1.1: Import Required Libraries

```python
# Data manipulation
import pandas as pd
import numpy as np

# Machine Learning
from sklearn.linear_model import LogisticRegression
from sklearn.neighbors import KNeighborsClassifier
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

# Evaluation metrics
from sklearn.metrics import accuracy_score, jaccard_score, f1_score, log_loss
from sklearn.metrics import confusion_matrix, ConfusionMatrixDisplay

# Visualization
import matplotlib.pyplot as plt
```

---

### Task 1.2: Load the Dataset

```python
# Load the dataset
url = 'https://raw.githubusercontent.com/MasoudMiM/ME_364/main/Steel_Plates_Faults/Data.csv'
df = pd.read_csv(url, names=['X_Minimum', 'X_Maximum', 'Y_Minimum', 'Y_Maximum', 
                              'Pixels_Areas', 'X_Perimeter', 'Y_Perimeter', 
                              'Sum_of_Luminosity', 'Minimum_of_Luminosity', 
                              'Maximum_of_Luminosity', 'Length_of_Conveyer', 
                              'TypeOfSteel_A300', 'TypeOfSteel_A400', 
                              'Steel_Plate_Thickness', 'Edges_Index', 'Empty_Index', 
                              'Square_Index', 'Outside_X_Index', 'Edges_X_Index', 
                              'Edges_Y_Index', 'Outside_Global_Index', 'LogOfAreas', 
                              'Log_X_Index', 'Log_Y_Index', 'Orientation_Index', 
                              'Luminosity_Index', 'SigmoidOfAreas', 'Pastry', 
                              'Z_Scratch', 'K_Scratch', 'Stains', 'Dirtiness', 
                              'Bumps', 'Other_Faults'])

# Display first few rows
df.head()
```

---

### Task 1.3: Explore the Dataset

**Question 1:** How many samples and features does the dataset have?

```python
# Write code to find the shape of the dataset
# YOUR CODE HERE
```

**Question 2:** Are there any missing values in the dataset?

```python
# Check for missing values
# YOUR CODE HERE
```

**Question 3:** What is the distribution of the target variable (`K_Scratch`)?

```python
# Check unique values and their counts
# YOUR CODE HERE

# Create a bar plot of the distribution
# YOUR CODE HERE
```

---

## Part 2: Data Preparation

### Task 2.1: Define Features and Target Variable

We'll predict whether a steel plate has K_Scratch fault (binary: 0 or 1).

```python
# Select features for our model
X = df[['X_Minimum', 'X_Maximum', 'Y_Minimum', 'Y_Maximum', 
        'Pixels_Areas', 'X_Perimeter', 'Y_Perimeter', 
        'Sum_of_Luminosity', 'Minimum_of_Luminosity', 
        'Maximum_of_Luminosity', 'TypeOfSteel_A300', 
        'TypeOfSteel_A400', 'Steel_Plate_Thickness']].values

# Define target variable
y = # YOUR CODE HERE

print(f"Feature matrix shape: {X.shape}")
print(f"Target vector shape: {y.shape}")
```


---

### Task 2.2: Normalize the Features

**Why normalize?** KNN is distance-based and very sensitive to feature scales. Logistic Regression also benefits from normalization for faster convergence.

```python
# Create MinMaxScaler object
scaler = # YOUR CODE HERE

# Fit and transform the features
X_scaled = # YOUR CODE HERE

# Verify normalization (all values should be between 0 and 1)
print(f"Min value after scaling: {X_scaled.min()}")
print(f"Max value after scaling: {X_scaled.max()}")
```

**Question 4:** Why is it important to normalize features for KNN specifically?


---

### Task 2.3: Split Data into Training and Test Sets

```python
# Split data: 70% training, 30% testing
X_train, X_test, y_train, y_test = # YOUR CODE HERE

print(f"Training set size: {X_train.shape[0]}")
print(f"Test set size: {X_test.shape[0]}")
print(f"Training set class distribution:\n{pd.Series(y_train).value_counts()}")
```

---

## Part 3: K-Nearest Neighbors (KNN) Classifier

### Task 3.1: Build KNN Model

```python
# Create KNN classifier with K=5
knn = # YOUR CODE HERE

# Train the model
# YOUR CODE HERE

# Make predictions on both training and test sets
y_train_pred_knn = knn.predict(X_train)
y_test_pred_knn = knn.predict(X_test)

print("KNN model trained successfully!")
```

---

### Task 3.2: Evaluate KNN Model

```python
# Calculate metrics for training set
acc_train_knn = # YOUR CODE HERE
f1_train_knn = # YOUR CODE HERE

print("KNN Training Set Performance:")
print(f"Accuracy:  {acc_train_knn:.3f}")
print(f"F1-Score:  {f1_train_knn:.3f}")

print("\n" + "="*50 + "\n")

# Calculate metrics for test set
acc_test_knn = # YOUR CODE HERE
f1_test_knn = # YOUR CODE HERE

print("KNN Test Set Performance:")
print(f"Accuracy:  {acc_test_knn:.3f}")
print(f"F1-Score:  {f1_test_knn:.3f}")
```

**Question 5:** Is there a significant difference between training and test performance? What might this indicate?

---

### Task 3.3: Confusion Matrix for KNN

```python
# Create confusion matrix
cm_knn = # YOUR CODE HERE

# Display confusion matrix
disp_knn = # YOUR CODE HERE
disp_knn.plot()
plt.title('KNN Confusion Matrix (Test Set)')
plt.show()

print("Confusion Matrix:")
print(cm_knn)
```

**Question 6:** Based on the confusion matrix, what type of errors is the KNN model making more frequently?

---

### Task 3.4: Experiment with Different K Values

**Optional Challenge:** Try different values of K and see how performance changes.

```python
# Test different K values
k_values = [1, 3, 5, 7, 9, 15, 21]
accuracies = []

for k in k_values:
    knn_temp = KNeighborsClassifier(n_neighbors=k)
    knn_temp.fit(X_train, y_train)
    y_pred_temp = knn_temp.predict(X_test)
    acc = accuracy_score(y_test, y_pred_temp)
    accuracies.append(acc)
    print(f"K={k}: Accuracy = {acc:.3f}")

# Plot results
plt.figure(figsize=(10, 6))
plt.plot(k_values, accuracies, marker='o')
plt.xlabel('K Value')
plt.ylabel('Accuracy')
plt.title('KNN Performance vs. K Value')
plt.grid(True)
plt.show()
```

**Question 7:** What is the optimal K value for this dataset? Why might very small or very large K values perform poorly? Why shouldn't we just use `k=1`?

---

## Part 4: Logistic Regression Classifier

### Task 4.1: Build Logistic Regression Model

```python
# Create Logistic Regression classifier
lr = # YOUR CODE HERE

# Train the model
# YOUR CODE HERE

# Make predictions on both training and test sets
y_train_pred_lr = # YOUR CODE HERE
y_test_pred_lr = # YOUR CODE HERE

# Get probability predictions
y_test_pred_proba_lr = # YOUR CODE HERE

print("Logistic Regression model trained successfully!")
print(f"Classes: {lr.classes_}")
```

---

### Task 4.2: Examine Probability Predictions

```python
# Display first 10 probability predictions
print("Sample probability predictions (first 10):")
print("Format: [P(class=0), P(class=1)]")
for i in range(10):
    actual = y_test.iloc[i]
    predicted = y_test_pred_lr[i]
    proba = y_test_pred_proba_lr[i]
    print(f"Sample {i}: Actual={actual}, Predicted={predicted}, "
          f"Probabilities={proba[0]:.3f}, {proba[1]:.3f}")
```

**Question 8:** How does Logistic Regression make its final classification decision based on these probabilities?

---

### Task 4.3: Evaluate Logistic Regression Model

```python
# Calculate metrics for training set
acc_train_lr = # YOUR CODE HERE
f1_train_lr = # YOUR CODE HERE

print("Logistic Regression Training Set Performance:")
print(f"Accuracy:  {acc_train_lr:.3f}")
print(f"F1-Score:  {f1_train_lr:.3f}")

print("\n" + "="*50 + "\n")

# Calculate metrics for test set
acc_test_lr = # YOUR CODE HERE
f1_test_lr = # YOUR CODE HERE)
log_loss_lr = # YOUR CODE HERE

print("Logistic Regression Test Set Performance:")
print(f"Accuracy:  {acc_test_lr:.3f}")
print(f"F1-Score:  {f1_test_lr:.3f}")
print(f"Log Loss:  {log_loss_lr:.3f}")
```

**Question 9:** How does the Log Loss metric differ from accuracy? Why is it particularly useful for Logistic Regression?

---

### Task 4.4: Confusion Matrix for Logistic Regression

```python
# Create confusion matrix
cm_lr = # YOUR CODE HERE

# Display confusion matrix
disp_lr = # YOUR CODE HERE
disp_lr.plot()
plt.title('Logistic Regression Confusion Matrix (Test Set)')
plt.show()

print("Confusion Matrix:")
print(cm_lr)
```

**Question 10:** Compare this confusion matrix with the KNN confusion matrix. Which model makes fewer errors?

---

## Part 5: Model Comparison and Analysis

### Task 5.1: Side-by-Side Comparison

```python
# Create comparison DataFrame
comparison = pd.DataFrame({
    'Model': ['KNN', 'Logistic Regression'],
    'Accuracy': [acc_test_knn, acc_test_lr],
    'F1-Score': [f1_test_knn, f1_test_lr]
})

print("Model Comparison (Test Set):")
print(comparison.to_string(index=False))

# Visualize comparison
comparison.set_index('Model').plot(kind='bar', figsize=(10, 6))
plt.title('Model Performance Comparison')
plt.ylabel('Score')
plt.xlabel('Model')
plt.legend(loc='lower right')
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()
```

**Question 11:** Based on all metrics, which model performs better on this dataset?

---

**Question 12:** 
- Which model has better precision for detecting faults?
- Which model has better recall for detecting faults?
- In a steel manufacturing context, which is more important: precision or recall? Why?

---

**Question 13:** If you had to deploy one of these models in a real steel manufacturing plant, which would you choose and why?

---

**Question 14:** What additional steps could you take to improve the performance of these models?

---

## Challenges (Optional)

### Challenge 1: Feature Selection
Try training models with different subsets of features. Can you achieve similar performance (or better) with fewer features?

### Challenge 2: Multi-class Classification
We only did binary classification, i.e. our target variable could have only two possible values. Try predicting multiple fault types using a multi-class classification (e.g., combine multiple fault columns). See the guide below. How does model performance change?


#### Guide:
One approach is to define a new column that encodes the pair of two or more defects into one target categorical column with multiple category. Here is an example for combining columns `K_Scratch` and `Bumbs`.
What the combine function is doing

```python
# The function multiplies the K_Scratch value by 2 and then adds the Bumps value.
def combine(row):
    return row['K_Scratch'] * 2 + row['Bumps']
```
Each row of your data has two binary columns:

|column	| possible values |
|----|----|
|K_Scratch | 0 or 1 |
|Bumps	| 0 or 1 |

The function multiplies the `K_Scratch` value by 2 and then adds the `Bumps` value.
Because both inputs are only 0 or 1, the arithmetic can only yield four distinct results:

|K_Scratch|	Bumps |	Calculation	| Result (combined) |	Meaning (human‑readable) |
| ---- | ---- | ---- | ---- | --- |
|0	|0	| 0 × 2 + 0 = 0	| 0	| Neither scratch nor bump |
|0	|1	| 0 × 2 + 1 = 1	| 1	| Only bump present |
|1	|0	| 1 × 2 + 0 = 2	| 2	| Only scratch present |
|1	|1	| 1 × 2 + 1 = 3	| 3	| Both scratch and bump |

So the single integer combined encodes the joint state of the two binary variables.
When you feed this column to a multiclass classifier, the model learns to predict one of four mutually exclusive classes (0, 1, 2, 3). 


```python
# ----- Building the combined label ---------------------------------
def combine(row):
    return row['K_Scratch'] * 2 + row['Bumps']

df['K_Bump_combined'] = df.apply(combine, axis=1)

# ----- Split data ------------------------------------------------
x_dataM = df.drop(columns=['K_Scratch', 'Bumps', 'K_Bump_combined'])
y_dataM = df['K_Bump_combined']

MinMaxscalerM = MinMaxScaler()  # define min max scaler
x_data_scaledM = MinMaxscaler.fit_transform(x_dataM)  # transform data 

X_trainM, X_testM, y_trainM, y_testM = train_test_split(
    x_data_scaledM, y, test_size=0.2, random_state=42, stratify=y
)
```

---

## Submission

Save your completed notebook with all code cells executed and questions answered. Make sure to include:

1. All code cells with outputs
2. Answers to all questions (1-14)
3. All visualizations (confusion matrices, comparison plots)
4. Any bonus challenges attempted

**File name:** `LastName_FirstName_Classification_Assignment.ipynb`

