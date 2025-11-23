# Final Project
## ME 371: Data-Driven Problem Solving
## Fall 2025

---

## Table of Contents
- [Introduction](#introduction)
- [Important Dates](#important-dates)
- [Project Overview](#project-overview)
- [Dataset Options](#dataset-options)
  - [Provided Datasets](#provided-datasets)
  - [Custom Dataset Requirements](#custom-dataset-requirements)
- [Project Requirements](#project-requirements)
  - [Technical Components](#technical-components)
- [Grading Criteria](#grading-criteria)
- [Progress Report](#progress-report)
- [Video Presentation Requirements](#video-presentation-requirements)
- [Submission Guidelines](#submission-guidelines)
- [Frequently Asked Questions](#frequently-asked-questions)

---

## Introduction

This document describes the final project for ME 371: Data-Driven Problem Solving. You will conduct a comprehensive machine learning analysis, including exploratory data analysis, model development, optimization, and evaluation. This project can be completed individually or in groups of two.

You have two options for your dataset:
1. Use one of the three provided datasets
2. Choose your own dataset related to your interests

The project requires submission of a well-documented **Jupyter notebook**, **PowerPoint presentation slides**, and a **recorded video presentation** demonstrating your work.

---

## Important Dates

| Milestone | Date | Deliverable |
|-----------|------|-------------|
| Project Released | Tuesday, November 25 | - |
| Progress Report Due | Sunday, December 7, 11:59 PM | Progress report (PDF) |
| Final Submission | Friday, December 19, 11:59 PM | Notebook + PowerPoint + Video |

---

## Project Overview

**Goal**: Develop and evaluate machine learning models for a classification problem of your choice.

**Team Structure**: Individual or groups of 2 students

**Deliverables**:
1. Jupyter notebook with complete analysis
2. PowerPoint presentation slides
3. 10-minute recorded video presentation
4. Progress report (due December 7)

**Project Focus**: Your project must focus on a **classification task**:
- Binary classification (2 classes)
- Multi-class classification (3+ classes)

**Examples of classification problems**:
- Image classification (objects, medical images, handwritten digits)
- Anomaly detection (fraud detection, defect detection)
- Medical diagnosis
- Predictive maintenance (will equipment fail? yes/no)
- Species identification
- Text categorization (spam detection, sentiment analysis)

---

## Dataset Options

You have the flexibility to either use one of the provided datasets or find your own dataset that aligns with your interests.

### Provided Datasets

#### Dataset I: Aviation Accidents Database

This dataset is part of the National Transportation Safety Board (NTSB) aviation accident database. The provided dataset includes recorded "events" from 2008 to 2022 for civil aviation accidents and incidents within the United States.

- **Source**: [NTSB Aviation Data](https://data.ntsb.gov/avdata)
- **Format**: CSV with data dictionary
- **Size**: Multiple thousands of records
- **Potential Classification Tasks**: 
  - Predict accident severity (fatal vs. non-fatal)
  - Predict accident type/category
  - Predict whether weather was a contributing factor
  - Classify phase of flight when accident occurred
- **Dataset**: Download the dataset from [here](https://drive.google.com/file/d/1hwBg2jSRLCty9x9VjYfB3LpGK8MpNnN2/view?usp=sharing).

#### Dataset II: Building Energy Database

This dataset contains synthetic building operation data including HVAC, lighting, miscellaneous electric loads, occupant counts, environmental parameters, and energy consumption at 1-hour intervals for years 2001 and 2005.

- **Source**: [Nature Scientific Data](https://www.nature.com/articles/s41597-021-00989-6)
- **Format**: Pickle file (use `pandas.read_pickle()`)
- **Size**: Thousands of hourly records
- **Potential Classification Tasks**:
  - Classify high vs. low energy consumption periods
  - Predict occupancy levels (low/medium/high)
  - Classify operational modes (heating/cooling/neutral)
  - Identify anomalous operation patterns
- **Dataset**: Download the dataset from [here](https://drive.google.com/file/d/19_FI4MtcwCAPppSGPCg_L8EDlJde8GOs/view?usp=sharing).

#### Dataset III: CIFAR-10 Image Dataset

A subset of the CIFAR-10 dataset consisting of 50,000 32×32 color images across 10 classes (airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck).

- **Source**: [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html)
- **Format**: Image files + CSV with labels
- **Size**: 50,000 images
- **Classification Task**: Multi-class image classification (10 classes)
- **Dataset**: Download the dataset from [here](https://drive.google.com/file/d/19Z13J4fcugjoaQb8SozJLEgdJbdaelnR/view?usp=sharing).

**Note**: You will need to research how to load and process images in Python. As an example, take a look at the the homework `Homework: Cast Manufactured Part Classification`.

---

### Custom Dataset Requirements

If you choose to use your own dataset, it must meet the following criteria:

| Data Type | Minimum Samples | Minimum Features | Notes |
|-----------|----------------|------------------|-------|
| **Structured/Tabular Data** | 1,000 samples | 5 features | CSV, Excel, etc. |
| **Image Data** | 500 samples | N/A | At least 2 classes |
| **Audio Data** | 500 samples | N/A | At least 2 classes |

**Additional Requirements for Custom Datasets**:
- Must be suitable for classification (have clear class labels)
- At least 2 classes (binary) or 3+ classes (multi-class)
- **Must properly cite your data source** in your notebook
- Avoid datasets already analyzed in class

**Recommended Data Sources**:
- [Kaggle Datasets](https://www.kaggle.com/datasets)
- [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php)
- [Google Dataset Search](https://datasetsearch.research.google.com/)
- [AWS Open Data](https://registry.opendata.aws/)
- [Data.gov](https://data.gov/)
- [Papers with Code Datasets](https://paperswithcode.com/datasets)

**Note**: If using a custom dataset, briefly justify your choice in the introduction section of your notebook.

---

## Project Requirements

Your project must include all components listed below. These requirements apply whether you use a provided dataset or your own.

### Technical Components

#### 1. Problem Definition and Introduction (5 points)

- **Clear problem statement**: What classification problem are you solving?
- **Motivation**: Why is this problem important or interesting?
- **Dataset description**: 
  - Source and citation
  - Number of samples and features
  - Class distribution
  - Any known challenges
- **Success criteria**: What metrics will you use? What performance would be considered "good"?

---

#### 2. Exploratory Data Analysis (15 points)

**Data Overview**:
- Dataset dimensions and structure
- Feature types (numerical, categorical)
- Class distribution (check for imbalance)
- Missing values analysis

**Statistical Analysis**:
- Descriptive statistics for numerical features
- Distribution analysis for each feature
- Correlation analysis between features
- Outlier detection and analysis

**Visualizations** (minimum 5 meaningful plots):
- Class distribution
- Feature distributions
- Correlation heatmap
- Box plots or simlar plots for feature comparison across classes
- Any other relevant visualizations

**Key Questions to Address**:
- Are there any data quality issues?
- Are the classes balanced or imbalanced?
- Which features appear most relevant?
- Are there any obvious patterns or relationships?

---

#### 3. Data Preprocessing and Cleaning (10 points)

**Required Preprocessing Steps**:

1. **Handle Missing Values**
   - Identify extent of missing data
   - Choose appropriate strategy (drop, impute, etc.)
   - Justify your decisions

2. **Feature Engineering** (if applicable)
   - Create new features that might be useful
   - Transform existing features properly

3. **Feature Scaling/Normalization**
   - Apply when appropriate for your algorithms
   - Use StandardScaler, MinMaxScaler, or other methods
   - Document your choice

4. **Handle Imbalanced Data** (if applicable)
   - Use resampling techniques (SMOTE, under/oversampling)
   - Document your approach

5. **Data Splitting**
   - Train-test split (or train-validation-test)
   - Use stratified splitting for imbalanced data
   - Clearly state split ratios

**Important**: Document and justify all preprocessing decisions.

---

#### 4. Model Development (15 points)

**Required**: Implement at least **TWO different algorithms**:

**Algorithm Requirements**:
- At least **one algorithm** must be from those discussed in class:
  - Logistic Regression
  - K-Nearest Neighbors (KNN)
  - Neural Networks (Shallow or Deep)
  - Decision Trees
  
- The **second algorithm** can be:
  - Another algorithm from class, OR
  - A more advanced algorithm such as:
    - Random Forests
    - Gradient Boosting (XGBoost, LightGBM, CatBoost)
    - Support Vector Machines (SVM)
    - Ensemble methods (Bagging, Boosting, Stacking)
    - Convolutional Neural Networks (for images)
    - Advanced architectures (ResNet, VGG, etc.)

**For Each Model**:
- Describe the model architecture/configuration
- Document hyperparameters used
- Show training process (loss curves, convergence)
- Implement a simple baseline model for comparison

**Note**: You are encouraged to explore algorithms beyond what was covered in class. This is an opportunity to learn something new and demonstrate initiative.

---

#### 5. Model Optimization and Refinement (15 points)

**Required Optimization Techniques**:

1. **Hyperparameter Tuning**
   - Grid Search or Random Search
   - Document search space
   - Show results of different configurations

2. **Cross-Validation**
   - Use K-Fold or Stratified K-Fold
   - Report cross-validation scores
   - Compare with simple train-test split

3. **Feature Selection**
   - Feature importance analysis
   - Recursive Feature Elimination (RFE)
   - Or other selection methods
   - Show impact on performance


**Analysis**:
- Compare performance before and after optimization
- Discuss overfitting/underfitting
- Document iterative improvements

---

#### 6. Performance Evaluation (15 points)

**Required Evaluation Metrics**:

For **all classification models**, report:
- Accuracy
- Precision (per class and average)
- Recall (per class and average)
- F1-Score (per class and average)
- Confusion Matrix (visualization)

**Model Comparison**:
- Create comparison table of all models
- Visualize performance differences

**Cross-Model Analysis**:
- Which model performs best? Why?
- Trade-offs between models (speed vs. accuracy, interpretability vs. performance)
- When would you choose one model over another?

---

#### 7. Results Interpretation and Discussion (10 points)

**Interpret Your Results**:
- What do your models tell you about the problem?
- Which features are most important? Why?
- Are there patterns in misclassifications?
- How does performance vary across classes?

**Limitations and Challenges**:
- What limitations does your analysis have?
- What challenges did you encounter?
- What would you do differently?

**Real-World Applicability**:
- How could your model be used in practice?
- What considerations would be needed for deployment?
- What are potential risks or ethical concerns?

**Future Work**:
- What improvements could be made?
- What additional data would be helpful?
- What other approaches might work better?

---

## Grading Criteria

**Total: 100 points**

| Component | Points | Description |
|-----------|--------|-------------|
| **Progress Report** | 8 | Demonstrates meaningful progress, clear problem definition, realistic timeline |
| **Problem Definition** | 5 | Clear problem statement, motivation, dataset description, success criteria |
| **Exploratory Data Analysis** | 15 | Comprehensive statistical analysis, meaningful visualizations, data quality assessment, insights |
| **Data Preprocessing** | 10 | Appropriate handling of missing values, feature engineering, scaling, train-test split, documentation |
| **Model Development** | 15 | At least 2 algorithms (1 from class, 1 from class or advanced), proper implementation, baseline comparison |
| **Model Optimization** | 15 | Optimization techniques, hyperparameter tuning, addressing over/underfitting |
| **Performance Evaluation** | 15 | Multiple metrics, confusion matrix, model comparison, error analysis, thorough evaluation |
| **Results & Discussion** | 10 | Interpretation of results, limitations, real-world applicability, future work |
| **Documentation & Code Quality** | 7 | Well-organized notebook, clear comments, professional presentation, proper citations |

---

## Progress Report

**Due: Sunday, December 7, 11:59 PM**

Submit a progress report that demonstrates you are on track to complete the project.

### Required Elements

**1. Header Information**
- Your name (or both names if working in a group)
- Project title
- Date

**2. Dataset Selection** (0.5 pages)
- Which dataset are you using (provided or custom)?
- If custom: source, size, and citation
- Brief description of the dataset
- Verification that it meets size requirements

**3. Problem Statement** (0.5 pages)
- What classification problem are you solving?
- Why is this interesting or important?
- What are your target classes?

**4. Progress Summary** (1-2 pages)

**Completed Work**:
- EDA findings (include 1-2 sample visualizations)
- Data preprocessing steps completed
- Initial model(s) implemented
- Any preliminary results

**Code Snippets**: Include brief examples showing:
- Data loading
- At least one visualization
- Evidence of model implementation

**5. Work Plan** (0.5 pages)
- What remains to be done?
- Timeline for completing remaining tasks
- If working in a group: division of responsibilities
- Any challenges or concerns?

**Format**: Submit as a **PDF document** (2-4 pages total)

**Grading**: Progress report is worth **8 points** (included in total 100 points)

**Evaluation Criteria**:
- Demonstrates meaningful progress (not just planning)
- Clear problem definition
- Dataset selected and analyzed
- Realistic timeline for completion
- Professional presentation

**Purpose**: The progress report ensures you're on track and provides an opportunity for early feedback. Students making insufficient progress will receive guidance.

---

## Video Presentation Requirements

Record a **10-minute video presentation** that demonstrates your work and findings. You should create PowerPoint slides to accompany your presentation.

### PowerPoint Slide Requirements

Create a professional PowerPoint presentation with the following structure:

**Recommended Slide Organization** (10-15 slides total):

1. **Title Slide**
   - Project title
   - Your name(s)
   - Course: ME 371 - Fall 2025
   - Date

2. **Problem Statement** (1-2 slides)
   - What problem are you solving?
   - Why is it important?
   - Dataset overview

3. **Exploratory Data Analysis** (2-3 slides)
   - Key data characteristics
   - Important visualizations
   - Initial insights

4. **Methodology** (2-3 slides)
   - Data preprocessing steps
   - Models selected and why
   - Optimization techniques applied

5. **Results** (3-4 slides)
   - Performance metrics comparison
   - Confusion matrix
   - Model comparison visualizations
   
6. **Discussion** (1-2 slides)
   - Key findings
   - Limitations
   - Future work

7. **Conclusions** (1 slide)
   - Summary of achievements
   - Main takeaways

**Slide Design Tips**:
- Use clear, readable fonts (minimum 18pt for body text)
- Include visualizations from your notebook
- Use bullet points, not paragraphs
- Maintain consistent formatting
- Include slide numbers
- Cite data sources

---

### Video Content Requirements

**1. Introduction (1-2 minutes)**
- Introduce yourself/yourselves
- Problem statement and motivation
- Dataset description (source, size, classes)
- Brief overview of your approach

**2. Code Walkthrough (5-6 minutes)**
- Show your Jupyter notebook (screen recording)
- Highlight key sections:
  - Interesting EDA findings
  - Data preprocessing decisions
  - Model architectures/implementations
  - Training process
  - Optimization techniques applied
- **Don't read code line-by-line** - explain concepts and design decisions
- Show 1-2 interesting visualizations

**3. Results and Discussion (2-3 minutes)**
- Show performance metrics and comparison
- Present confusion matrix
- Demonstrate best model predictions
- Discuss feature importance
- Key insights and conclusions
- Limitations and future work

---

### Technical Requirements

| Requirement | Specification |
|-------------|---------------|
| **Duration** | Exactly 10 minutes (±30 seconds) |
| **Format** | MP4, MOV, or AVI |
| **File Size** | Maximum 500 MB |
| **Resolution** | Minimum 720p (1280×720) |
| **Audio** | Clear audio - test your microphone |
| **Content** | PowerPoint slides + screen recording of notebook + voiceover |

---

### Presentation Tips

**Before Recording**:
- Write a script or outline
- Practice your presentation multiple times
- Time yourself to ensure you're within 10 minutes
- Close unnecessary applications
- Clean up your desktop

**During Recording**:
- Speak clearly and at a moderate pace
- Use a quiet environment
- Show your face (picture-in-picture) if comfortable
- Use cursor/highlighting to draw attention to important parts
- Zoom in on code when necessary
- Pause briefly between sections

**After Recording**:
- Watch your video to check quality
- Verify audio is clear throughout
- Ensure all demonstrations work properly
- Check file size and format

---

### File Naming

**Notebook** (Individual): `ME371_FinalProject_YourLastName.ipynb`

**Notebook** (Group): `ME371_FinalProject_LastName1_LastName2.ipynb`

**PowerPoint** (Individual): `ME371_FinalProject_YourLastName.pptx`

**PowerPoint** (Group): `ME371_FinalProject_LastName1_LastName2.pptx`

**Video** (Individual): `ME371_FinalProject_YourLastName.mp4`

**Video** (Group): `ME371_FinalProject_LastName1_LastName2.mp4`

---

## Submission Guidelines

### What to Submit

**By December 19, 11:59 PM**, submit the following files:

1. **Jupyter Notebook** (.ipynb file)
2. **PowerPoint Presentation** (.pptx file)
3. **Video Presentation** (.mp4, .mov, or .avi file)

**Optional**: If your notebook requires specific data files not publicly available, include them or provide download instructions in the notebook.

---

### Notebook Requirements

Your notebook should be a professional-quality document suitable for sharing with colleagues or potential employers.

#### Notebook Structure

**1. Header Section** (Markdown cell at top)
```markdown
# Final Project: [Your Project Title]
## ME 371: Data-Driven Problem Solving
## Fall 2025

**Name(s)**: Your Name (and partner's name if applicable)
**Date**: December 19, 2025
**Dataset**: [Name and source of your dataset]
```

**2. Table of Contents**
- Use markdown headers (##, ###) for sections
- Organize logically

**3. Required Sections**
1. Introduction and Problem Statement
2. Data Loading and Overview
3. Exploratory Data Analysis
4. Data Preprocessing
5. Model Development
   - Model 1: [Name]
   - Model 2: [Name]
6. Model Optimization
7. Model Evaluation and Comparison
8. Results and Discussion
9. Conclusions
10. References

---

### Code Quality Standards

#### Variable Naming
- Use descriptive, meaningful names
- Follow Python conventions (snake_case)
- Examples:
  - ✅ `train_accuracy`, `confusion_matrix`, `best_model`
  - ❌ `a`, `x1`, `temp`, `thing`

#### Code Comments
- Explain *why*, not just *what*
- Comment complex logic

#### Code Organization
- One logical task per cell when possible
- Keep cells under 50 lines when practical
- Remove experimental/debugging code
- Group related imports at the top
- Limit line length to 79-88 characters

#### Output Management
- Include all relevant outputs
- **Don't print large datasets or arrays**
- Use `.head()`, `.tail()`, `.sample()` to display data
- Clear unnecessary print statements

---

### Markdown Documentation

#### Explanations
- Explain your reasoning and decisions
- Interpret results and findings
- Discuss implications
- Each section should have text explaining what you're doing and why

#### Formatting
- Use headers for organization:
  - `##` for main sections
  - `###` for subsections
  - `####` for sub-subsections
- Use **bold** for emphasis
- Use bullet points and numbered lists
- Include equations using LaTeX, if you are familiar with it:
  
  The accuracy is calculated as: $\frac{TP + TN}{TP + TN + FP + FN}$
  

#### Visualizations
**Every plot must have**:
- Descriptive title
- Labeled axes with units
- Legend (when appropriate)
- Appropriate colors/styles
- Caption explaining what it shows

```python
plt.figure(figsize=(10, 6))
plt.plot(history.history['accuracy'], label='Training Accuracy')
plt.plot(history.history['val_accuracy'], label='Validation Accuracy')
plt.title('Model Accuracy Over Epochs')
plt.xlabel('Epoch')
plt.ylabel('Accuracy')
plt.legend()
plt.grid(True, alpha=0.3)
plt.show()
```

---

### Citations and References

**Required Citations**:
- Dataset source (with URL)
- Any external code used (with URLs)
- Papers or articles referenced

**Format** (use Markdown at end of notebook):
```markdown
## References

1. Dataset: [Name]. Available at: [URL]
2. Smith, J. et al. (2023). Paper title. Journal Name.
3. Code adapted from: [URL]
4. scikit-learn documentation: https://scikit-learn.org/
```

---

### Before Submitting

1. **Clean Up Notebook**
   - Remove experimental/debugging code
   - Remove empty cells
   - Check for TODOs or incomplete sections
   - Verify all markdown cells are properly formatted

2. **Restart and Run All**
   - Kernel → Restart & Run All
   - Verify all cells execute without errors
   - Check that all outputs display correctly
   - Verify execution time is reasonable

3. **Review Content**
   - Read through entire notebook
   - Check for typos and grammar
   - Ensure logical flow
   - Verify all visualizations have titles and labels
   - Confirm all requirements addressed

4. **Verify Files**
   - Notebook has correct filename
   - PowerPoint has correct filename
   - Video has correct filename
   - Video plays correctly and is under 10 minutes
   - Progress report was submitted on time

5. **Check PowerPoint**
   - All slides are complete
   - Visualizations are clear and readable
   - Formatting is consistent
   - No typos or errors


### Using External Resources

**You MUST**:
- Understand every line of code in your submission
- Cite all external sources (code, tutorials, papers)
- Adapt code to your specific problem (don't just copy-paste)
- Be able to explain your code in the video presentation

**Using LLMs/AI Tools**:
- Can be used for learning and debugging
- Cannot be used to generate entire sections without understanding
- You must be able to explain and justify all code
- Document when you use AI assistance

---

## Frequently Asked Questions

**Q: Can I work alone or do I need a partner?**
A: You can work either individually or with one partner. Groups of 3+ are not allowed.

**Q: Can I use a dataset from Kaggle?**
A: Yes! Just make sure it meets the size requirements and is suitable for classification.

**Q: What if my dataset has 50,000 samples? Do I need to use all of them?**
A: You can use a subset for computational efficiency, but mention this and justify the sample size.

**Q: Can I use pre-trained models (like ResNet for images)?**
A: Yes! Using transfer learning is encouraged for image data. Just make sure you understand how it works and can explain it.

**Q: How detailed should the video presentation be?**
A: Focus on high-level explanation and key results. You don't need to show every single line of code.

**Q: What happens if I miss the progress report deadline?**
A: You'll lose 8 points. However, the progress report is meant to help you stay on track, so try to submit it on time.

**Q: Can I change my dataset after the progress report?**
A: Only if you have a very good reason. Email me first to discuss.

**Q: What if my models aren't performing well?**
A: That's okay! Document what you tried, analyze why it didn't work, and discuss what could be improved. Negative results are still valuable.

**Q: Do I need to submit the PowerPoint separately from the video?**
A: Yes, submit both the PowerPoint file (.pptx) and the video recording separately.

**Q: Can I use Jupyter notebook slides instead of PowerPoint?**
A: No, please use PowerPoint (.pptx) or Google Slides (exported as .pptx) for consistency.

**Q: Can I use Google Colab for my project?**
A: Yes, Google Colab is acceptable, especially for computationally intensive tasks. Just make sure to download and submit your notebook as a .ipynb file.

**Q: How much time should I allocate for this project?**
A: Plan for approximately 30-40 hours of work total, distributed over the 3-4 weeks. Start early to avoid last-minute stress.

**Q: What if I encounter technical difficulties close to the deadline?**
A: Start early to allow time for troubleshooting. If you encounter issues, contact me as soon as possible, not on the day of the deadline.

