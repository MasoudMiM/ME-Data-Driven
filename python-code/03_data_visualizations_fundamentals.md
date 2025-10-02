# Data Visualization for Data Analysis

## Learning Objectives
By the end of this module, you will be able to:
- Create effective visualizations using matplotlib, seaborn, and plotly
- Choose appropriate chart types for different data analysis scenarios
- Customize plots with labels, colors, and styling for professional presentation
- Use subplots to create comprehensive multi-panel visualizations

---

## 📝 IN-CLASS ASSIGNMENT Setup

**Create a new Jupyter notebook** named `your_name_data_visualization.ipynb`

You will complete exercises throughout this lesson in your notebook. Each exercise should be completed before moving to the next section.

---

## Introduction to Data Visualization

### Why Visualize Data?
Data visualization transforms numbers into insights. Good visualizations can reveal patterns, outliers, and relationships that are invisible in raw data tables.

### Essential Libraries

```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
import plotly.graph_objects as go


%matplotlib inline
```

### Plotting functions

```python
# plotting the Sine function between [0, 2pi]
x = np.linspace(0,2,50)
y = np.sin(x*np.pi)

plt.figure(figsize=(8, 5))
plt.plot(x, y, marker='o')
plt.title('Test Plot')
plt.xlabel('X values')
plt.ylabel('Y values')
plt.show()
```


## Bar Plots - Comparing Categories

### Basic Bar Charts

Bar plots are perfect for comparing quantities across different categories. They work best with categorical data on one axis and numerical data on the other.

```python
categories = ['Product A', 'Product B', 'Product C', 'Product D']
values = [23, 45, 56, 32]

# matplotlib version
plt.figure(figsize=(10, 6))
plt.bar(categories, values, color='skyblue')
plt.title('Sales by Product')
plt.xlabel('Products')
plt.ylabel('Sales (Units)')
plt.show()

# seaborn
plt.figure(figsize=(10, 6))
sns.barplot(x=categories, y=values)
plt.title('Sales by Product')
plt.show()
```

### Bar Charts with Real Data

```python
dft = sns.load_dataset('titanic')

display(dft.head())
print(f"Dataset shape: {dft.shape}")
print(f"Columns: {dft.columns.tolist()}")
```

### 📝 Exercise 1: Titanic Survival Analysis
**Complete this in your notebook before proceeding**

Using the Titanic dataset:
1. Load the dataset using `dfQ1 = sns.load_dataset('titanic')`
2. Explore the dataset structure (head, shape, columns, columns data types, descriptive statistics)
3. Create a vertical bar chart showing passenger survival by sex, with passenger class as hue:
   ```python
   # seaborn.barplot has a "hue" option that enables us to split by an additional categorical value. Essentially, "hue" shows how many different values an indicator can have.

   plt.figure(figsize=(10, 6))
   sns.countplot(data=dfQ1, x='sex', hue='survived', palette='Set2')
   plt.title('Titanic Survival by Gender')
   plt.xlabel('Gender')
   plt.ylabel('Number of Passengers')
   plt.show()
   ```
4. Create another bar chart showing survival by passenger class with sex as hue

---

## Scatter Plots - Exploring Relationships

### Basic Scatter Plots

Scatter plots reveal relationships between two continuous variables. They're essential for identifying correlations, clusters, and outliers.

Let's use 3D printer dataset. The aim of the dataset was to determine how much of the adjustment parameters in 3d printers affect the print quality, accuracy and strength. There are nine setting parameters and three measured output parameters.

Setting Parameters:
- Layer Height (mm)
- Wall Thickness (mm)
- Infill Density (%)
- Infill Pattern ()
- Nozzle Temperature (ºC)
- Bed Temperature (ºC)
- Print Speed (mm/s)
- Material ()
- Fan Speed (%)

Output Parameters: (Measured)
- Roughness (µm)
- Tension (ultimate) Strenght (MPa)
- Elongation (%) 

This data is based on the Ultimaker S5 3-D printer settings and filaments.

