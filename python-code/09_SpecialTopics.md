# ME 371 - Data-Driven Problem Solving
## In-Class Assignment: Special Topics

## Overview

In this assignment, you will apply advanced machine learning techniques to a **predictive maintenance problem** for industrial rotating machinery. You will work with sensor data from a manufacturing facility to predict equipment failures before they occur.

**Learning Objectives:**
1. Handle imbalanced datasets using resampling techniques
2. Apply cross-validation for robust model evaluation
3. Optimize hyperparameters using Grid Search and Random Search
4. Select important features to improve model performance

**Submission Instructions:**
- Create a Jupyter notebook named: `LastName_FirstName_Assignment.ipynb`
- Include all code, outputs, and answers to questions
- Submit your completed notebook to Canvas by [Due Date]
- Make sure all cells are executed and outputs are visible

---

## Problem Description

You are a data scientist working for a manufacturing company that operates critical rotating equipment (pumps, motors, compressors). Equipment failures cause:
- Production downtime ($10,000/hour)
- Safety risks
- Costly emergency repairs

The maintenance team has installed sensors to monitor:
- Vibration levels (3 axes)
- Temperature (motor, bearing, ambient)
- Pressure readings
- Acoustic emissions
- Rotational speed
- Power consumption
- Operating hours

**Your Goal:** Build a model to predict equipment failures 24 hours in advance, allowing for planned maintenance.

**The Challenge:** Equipment failures are rare (only ~2% of operating hours result in failures within 24 hours), creating a highly imbalanced dataset.

---

## Dataset Description

**Features (20 sensor readings):**
- `vibration_x`, `vibration_y`, `vibration_z`: Vibration amplitude (mm/s)
- `temp_motor`: Motor temperature (°C)
- `temp_bearing_1`, `temp_bearing_2`: Bearing temperatures (°C)
- `temp_ambient`: Ambient temperature (°C)
- `pressure_inlet`, `pressure_outlet`: Pressure readings (bar)
- `acoustic_emission`: Acoustic emission level (dB)
- `rotational_speed`: RPM
- `power_consumption`: kW
- `operating_hours`: Cumulative operating hours
- `load_percentage`: Current load (%)
- `oil_pressure`: Lubrication pressure (bar)
- Plus 5 additional derived features from signal processing

**Target Variable:**
- `failure`: 0 = Normal operation, 1 = Failure within 24 hours

---

## Part 1: Setup and Data Exploration

### Task 1.1: Import Libraries and Load Data

Create a new Jupyter notebook and start with the following code:

```python
# imprting required libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import (confusion_matrix, 
                             ConfusionMatrixDisplay, accuracy_score, 
                             precision_score, recall_score, f1_score)
import warnings
warnings.filterwarnings('ignore')

# random seed for reproducibility
np.random.seed(42)

# plotting style
plt.style.use('seaborn-v0_8-darkgrid')
sns.set_palette("husl")
```

### Task 1.2: Generate Synthetic Dataset

Since we don't have access to real industrial data, we'll create a realistic synthetic dataset:

```python
from sklearn.datasets import make_classification

# synthetic generatino of imbalanced dataset simulating equipment sensor data
X, y = make_classification(
    n_samples=10000,       # 10,000 hours of operation
    n_features=20,         # 20 sensor readings
    n_informative=15,      # 15 truly predictive features
    n_redundant=5,         # 5 correlated features
    n_classes=2,           # Binary: Normal vs. Failure
    weights=[0.98, 0.02],  # 98% normal, 2% pre-failure (highly imbalanced)
    flip_y=0.01,           # 1% label noise (sensor errors)
    random_state=42
)

# feature names (sensor readings)
feature_names = [
    'vibration_x', 'vibration_y', 'vibration_z',
    'temp_motor', 'temp_bearing_1', 'temp_bearing_2', 'temp_ambient',
    'pressure_inlet', 'pressure_outlet',
    'acoustic_emission', 'rotational_speed', 'power_consumption',
    'operating_hours', 'load_percentage', 'oil_pressure',
    'feature_16', 'feature_17', 'feature_18', 'feature_19', 'feature_20'
]

# define DataFrame
df = pd.DataFrame(X, columns=feature_names)
df['failure'] = y

print("="*80)
print("EQUIPMENT FAILURE PREDICTION DATASET")
print("="*80)
print(f"\nDataset shape: {df.shape}")
print(f"Number of samples: {len(df)}")
print(f"Number of features: {len(feature_names)}")
```

### Task 1.3: Explore Class Distribution

