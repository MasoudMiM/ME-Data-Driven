# Data-Driven Problem Solving for Mechanical Engineers

## Textbooks:

- Theory:

    - **Primary:** Brunton, S. L., & Kutz, J. N. (2022). "[Data-driven science and engineering: Machine learning, dynamical systems, and control](https://www.amazon.com/Data-Driven-Science-Engineering-Learning-Dynamical/dp/1009098489)". Cambridge University Press.
        > book website: https://www.databookuw.com
    - **Supplementary (for RL):** Prince, S. J. (2023). "[Understanding deep learning](https://www.amazon.com/Understanding-Deep-Learning-Simon-Prince/dp/0262048647)". MIT press.
        > book website: https://udlbook.github.io/udlbook

- Programming:
    - Géron, A. (2022). "[Hands-on machine learning with Scikit-Learn, Keras, and TensorFlow: Concepts, tools, and techniques to build intelligent systems.](https://www.amazon.com/Hands-Machine-Learning-Scikit-Learn-TensorFlow/dp/1492032646)" O'Reilly Media, Inc.

## Assessment Structure:
- **Midterm Exam:** 25%
- **Final Exam:** 25%
- **Final Project:** 15%
- **Weekly Assignments:** 20%
- **Class Participation & Assignments:** 15%

## Course Agenda

We will be loosely following this agenda and covering these topics:

### 1. Course Introduction & Data-Driven Engineering
- **Theory:**  Course overview, data-driven methodology in engineering

- **Hands-on Lab:**
    - General Python overview
    - NumPy for calculations, array operations
    - Loading and visualizing datasets (sensors, experiments)
    - Basic statistical analysis of system data

### 2. Singular Value Decomposition
- **Theory:** SVD overview, mathematical foundation, low-rank approximation, data compression  

- **Hands-on Lab:**
    - Implementing SVD with NumPy
    - Matrix decomposition of experimental data
    - Image compression 
    - Noise reduction in sensor measurements

### 3. Dynamic Mode Decomposition (DMD)
- **Theory:** DMD fundamentals, relationship to SVD, applications to time-series data  

    **Hands-on Lab:**
    - DMD implementation for vibration analysis
    - Extracting dynamic modes from experimental data
    - Time series analysis of systems
    - _Modal identification and frequency analysis_

### 4. Pseudo-inverse and Least Squares
- **Theory:** Pseudo-inverse, least squares method, linear regression

- **Hands-on Lab:**
    - Curve fitting for experimental data
    - Parameter estimation in systems
    - _Solving over-determined systems from multiple sensors_

### 5. Principal Component Analysis & Data Alignment
- **Theory:** PCA theory, dimensionality reduction, SVD truncation, data alignment techniques  

- **Hands-on Lab:**
    - PCA on multi-sensor vibration data
    - Feature extraction from high-dimensional measurements
    - Synchronizing multi-channel data acquisition
    - _Optimal rank selection for engineering applications_

### 6. Classic Curve Fitting and Regression
- **Theory:** Polynomial fitting, basis functions, regression fundamentals 

- **Hands-on Lab:**
    - Fitting material property curves (stress-strain, fatigue)
    - Scipy.optimize for nonlinear curve fitting
    - Residual analysis and goodness of fit

### 7. Nonlinear Regression and Optimization
- **Theory:** Gradient descent, nonlinear regression, optimization

- **Hands-on Lab:**
    - Parameter identification in dynamic systems
    - Optimization of engineering design parameters
    - Gradient descent 

### Midterm Exam
- **Exam:** Written exam covering topics 1-7

### 8. Model Selection and Cross-Validation
- **Theory:** Bias-variance tradeoff, cross-validation, information criteria 

- **Hands-on Lab:**
    - Model selection for predictive maintenance
    - Cross-validation for system identification
    - Hyperparameter tuning for models 

### 9. Clustering and Pattern Recognition
- **Theory:** K-means, hierarchical clustering, mixture models 

- **Hands-on Lab:**
    - Fault mode clustering in systems
    - Material property classification
    - Operational regime identification

### 10. Classification and Supervised Learning
- **Theory:** Linear discriminants, SVM, decision trees  

- **Hands-on Lab:**
    - Binary classification for equipment health monitoring
    - Quality control in manufacturing processes
    - Feature importance analysis

### 11. Neural Networks for Engineering
- **Theory:** Neural network basics, backpropagation, applications

- **Hands-on Lab:**
    - Neural networks for system identification
    - Nonlinear function approximation
    - Introduction to TensorFlow/Keras for engineering problems

### 12. Reinforcement Learning for Engineering Applications
- **Theory:** RL fundamentals, Q-learning, policy gradient methods, applications in control and optimization  

- **Hands-on Lab:**
    - RL for optimal control of mechanical systems
    - Optimization using reinforcement learning