```python
# 3D printer data
url = 'https://raw.githubusercontent.com/MasoudMiM/ME_364/main/3D_Printer_Data/3DPrinterDataset.csv'
dfp = pd.read_csv(url)

print("3D Printer Dataset columns:")
print(dfp.columns.tolist())
print("\nDataset description:")
print(dfp.describe())
```

### Creating Scatter Plots

```python
plt.figure(figsize=(10, 6))
plt.scatter(dfp['layer_height'], dfp['roughness'], alpha=0.6)
plt.xlabel('Layer Height (mm)')
plt.ylabel('Roughness (μm)')
plt.title('3D Print Quality: Layer Height vs Surface Roughness')
plt.show()

# enhanced with seaborn - size and color
plt.figure(figsize=(12, 8))
sns.scatterplot(data=dfp, x='layer_height', y='roughness', 
                hue='material', size='infill_density', 
                sizes=(50, 200), alpha=0.7)
# The "sizes" argument shows a min, max tuple.
plt.title('3D Print Parameters Analysis')
plt.show()
```

### 📝 Exercise 2: 3D Printer Data Analysis
**Complete this in your notebook before proceeding**

Using the 3D printer dataset:
1. Load the dataset and explore its structure (describe, shape, info, etc)
2. Create a scatter plot showing the relationship between 'nozzle_temperature' and 'tension_strenght'
3. Create an enhanced scatter plot with:
   - X-axis: 'print_speed'
   - Y-axis: 'tension_strenght'  
   - Color (hue): 'material'
   - Size: 'infill_density'
4. Add appropriate title and axis labels
5. Calculate and display the correlation coefficient between print speed and tensile strength

---

## Box Plots - Understanding Distributions

### Box Plot Fundamentals

Box plots show the distribution of data through quartiles, helping identify outliers and compare distributions across categories.

```python
# age by class
plt.figure(figsize=(12, 6))
sns.boxplot(data=dft, x='class', y='age')
plt.title('Age Distribution by Passenger Class')
plt.xlabel('Passenger Class')
plt.ylabel('Age (years)')
plt.show()

# age by survival status
plt.figure(figsize=(10, 6))
sns.boxplot(data=dft, x='survived', y='age')
plt.title('Age Distribution by Survival')
plt.show()

# fare by passenger class
plt.figure(figsize=(10, 6))
sns.boxplot(data=dft, x='class', y='fare')
plt.title('Fare Distribution by Class')
plt.show()
```

### 📝 Exercise 3: Distribution Analysis
**Complete this in your notebook before proceeding**

Using the 3D printer dataset:
1. Create a box plot showing the distribution of 'roughness' by 'material' type
2. Create two separate box plots:
   - First: 'tension_strenght' by 'infill_pattern'
   - Second: 'elongation' by 'material'
3. Identify any outliers and print the corresponding data for thos outliers.

---

## Histogram Plots - Frequency Distributions

### Understanding Histograms

Histograms show the frequency distribution of a single continuous variable by dividing the data into bins.

```python
url = 'https://raw.githubusercontent.com/MasoudMiM/ME_364/main/Airfoil_noise/Airfoil_Noise.csv'
df1 = pd.read_csv(url, header=None, 
                  names=['Frequency (Hz)', 'Attack_Angle (deg)', 'Chord (m)', 'FS_Velocity (m/s)', 'SSD_Thickness (m)', 'Sound_Pressure_Level (dB)'])

print("Airfoil dataset loaded:")
display(df1.head())
```

### Creating Histograms

```python
# basic frequency distribution
plt.figure(figsize=(10, 6))
plt.hist(df1['Frequency (Hz)'], bins=20, color='skyblue', alpha=0.7, edgecolor='black')
plt.title('Distribution of Frequency')
plt.xlabel('Frequency (Hz)')
plt.ylabel('Count')
plt.show()

# sound pressure level
plt.figure(figsize=(10, 6))
plt.hist(df1['Sound_Pressure_Level (dB)'], bins=25, color='lightcoral', alpha=0.7, edgecolor='black')
plt.title('Distribution of Sound Pressure Level')
plt.xlabel('Sound Pressure Level (dB)')
plt.ylabel('Count')
plt.show()
```