```python
print("\nClass Distribution:")
print(df['failure'].value_counts())

print("\nClass Distribution (Percentage):")
print(df['failure'].value_counts(normalize=True) * 100)

# visualization
fig, axes = plt.subplots(1, 2, figsize=(14, 5))

sns.countplot(data=df, x='failure', ax=axes[0])
axes[0].set_title('Class Distribution - Count')
axes[0].set_xlabel('Failure Status')
axes[0].set_ylabel('Count')
axes[0].set_xticklabels(['Normal (0)', 'Failure (1)'])

# adding labels to the count plots on bars
for container in axes[0].containers:
    axes[0].bar_label(container)

# pie chart
failure_counts = df['failure'].value_counts()
axes[1].pie(failure_counts, labels=['Normal', 'Failure'], autopct='%1.1f%%',
            startangle=90, colors=['lightblue', 'coral'])
axes[1].set_title('Class Distribution - Percentage')

plt.tight_layout()
plt.show()
```

**📝 QUESTION 1.1:** What percentage of the data represents equipment failures? Why is this a problem for machine learning models?

**YOUR ANSWER:**
```
[Type your answer here]
```

---

## Part 2: Handling Imbalanced Data

### Creating Train-Test Split

```python
# separating features and target
X = df.drop('failure', axis=1) # features
y = df['failure'] # target variable

# using stratify=y to maintain class distribution
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

print(f"\nTraining set size: {len(X_train)}")
print(f"Test set size: {len(X_test)}")
print(f"\nTraining set class distribution:")
print(pd.Series(y_train).value_counts())
print(f"\nTest set class distribution:")
print(pd.Series(y_test).value_counts())
```

### Task 2.1: Baseline Model (No Resampling)

First, let's see how a model (KNN classifier) performs without handling the imbalance:

```python
from sklearn.neighbors import KNeighborsClassifier

# TODO: scale features using StandardScaler (essential for KNN)
scaler = StandardScaler()
X_train_scaled = # YOUR CODE HERE
X_test_scaled = # YOUR CODE HERE

# training the baseline KNN model
print("\n" + "="*80)
print("BASELINE MODEL - K-Nearest Neighbors (No Resampling)")
print("="*80)

# TODO: defining and training your knn model with k = 5
knn_baseline = # YOUR CODE HERE
knn_baseline.fit(X_train_scaled, y_train)

# making predictions
y_pred_baseline = knn_baseline.predict(X_test_scaled)

# evaluation
print(f"\nAccuracy:  {accuracy_score(y_test, y_pred_baseline):.4f}")
print(f"Precision: {precision_score(y_test, y_pred_baseline):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred_baseline):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred_baseline):.4f}")

# confusion matrix
cm_baseline = confusion_matrix(y_test, y_pred_baseline)
disp = ConfusionMatrixDisplay(cm_baseline, display_labels=['Normal', 'Failure'])
disp.plot(cmap='Blues')
plt.title('Baseline Model - Confusion Matrix')
plt.show()
```

**📝 QUESTION 2.1:** The model achieves high accuracy but low recall. In the context of predictive maintenance, what does this mean? What are the consequences of missing a failure prediction (false negative)?

**YOUR ANSWER:**
```
[Type your answer here]
```

### Task 2.2: Random Undersampling

```python
from imblearn.under_sampling import RandomUnderSampler

print("\n" + "="*80)
print("RANDOM UNDERSAMPLING")
print("="*80)

# TODO: random undersamplng
rus = # YOUR CODE HERE
X_train_rus, y_train_rus = # YOUR CODE HERE

print(f"\nOriginal training set size: {len(X_train_scaled)}")
print(f"After undersampling: {len(X_train_rus)}")
print(f"\nClass distribution after undersampling:")
print(pd.Series(y_train_rus).value_counts())

# TODO: Train KNN with undersampled data - define and train your knn model with k = 5
knn_rus = # YOUR CODE HERE
knn_rus.fit(X_train_rus, y_train_rus)
y_pred_rus = knn_rus.predict(X_test_scaled)

# esvaluate
print(f"\nAccuracy:  {accuracy_score(y_test, y_pred_rus):.4f}")
print(f"Precision: {precision_score(y_test, y_pred_rus):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred_rus):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred_rus):.4f}")
```

### Task 2.3: Random Oversampling

```python
from imblearn.over_sampling import RandomOverSampler

print("\n" + "="*80)
print("RANDOM OVERSAMPLING")
print("="*80)

# TODO: rndom oversampling with sampling_strategy=0.5
ros = # YOUR CODE HERE
X_train_ros, y_train_ros = # YOUR CODE HERE

print(f"\nOriginal training set size: {len(X_train_scaled)}")
print(f"After oversampling: {len(X_train_ros)}")
print(f"\nClass distribution after oversampling:")
print(pd.Series(y_train_ros).value_counts())

# TODO: Train KNN with oversampled data
knn_ros = # YOUR CODE HERE
# YOUR CODE HERE: fitting the model
y_pred_ros = # YOUR CODE HERE: make predictions

# TODO: evaluation and printing the metrics
print(f"\nAccuracy:  {accuracy_score(y_test, y_pred_ros):.4f}")
# YOUR CODE HERE: print precision, recall, F1-score
```

