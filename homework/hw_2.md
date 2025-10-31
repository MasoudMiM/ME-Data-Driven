# Homework II - Regression Analysis

---

## **Question I - Simple Linear Regression**

A series of measurements have been done on a vibrating system, which can be simplified as a single degree-of-freedom system. The stiffness of the system was changed and the time period of the system was measured. The data is recorded in a dataset attached to this assignment with the name [Q1.csv](./Q1.csv). This dataset includes stiffness values and the corresponding time period for the oscillation. Use **simple linear regression** to estimate the system's mass.

**NOTES:**
- For a system with single degree-of-freedom, the natural frequency $\omega_n$ is defined as $\omega_n=\sqrt{\frac{k}{m}}$, where $k$ is the stiffness and $m$ is system's mass.
- The time period of a system and its natural frequency are related by: $\omega_n=\frac{2\pi}{T}$, where $T$ is the time period.
- Based on the these equations, you can find a linear relationship between time period and stiffness. Use that to develop your model.

**Deliverables:**
- Report the coefficients (intercept and slope) of your linear regression model
- Report the estimated mass of the system
- Calculate and report MSE and R² score
- Create a scatter plot of the data with the fitted regression line overlaid

```python
# Your code goes here
```

---

## **Question II - Multiple Linear Regression**

We are trying to model a system with two degrees of freedom based on measurement data. We have the magnitude of input force and the corresponding maximum displacements of mass 1 and mass 2 for given input forces. The data is stored in the csv file [Q2.csv](./Q2.csv).

**Tasks:**
1. Use **Multiple Linear Regression** to develop a model to predict the magnitude of the input force if we know the displacements of mass 1 and mass 2
2. Split your data into 80% training and 20% testing
3. Use evaluation metrics (MAE, MSE, RMSE, R²) to assess the performance of your model
4. Run your model multiple times with different random states. Do you see anything unusual about these metrics? Comment on the consistency of your results.

**Deliverables:**
- Report all four evaluation metrics (MAE, MSE, RMSE, R²)
- Report the coefficients of your model ($W_0$, $W_1$, $W_2$)
- What is the predicted force magnitude when mass 1 and mass 2 displacements are both 0.12 m?
- Comment on whether this is a good model and why it is or it is not a good model? If it is not a good model, what can be done to improve the model's performance?

```python
# Your code goes here
```

---

## **Question III - Power Plant Energy Output Prediction**

For this question, we will be using a dataset that contains data collected from a Combined Cycle Power Plant over 5 years, when the power plant was set to work with full load. The dataset is provided as an excel file named [CCPP_data.xlsx](./CCPP_data.xlsx). We will use the data in `Sheet 1` only. Features consist of hourly average ambient variables:

- **AT**: Ambient Temperature (1.81°C to 37.11°C)
- **AP**: Ambient Pressure (992.89-1033.30 milibar)
- **RH**: Relative Humidity (25.56% to 100.16%)
- **V**: Exhaust Vacuum (25.36-81.56 cm Hg)
- **PE**: Net hourly electrical energy output (420.26-495.76 MW) - **Target Variable**

### **Part (a) - Multiple Linear Regression**

1. First, provide a pairwise plot to observe the relationships between all the variables
2. Develop a **multiple linear regression** model that can predict electrical energy output (PE)
3. Use all four features (AT, AP, RH, V) provided in the dataset
4. Take 20% of the data for testing

**Deliverables:**
- Pairwise plot showing relationships between variables
- Which feature appears to have the strongest relationship with PE based on the pairwise plot?
- Report MSE and R² score for both training and test sets
- Report the coefficients for each feature


```python
# Your code goes here
```

### **Part (b) - Univariate Polynomial Regression**

Select **one feature** that you think has the strongest relationship with PE (based on your pairwise plot from part a). Develop **univariate polynomial regression** models with degrees 1, 2, 3, 4, and 5 to predict PE using only this single feature.

**Deliverables:**
- Create a table comparing the five models with the following columns:
  - Polynomial Degree
  - Training MSE
  - Test MSE
  - R² Score (test)
- Create a visualization showing:
  - The original data points
  - All five fitted polynomial curves on the same plot
- Which polynomial degree gives the best performance? Which one would you choose as the final model? Justify your answers.
- Do you observe any signs of underfitting or overfitting? At which degree(s)?

```python
# Your code goes here
```

### **Part (c) - Multivariate Polynomial Regression**

Now use **all four features** (AT, AP, RH, V) to develop **multivariate polynomial regression** models with degrees 1, 2, and 3.

**Deliverables:**
- Create a comparison table with the following:
  - Polynomial Degree
  - Number of features created (use `poly.n_output_features_` or count from `get_feature_names_out()`)
  - Training MSE
  - Test MSE
  - R² Score (test)
- Compare the performance of the three models
- How does the degree 1 multivariate model compare to the degree 1 univariate model from part (b)?
- Do you see signs of overfitting?

```python
# Your code goes here
```

---

## **Question IV - Understanding the Fitting Problem**

Using the same CCPP dataset from Question III, we will explore model capacity and the bias-variance tradeoff.

### **Part (a) - Exploring Model Capacity**

Using the same single feature you selected in Question III(b), create polynomial regression models for degrees 1 through 10.

**Deliverables:**
1. Create a plot with polynomial degree on the x-axis and error on the y-axis, showing:
   - Training MSE (one line)
   - Test MSE (another line)
   - Use different colors and a legend to distinguish the two lines

2. Answer the following questions:
   - At what degree does the model start to overfit? How can you tell?
   - What happens to the training error as degree increases?
   - What happens to the test error as degree increases?
   - What is the optimal polynomial degree for this problem?

```python
# Your code goes here
```

### **Part (b) - Visualizing Underfitting and Overfitting**

Create separate visualizations for polynomial degrees 2-10 (using the same single feature):

- For each degree, create a scatter plot showing:
   - Training data points
   - Test data points (in a different color)
   - The fitted polynomial curve


**Deliverables:**
- Three separate plots as described above. You need to put them all in one plot as subplots and as a 3x3 grid (three row three columns). See the code from the lecture notes to learn how to do it.
- Brief commentary explaining what you observe in these plots and how each could represent under-fitting, over-fitting, or optimal fit.

```python
# Your code goes here
```

---

## **Question V - Model Selection and Interpretation**

Based on all your work in Questions III and IV, which model would you recommend for predicting power plant energy output in production? Provide a detailed justification (4-5 sentences) for your choice. Consider:
   - Linear regression (Q3a)
   - Best univariate polynomial (Q3b)
   - Best multivariate polynomial (Q3c)

```python
# Your code goes here (if any calculations needed)
```

---

## **Submission Guidelines**

Submit a single Jupyter notebook (.ipynb file) named `FirstName_LastName_HW_2.ipynb` that includes:
- All code for each question
- All requested plots and visualizations
- All numerical results clearly labeled
- Written responses to interpretation questions
- Comments in your code explaining key steps

**Note:** Make sure your code is clear and well-written and your plots have proper titles, axis labels, and legends.