### Overlapping Histograms

```python
# compare different attack angles
low_angle = df1[df1['Attack_Angle (deg)'] <= 5]
high_angle = df1[df1['Attack_Angle (deg)'] > 10]

plt.figure(figsize=(12, 6))
plt.hist(low_angle['Sound_Pressure_Level (dB)'], alpha=0.6, label='Low Angle (≤5°)', 
         bins=20, color='blue')
plt.hist(high_angle['Sound_Pressure_Level (dB)'], alpha=0.6, label='High Angle (>10°)', 
         bins=20, color='red')
plt.xlabel('Sound Pressure Level (dB)')
plt.ylabel('Frequency')
plt.title('Sound Pressure Distribution by Attack Angle')
plt.legend()
plt.show()
```

### 📝 Exercise 4: Histogram Analysis
**Complete this in your notebook before proceeding**

Using the airfoil noise dataset:
1. Create a histogram of the 'Chord (m)' variable with 5 bins
2. Create overlapping histograms showing 'FS_Velocity (m/s)' for different frequency ranges:
   ```python
   # Filter data for different frequency ranges
   low_freq = df1[df1['Frequency (Hz)'] <= 1000]
   high_freq = df1[df1['Frequency (Hz)'] > 10000]
   
   plt.figure(figsize=(12, 7))
   plt.hist(low_freq['FS_Velocity (m/s)'], alpha=0.6, label='Low Frequency (≤1000 Hz)', 
            bins=5, color='green')
   plt.hist(high_freq['FS_Velocity (m/s)'], alpha=0.6, label='High Frequency (>3000 Hz)', 
            bins=5, color='purple')
   plt.xlabel('Free Stream Velocity (m/s)')
   plt.ylabel('Count')
   plt.title('Velocity Distribution by Frequency Range')
   plt.legend()
   plt.show()
   ```
3. Calculate and compare the mean free stream velocities for low vs high frequency ranges
4. Create a third histogram showing the distribution of 'SSD_Thickness (m)' with appropriate bin size

---

## Pie Charts - Part-to-Whole Relationships

### Creating Effective Pie Charts

Pie charts work best for showing how parts make up a whole, especially with categorical data that has clear proportions.

```python
survival_counts = dft['survived'].value_counts()

plt.figure(figsize=(8, 8))
plt.pie(survival_counts.values, labels=['Did not survive', 'Survived'], 
        autopct='%1.1f%%', startangle=90, colors=['lightcoral', 'lightblue'])
plt.title('Titanic Passenger Survival')
plt.show()

# class distribution
class_counts = dft['class'].value_counts()
plt.figure(figsize=(8, 8))
plt.pie(class_counts.values, labels=class_counts.index, 
        autopct='%1.1f%%', startangle=90, colors=['gold', 'lightgreen', 'plum'])
plt.title('Passenger Class Distribution')
plt.show()
```

### 📝 Exercise 5: Pie Chart Analysis
**Complete this in your notebook before proceeding**

Using the 3D printer dataset:
1. Create a pie chart showing the distribution of different materials used
2. Create a pie chart showing the distribution of infill patterns

---

## Bubble Charts - Three-Dimensional Data

### Advanced Scatter Plots with Size

Bubble charts add a third dimension to scatter plots by varying the size of points based on a third variable.

```python
# data available for energy generated using various renewable resources in the UK for different years in different regions.
url = 'https://raw.githubusercontent.com/MasoudMiM/ME_364/main/UK_Renewable_Energy/UKEnergy.csv'
dfUK = pd.read_csv(url)

print("UK Energy dataset:")
print(dfUK.head(10))
print(f"Columns: {dfUK.columns.tolist()}")
```

### Creating Bubble Charts