### Task 2.4: SMOTE (Synthetic Minority Over-sampling Technique)

```python
from imblearn.over_sampling import SMOTE

print("\n" + "="*80)
print("SMOTE (SYNTHETIC MINORITY OVER-SAMPLING)")
print("="*80)

# TODO: SMOTE with sampling_strategy=0.5
smote = # YOUR CODE HERE
X_train_smote, y_train_smote = # YOUR CODE HERE

print(f"\nOriginal training set size: {len(X_train_scaled)}")
print(f"After SMOTE: {len(X_train_smote)}")
print(f"\nClass distribution after SMOTE:")
print(pd.Series(y_train_smote).value_counts())

# TODO: Train KNN with SMOTE data
knn_smote = # YOUR CODE HERE
# YOUR CODE HERE: fit and predict

# TODO: Evaluate
# YOUR CODE HERE: print all metrics
```

### Task 2.5: Compare Resampling Techniques

```python
# DataFrame to easily plot the comparison
comparison_df = pd.DataFrame({
    'Method': ['Baseline', 'Undersampling', 'Oversampling', 'SMOTE'],
    'Accuracy': [
        accuracy_score(y_test, y_pred_baseline),
        accuracy_score(y_test, y_pred_rus),
        # TODO: Add oversampling accuracy
        # TODO: Add SMOTE accuracy
    ],
    'Precision': [
        precision_score(y_test, y_pred_baseline),
        # TODO: Complete for all methods
    ],
    'Recall': [
        recall_score(y_test, y_pred_baseline),
        # TODO: Complete for all methods
    ],
    'F1-Score': [
        f1_score(y_test, y_pred_baseline),
        # TODO: Complete for all methods
    ]
})

print("\n" + "="*80)
print("COMPARISON OF RESAMPLING TECHNIQUES")
print("="*80)
print(comparison_df.to_string(index=False))

# comparing
comparison_df.set_index('Method')[['Precision', 'Recall', 'F1-Score']].plot(
    kind='bar', figsize=(12, 6)
)
plt.title('Comparison of Resampling Techniques for Equipment Failure Prediction')
plt.ylabel('Score')
plt.xlabel('Method')
plt.xticks(rotation=45, ha='right')
plt.legend(loc='lower right')
plt.ylim([0, 1])
plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.show()
```

**📝 QUESTION 2.2:** 

a) Which resampling technique achieved the best balance between precision and recall?

b) For predictive maintenance, is it more important to maximize recall or precision? Why?

c) What is the trade-off when using undersampling?

**YOUR ANSWER:**
```
a) [Type your answer here]
b) [Type your answer here]
c) [Type your answer here]
```

---

## Part 3: Cross-Validation

### Task 3.1: K-Fold Cross-Validation

We'll use the SMOTE-resampled data for cross-validation for a Logistic Regression model.

```python
from sklearn.model_selection import cross_val_score, KFold
from sklearn.linear_model import LogisticRegression

print("\n" + "="*80)
print("K-FOLD CROSS-VALIDATION")
print("="*80)

# logistic regression model object definition
lr = LogisticRegression(max_iter=1000, random_state=42)

# TODO: 5-Fold Cross-Validation implementation
kfold = KFold(n_splits=5, shuffle=True, random_state=42)
scores_kfold = cross_val_score(
    # YOUR CODE HERE: pass lr, X_train_smote, y_train_smote, cv, and scoring='f1'
)

print("\n5-Fold Cross-Validation Results:")
print(f"F1 Scores for each fold: {scores_kfold}")
print(f"Mean F1 Score: {scores_kfold.mean():.4f}")
print(f"Std F1 Score:  {scores_kfold.std():.4f}")

# Visualize fold results
plt.figure(figsize=(10, 5))
plt.bar(range(1, 6), scores_kfold)
plt.axhline(y=scores_kfold.mean(), color='r', linestyle='--', 
           label=f'Mean: {scores_kfold.mean():.4f}')
plt.xlabel('Fold Number')
plt.ylabel('F1 Score')
plt.title('K-Fold Cross-Validation Results')
plt.legend()
plt.ylim([0, 1])
plt.grid(axis='y', alpha=0.3)
plt.show()
```

### Task 3.2: Stratified K-Fold Cross-Validation

```python
from sklearn.model_selection import StratifiedKFold

print("\n" + "="*80)
print("STRATIFIED K-FOLD CROSS-VALIDATION")
print("="*80)

# TODO: Create StratifiedKFold object with 5 splits
skfold = # YOUR CODE HERE

# TODO: Apply Stratified K-Fold CV
scores_skfold = # YOUR CODE HERE

print("\nStratified 5-Fold Cross-Validation Results:")
print(f"F1 Scores for each fold: {scores_skfold}")
print(f"Mean F1 Score: {scores_skfold.mean():.4f}")
print(f"Std F1 Score:  {scores_skfold.std():.4f}")

# Compare K-Fold vs Stratified K-Fold
comparison = pd.DataFrame({
    'Method': ['K-Fold', 'Stratified K-Fold'],
    'Mean F1': [scores_kfold.mean(), scores_skfold.mean()],
    'Std F1': [scores_kfold.std(), scores_skfold.std()]
})
print("\nComparison:")
print(comparison.to_string(index=False))
```

### Task 3.3: Multiple Metrics Evaluation

```python
from sklearn.model_selection import cross_validate

print("\n" + "="*80)
print("CROSS-VALIDATION WITH MULTIPLE METRICS")
print("="*80)

# defining scoring metrics
scoring = ['accuracy', 'precision', 'recall', 'f1']

# TODO: use cross_validate with StratifiedKFold
results = cross_validate(
    # YOUR CODE HERE: pass estimator, X, y, cv, scoring, and return_train_score=True
)

# results
print("\nCross-Validation Results (Mean ± Std):")
for metric in scoring:
    train_scores = results[f'train_{metric}']
    test_scores = results[f'test_{metric}']
    print(f"{metric.capitalize():12s} - Train: {train_scores.mean():.4f} (±{train_scores.std():.4f})  "
          f"Test: {test_scores.mean():.4f} (±{test_scores.std():.4f})")
```

**📝 QUESTION 3.1:** 

a) Why do we observe a difference between training and test scores?

b) What does it mean if the training score is much higher than the test score?

c) Why is Stratified K-Fold particularly important for our equipment failure dataset?

**YOUR ANSWER:**
```
a) [Type your answer here]
b) [Type your answer here]
c) [Type your answer here]
```

---

## Part 4: Hyperparameter Tuning

### Task 4.1: Grid Search for KNN

```python
from sklearn.model_selection import GridSearchCV

print("\n" + "="*80)
print("GRID SEARCH - K-NEAREST NEIGHBORS")
print("="*80)

# Defining the parameter grid
param_grid_knn = {
    'n_neighbors': [3, 5, 7, 9, 11, 13],
    'weights': ['uniform', 'distance'],
    'metric': ['euclidean', 'manhattan', 'minkowski']
}

print(f"\nParameter grid:")
for param, values in param_grid_knn.items():
    print(f"  {param}: {values}")
print(f"\nTotal combinations to try: {6 * 2 * 3} = 36")
print(f"With 5-fold CV: {36 * 5} = 180 model fits\n")

# creating KNN classifier
knn = KNeighborsClassifier()

# TODO: create GridSearchCV object with stratified k-fold scross validation k=5
grid_search_knn = # YOUR CODE HERE

# TODO: fit grid search (this may take a minute)
print("Starting grid search...")
# YOUR CODE HERE

# displaying the results
print(f"\n{'='*80}")
print("GRID SEARCH RESULTS")
print(f"{'='*80}")
print(f"Best parameters: {grid_search_knn.best_params_}")
print(f"Best cross-validation F1 score: {grid_search_knn.best_score_:.4f}")

# evaluating on test set
best_knn = grid_search_knn.best_estimator_
y_pred_knn_tuned = best_knn.predict(X_test_scaled)

print(f"\nPerformance on Test Set:")
print(f"Accuracy:  {accuracy_score(y_test, y_pred_knn_tuned):.4f}")
print(f"Precision: {precision_score(y_test, y_pred_knn_tuned):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred_knn_tuned):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred_knn_tuned):.4f}")
```

### Task 4.2: Grid Search for Logistic Regression

```python
print("\n" + "="*80)
print("GRID SEARCH - LOGISTIC REGRESSION")
print("="*80)

# TODO: efine parameter grid for Logistic Regression
param_grid_lr = {
    'C': [0.001, 0.01, 0.1, 1, 10, 100],
    'penalty': ['l1', 'l2'],
    'solver': ['liblinear']  # liblinear supports both L1 and L2
}

# TODO: GridSearchCV for Logistic Regression
grid_search_lr = # YOUR CODE HERE

# TODO: executing the grid search
print("Starting grid search...")
# YOUR CODE HERE

# TODO: results
print(f"\n{'='*80}")
print("GRID SEARCH RESULTS")
print(f"{'='*80}")
# YOUR CODE HERE: print best parameters and score

# TODO: Evaluate on test set
# YOUR CODE HERE
```