```python
plt.figure(figsize=(12, 8))

# using first 200 rows for clarity
sample_data = dfUK.head(200)

plt.scatter(sample_data.iloc[:, 0], sample_data.iloc[:, 2], 
           s=sample_data.iloc[:, 4]*0.1, # size based on 3rd variable
           alpha=0.6, c=range(len(sample_data)), cmap='viridis')

plt.xlabel('Year')
plt.ylabel('Wind')
plt.title('UK Renewable Energy - Bubble Chart')
plt.colorbar(label='Total')
plt.show()
```

### Interactive Bubble Charts with Plotly

```python
# interactive version
fig = px.scatter(dfUK.head(200), 
                 x=dfUK.columns[0], y=dfUK.columns[2],
                 size=dfUK.columns[4],
                 hover_name=dfUK.columns[0],
                 title="Interactive UK Energy Data")
fig.show()
```

### 📝 Exercise 6: Bubble Chart Creation
**Complete this in your notebook before proceeding**

Using the 3D printer dataset:
1. Create a bubble chart with:
   - X-axis: layer height
   - Y-axis: tensile strength
   - Bubble size: infill density
2. Create an interactive version using Plotly Express. For this plot, also include color: for material type.
3. Identify any interesting patterns or clusters in the data

---

## Maps - Simple Geospatial Visualization

Maps help visualize data with geographic components, revealing spatial patterns and regional differences.

```python
import folium

# map centered on NY state
ny_map = folium.Map(location=[42.9538, -75.5268], zoom_start=7)

df_nysev = pd.read_csv('https://raw.githubusercontent.com/MasoudMiM/ME_364/main/EVStations_NY/EVChargingStations_NY_Sep12.csv')

# add circle markers for each station
for lat, lon, name, addr in zip(df_nysev['Latitude'], df_nysev['Longitude'], df_nysev['Station Name'], df_nysev['Street Address']):
    folium.CircleMarker(
        location=[lat, lon],
        popup=f"{name} - {addr}",
        color='blue',
        fill=True
    ).add_to(ny_map)

ny_map
```

## Subplots - Creating Multi-Panel Visualizations

### Understanding Subplots

Subplots allow you to combine multiple visualizations into a single figure, making it easier to compare different aspects of your data or tell a comprehensive story.

### Basic Subplot Layouts

```python
# basic 2x2 subplot layout
fig, axes = plt.subplots(2, 2, figsize=(15, 12))

# top left: bar plot
survival_by_class = dft.groupby('class')['survived'].mean()
axes[0, 0].bar(survival_by_class.index, survival_by_class.values, color='steelblue')
axes[0, 0].set_title('Survival Rate by Class')
axes[0, 0].set_ylabel('Survival Rate')

# top right: histogram  
axes[0, 1].hist(dft['age'].dropna(), bins=20, color='lightgreen', alpha=0.7, edgecolor='black')
axes[0, 1].set_title('Age Distribution')
axes[0, 1].set_xlabel('Age')
axes[0, 1].set_ylabel('Frequency')

# bottom left: box plot
dft.boxplot(column='fare', by='class', ax=axes[1, 0])
axes[1, 0].set_title('Fare Distribution by Class')
axes[1, 0].set_xlabel('Class')

# bottom right: scatter plot
scatter = axes[1, 1].scatter(dft['age'], dft['fare'], alpha=0.5, c=dft['survived'], cmap='RdYlBu')
axes[1, 1].set_title('Age vs Fare (colored by survival)')
axes[1, 1].set_xlabel('Age')
axes[1, 1].set_ylabel('Fare')
plt.colorbar(scatter, ax=axes[1, 1], label='Survived')

plt.suptitle('Titanic Dataset Analysis Dashboard', fontsize=16)
plt.tight_layout()
plt.show()
```

## Submission Instructions

**Submit your completed Jupyter notebook** (`your_name_data_visualization.ipynb`). Make sure your notebook includes:

- Clear section headers for each exercise
- Output from running each code cell showing the plots

## Final Comment

Focus on creating visualizations that not only look good but also effectively communicate insights from the data. Pay special attention to your subplot layouts - they should enhance understanding by allowing easy comparison and revealing different facets of your data.