### Task 4.3: Random Search for Neural Network

```python
from sklearn.model_selection import RandomizedSearchCV
from scipy.stats import randint, uniform
import tensorflow as tf
from tensorflow import keras
from scikeras.wrappers import KerasClassifier

print("\n" + "="*80)
print("RANDOM SEARCH - NEURAL NETWORK")
print("="*80)

# function to create neural network
def create_nn(units_layer1=32, units_layer2=16, learning_rate=0.001, dropout_rate=0.2):
    """
    Create a neural network for binary classification.
    
    Parameters:
    - units_layer1: Number of neurons in first hidden layer
    - units_layer2: Number of neurons in second hidden layer
    - learning_rate: Learning rate for optimizer
    - dropout_rate: Dropout rate for regularization
    """
    model = keras.Sequential([
        keras.layers.Input(shape=(X_train_smote.shape[1],)),
        keras.layers.Dense(units_layer1, activation='relu'),
        keras.layers.Dropout(dropout_rate),
        keras.layers.Dense(units_layer2, activation='relu'),
        keras.layers.Dropout(dropout_rate),
        keras.layers.Dense(1, activation='sigmoid')
    ])
    
    optimizer = keras.optimizers.Adam(learning_rate=learning_rate)
    model.compile(
        optimizer=optimizer,
        loss='binary_crossentropy',
        metrics=['accuracy']
    )
    return model

# KerasClassifier wrapper
nn_classifier = KerasClassifier(
    model=create_nn,
    epochs=20,
    batch_size=32,
    verbose=0,
    random_state=42
)

# parameter distributions (grid for searching)
param_dist_nn = {
    'model__units_layer1': randint(16, 64),
    'model__units_layer2': randint(8, 32),
    'model__learning_rate': uniform(0.0001, 0.01),
    'batch_size': [16, 32, 64]
}

print(f"\nParameter distributions:")
for param, dist in param_dist_nn.items():
    print(f"  {param}: {dist}")

# RandomizedSearchCV
random_search_nn = RandomizedSearchCV(
    estimator=nn_classifier,
    param_distributions=param_dist_nn,
    n_iter=10,  # Try 10 random combinations
    cv=3,  # Use 3-fold CV (faster for neural networks)
    scoring='f1',
    random_state=42,
    verbose=2,
    n_jobs=1  # Neural networks don't parallelize well with n_jobs
)

# TODO: fitting random search (this will take several minutes)
print("\nStarting random search (this may take 5-10 minutes)...")
# YOUR CODE HERE

print(f"\n{'='*80}")
print("RANDOM SEARCH RESULTS")
print(f"{'='*80}")
print(f"Best parameters: {random_search_nn.best_params_}")
print(f"Best cross-validation F1 score: {random_search_nn.best_score_:.4f}")

# evaluating on test set
best_nn = random_search_nn.best_estimator_
y_pred_nn_tuned = best_nn.predict(X_test_scaled)

print(f"\nPerformance on Test Set:")
print(f"Accuracy:  {accuracy_score(y_test, y_pred_nn_tuned):.4f}")
print(f"Precision: {precision_score(y_test, y_pred_nn_tuned):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred_nn_tuned):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred_nn_tuned):.4f}")
```

### Task 4.4: Compare All Tuned Models

```python
print("\n" + "="*80)
print("COMPARISON OF TUNED MODELS")
print("="*80)

# comparison DataFrame for evaluation metrics
tuned_comparison = pd.DataFrame({
    'Model': ['KNN (Tuned)', 'Logistic Regression (Tuned)', 'Neural Network (Tuned)'],
    'Accuracy': [
        accuracy_score(y_test, y_pred_knn_tuned),
        # TODO: Add LR accuracy
        accuracy_score(y_test, y_pred_nn_tuned)
    ],
    'Precision': [
        precision_score(y_test, y_pred_knn_tuned),
        # TODO: Add LR precision
        precision_score(y_test, y_pred_nn_tuned)
    ],
    'Recall': [
        recall_score(y_test, y_pred_knn_tuned),
        # TODO: Add LR recall
        recall_score(y_test, y_pred_nn_tuned)
    ],
    'F1-Score': [
        f1_score(y_test, y_pred_knn_tuned),
        # TODO: Add LR F1
        f1_score(y_test, y_pred_nn_tuned)
    ]
})

print(tuned_comparison.to_string(index=False))

# Visualize comparison
tuned_comparison.set_index('Model')[['Precision', 'Recall', 'F1-Score']].plot(
    kind='bar', figsize=(12, 6)
)
plt.title('Comparison of Tuned Models')
plt.ylabel('Score')
plt.xlabel('Model')
plt.xticks(rotation=45, ha='right')
plt.legend(loc='lower right')
plt.ylim([0, 1])
plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.show()
```

**📝 QUESTION 4.1:** 

a) Which model performed best after hyperparameter tuning?

b) Why would you prefer Random Search over Grid Search for neural networks?

c) If computation time is limited, which search method would you use and why?

**YOUR ANSWER:**
```
a) [Type your answer here]
b) [Type your answer here]
c) [Type your answer here]
```

---

## Part 5: Feature Selection

### Task 5.1: Recursive Feature Elimination (RFE)

```python
from sklearn.feature_selection import RFE

print("\n" + "="*80)
print("RECURSIVE FEATURE ELIMINATION (RFE)")
print("="*80)

# Logistic Regression as the estimator
lr_rfe = LogisticRegression(max_iter=1000, random_state=42)

# TODO: Create RFE object to select 10 features
rfe = RFE(
    # YOUR CODE HERE
)

# TODO: Fit RFE
print("\nFitting RFE...")
# YOUR CODE HERE

# Get selected features
selected_features_rfe = X.columns[rfe.support_]
print(f"\nSelected features ({len(selected_features_rfe)}):")
for i, feature in enumerate(selected_features_rfe, 1):
    print(f"  {i}. {feature}")

# feature rankings
feature_ranking = pd.DataFrame({
    'Feature': X.columns,
    'Selected': rfe.support_,
    'Ranking': rfe.ranking_
}).sort_values('Ranking')

print("\nAll features with rankings:")
print(feature_ranking.to_string(index=False))

# transforming data
X_train_rfe = rfe.transform(X_train_smote)
X_test_rfe = rfe.transform(X_test_scaled)

# training model with selected features
lr_with_rfe = LogisticRegression(max_iter=1000, random_state=42)
lr_with_rfe.fit(X_train_rfe, y_train_smote)
y_pred_rfe = lr_with_rfe.predict(X_test_rfe)

print("\n--- Logistic Regression with RFE Selected Features ---")
print(f"Accuracy:  {accuracy_score(y_test, y_pred_rfe):.4f}")
print(f"Precision: {precision_score(y_test, y_pred_rfe):.4f}")
print(f"Recall:    {recall_score(y_test, y_pred_rfe):.4f}")
print(f"F1-Score:  {f1_score(y_test, y_pred_rfe):.4f}")
```

### Task 5.2: RFECV (RFE with Cross-Validation)

```python
from sklearn.feature_selection import RFECV

print("\n" + "="*80)
print("RFECV (RFE WITH CROSS-VALIDATION)")
print("="*80)

# creating RFECV object with stratified KFold
rfecv = RFECV(
    estimator=LogisticRegression(max_iter=1000, random_state=42),
    step=1,
    cv=StratifiedKFold(5, shuffle=True, random_state=42),
    scoring='f1',
    n_jobs=-1,
    verbose=1
)

# TODO: fitting RFECV
print("\nFitting RFECV (this may take a minute)...")
# YOUR CODE HERE

print(f"\nOptimal number of features: {rfecv.n_features_}")
print(f"\nSelected features:")
selected_features_rfecv = X.columns[rfecv.support_]
for i, feature in enumerate(selected_features_rfecv, 1):
    print(f"  {i}. {feature}")

# plotting number of features vs. CV score
plt.figure(figsize=(12, 6))
n_features_range = range(1, len(rfecv.cv_results_['mean_test_score']) + 1)
plt.plot(n_features_range, rfecv.cv_results_['mean_test_score'], 
         'b-', linewidth=2, label='Mean CV Score')
plt.fill_between(n_features_range,
                 rfecv.cv_results_['mean_test_score'] - rfecv.cv_results_['std_test_score'],
                 rfecv.cv_results_['mean_test_score'] + rfecv.cv_results_['std_test_score'],
                 alpha=0.2)
plt.axvline(x=rfecv.n_features_, color='r', linestyle='--', 
           label=f'Optimal: {rfecv.n_features_} features')
plt.xlabel('Number of Features')
plt.ylabel('Cross-validation F1 Score')
plt.title('RFECV: Finding Optimal Number of Features')
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.show()

# TODO: Transform data and evaluate
X_train_rfecv = # YOUR CODE HERE
X_test_rfecv = # YOUR CODE HERE

# TODO: Train and evaluate model
lr_with_rfecv = # YOUR CODE HERE
# YOUR CODE HERE: fit, predict, and print metrics
```

### Task 5.3: Compare Feature Selection Methods

```python
print("\n" + "="*80)
print("FEATURE SELECTION COMPARISON")
print("="*80)

# training with all features for comparison
lr_all = LogisticRegression(max_iter=1000, random_state=42)
lr_all.fit(X_train_smote, y_train_smote)
y_pred_all = lr_all.predict(X_test_scaled)

# creating comparison DataFrame
feature_comparison = pd.DataFrame({
    'Method': ['All Features', 'RFE (10 features)', 'RFECV'],
    'Num Features': [X.shape[1], 10, rfecv.n_features_],
    'Accuracy': [
        accuracy_score(y_test, y_pred_all),
        accuracy_score(y_test, y_pred_rfe),
        # TODO: Add RFECV accuracy
    ],
    'Precision': [
        precision_score(y_test, y_pred_all),
        precision_score(y_test, y_pred_rfe),
        # TODO: Add RFECV precision
    ],
    'Recall': [
        recall_score(y_test, y_pred_all),
        recall_score(y_test, y_pred_rfe),
        # TODO: Add RFECV recall
    ],
    'F1-Score': [
        f1_score(y_test, y_pred_all),
        f1_score(y_test, y_pred_rfe),
        # TODO: Add RFECV F1
    ]
})

print(feature_comparison.to_string(index=False))

# Visualizing comparison
fig, axes = plt.subplots(1, 2, figsize=(15, 5))

# Performance comparison execution
feature_comparison.set_index('Method')[['Precision', 'Recall', 'F1-Score']].plot(
    kind='bar', ax=axes[0]
)
axes[0].set_title('Feature Selection Methods: Performance Comparison')
axes[0].set_ylabel('Score')
axes[0].set_xlabel('Method')
axes[0].set_ylim([0, 1])
axes[0].legend(loc='lower right')
axes[0].grid(axis='y', alpha=0.3)

# # of features vs F1-Score
axes[1].scatter(feature_comparison['Num Features'], 
               feature_comparison['F1-Score'], s=200, alpha=0.6)
for i, method in enumerate(feature_comparison['Method']):
    axes[1].annotate(method, 
                    (feature_comparison['Num Features'][i], 
                     feature_comparison['F1-Score'][i]),
                    xytext=(5, 5), textcoords='offset points')
axes[1].set_xlabel('Number of Features')
axes[1].set_ylabel('F1-Score')
axes[1].set_title('Feature Count vs Performance')
axes[1].grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```

**📝 QUESTION 5.1:** 

a) How many features did RFECV automatically select?

b) Does reducing the number of features improve or hurt performance?

c) What are the benefits of using fewer features besides potential performance gains?

d) Based on the selected features, what sensor readings seem most important for predicting equipment failures?

**YOUR ANSWER:**
```
a) [Type your answer here]
b) [Type your answer here]
c) [Type your answer here]
d) [Type your answer here]
```

---

## Part 6: Comprehensive End-to-End Pipeline (Optional)

### Task 6.1: Build Complete Pipeline

Now let's combine everything into one optimized workflow:

```python
print("\n" + "="*80)
print("COMPREHENSIVE END-TO-END PIPELINE")
print("="*80)

from sklearn.model_selection import train_test_split, StratifiedKFold, GridSearchCV
from sklearn.preprocessing import StandardScaler
from sklearn.feature_selection import RFECV
from imblearn.over_sampling import SMOTE
from sklearn.linear_model import LogisticRegression

# Step 1: initial splitting
print("\nStep 1: Initial train-test split...")
X_pipeline = df.drop('failure', axis=1)
y_pipeline = df['failure']
X_train_p, X_test_p, y_train_p, y_test_p = train_test_split(
    X_pipeline, y_pipeline, test_size=0.2, stratify=y_pipeline, random_state=42
)

# Step 2: scaling
print("Step 2: Scaling features...")
scaler_p = StandardScaler()
X_train_scaled_p = scaler_p.fit_transform(X_train_p)
X_test_scaled_p = scaler_p.transform(X_test_p)

# Step 3: dealing with imbalance with SMOTE
print("Step 3: Applying SMOTE...")
smote_p = SMOTE(sampling_strategy=0.5, random_state=42)
X_train_balanced_p, y_train_balanced_p = smote_p.fit_resample(X_train_scaled_p, y_train_p)

# Step 4: feature selection with RFECV
print("Step 4: Selecting features with RFECV...")
rfecv_p = RFECV(
    estimator=LogisticRegression(max_iter=1000, random_state=42),
    step=1,
    cv=StratifiedKFold(3, shuffle=True, random_state=42),  # Use 3-fold for speed
    scoring='f1',
    n_jobs=-1
)
X_train_selected_p = rfecv_p.fit_transform(X_train_balanced_p, y_train_balanced_p)
X_test_selected_p = rfecv_p.transform(X_test_scaled_p)

print(f"   Selected {rfecv_p.n_features_} features")

# Step 5: hyper-parameter tuning using Grid Search
print("Step 5: Tuning hyperparameters with Grid Search...")
param_grid_final = {
    'C': [0.01, 0.1, 1, 10],
    'penalty': ['l1', 'l2'],
    'solver': ['liblinear']
}

grid_final = GridSearchCV(
    LogisticRegression(max_iter=1000, random_state=42),
    param_grid_final,
    cv=StratifiedKFold(5, shuffle=True, random_state=42),
    scoring='f1',
    n_jobs=-1,
    verbose=0
)

grid_final.fit(X_train_selected_p, y_train_balanced_p)

print(f"   Best parameters: {grid_final.best_params_}")
print(f"   Best CV F1 score: {grid_final.best_score_:.4f}")

# Step 6: final evaluation procedure
print("\nStep 6: Final evaluation on test set...")
final_model = grid_final.best_estimator_
y_pred_final = final_model.predict(X_test_selected_p)

print("\n" + "="*80)
print("FINAL MODEL PERFORMANCE")
print("="*80)
print(f"\nAccuracy:  {accuracy_score(y_test_p, y_pred_final):.4f}")
print(f"Precision: {precision_score(y_test_p, y_pred_final):.4f}")
print(f"Recall:    {recall_score(y_test_p, y_pred_final):.4f}")
print(f"F1-Score:  {f1_score(y_test_p, y_pred_final):.4f}")

# Confusion Matrix
cm_final = confusion_matrix(y_test_p, y_pred_final)
disp = ConfusionMatrixDisplay(cm_final, display_labels=['Normal', 'Failure'])
disp.plot(cmap='Blues')
plt.title('Final Model - Confusion Matrix')
plt.show()

# summary of pipeline
print("\n" + "="*80)
print("PIPELINE SUMMARY")
print("="*80)
print(f"1. Original features: {X_pipeline.shape[1]}")
print(f"2. Selected features: {rfecv_p.n_features_}")
print(f"3. Resampling: SMOTE (sampling_strategy=0.5)")
print(f"4. Best model: Logistic Regression")
print(f"5. Best hyperparameters: {grid_final.best_params_}")
print(f"6. Test F1-Score: {f1_score(y_test_p, y_pred_final):.4f}")
```

### Task 6.2: Compare with Baseline

```python
# Train baseline model for comparison (no preprocessing)
print("\n" + "="*80)
print("BASELINE VS OPTIMIZED PIPELINE COMPARISON")
print("="*80)

baseline_simple = LogisticRegression(max_iter=1000, random_state=42)
baseline_simple.fit(X_train_scaled_p, y_train_p)
y_pred_baseline_simple = baseline_simple.predict(X_test_scaled_p)

# Create comparison
pipeline_comparison = pd.DataFrame({
    'Model': ['Baseline (No preprocessing)', 'Optimized Pipeline'],
    'Accuracy': [
        accuracy_score(y_test_p, y_pred_baseline_simple),
        accuracy_score(y_test_p, y_pred_final)
    ],
    'Precision': [
        precision_score(y_test_p, y_pred_baseline_simple),
        precision_score(y_test_p, y_pred_final)
    ],
    'Recall': [
        recall_score(y_test_p, y_pred_baseline_simple),
        recall_score(y_test_p, y_pred_final)
    ],
    'F1-Score': [
        f1_score(y_test_p, y_pred_baseline_simple),
        f1_score(y_test_p, y_pred_final)
    ]
})

print(pipeline_comparison.to_string(index=False))

# Visualize
pipeline_comparison.set_index('Model')[['Precision', 'Recall', 'F1-Score']].plot(
    kind='bar', figsize=(10, 6)
)
plt.title('Baseline vs Optimized Pipeline')
plt.ylabel('Score')
plt.xticks(rotation=0)
plt.ylim([0, 1])
plt.legend(loc='lower right')
plt.grid(axis='y', alpha=0.3)
plt.tight_layout()
plt.show()
```

**📝 QUESTION 6.1:** 

a) How much did the optimized pipeline improve performance compared to the baseline?

b) Which step in the pipeline do you think contributed most to the improvement?

c) In a real predictive maintenance system, what would be the business value of improving recall from the baseline to the optimized model?

d) Are there any trade-offs in the optimized pipeline that might be problematic in production?

**YOUR ANSWER:**
```
a) [Type your answer here]
b) [Type your answer here]
c) [Type your answer here]
d) [Type your answer here]
```

