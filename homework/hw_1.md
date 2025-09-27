# Wind Turbine Data Analysis Homework

## Instructions
Create a new Jupyter notebook named `your_name_wind_turbine_analysis.ipynb` and complete all the questions below. Each question should be answered with code and include the output.

---

## Dataset Information
You will be working with a subset of the **United States Wind Turbine Database (USWTDB)**, which contains information about the locations of land-based and offshore wind turbines in the United States, corresponding wind project information, and turbine technical specifications. 

For more information about this dataset, visit: https://eerscmap.usgs.gov/uswtdb

The key columns you'll be working with include:
- `case_id`: Unique USWTDB identifier for each turbine
- `t_state`: State where turbine is located
- `t_county`: County where turbine is located
- `p_name`: Project name
- `p_year`: Year project became operational
- `p_tnum`: Number of turbines in project
- `p_cap`: Project capacity (MW)
- `t_manu`: Turbine original equipment manufacturer
- `t_model`: Turbine model
- `t_cap`: Turbine capacity (kW)
- `t_hh`: Turbine hub height (meters)
- `t_rd`: Turbine rotor diameter (meters)
- `t_rsa`: Turbine rotor swept area (meters²)
- `t_ttlh`: Turbine total height - calculated (meters)
- `xlong`: Longitude (decimal degrees)
- `ylat`: Latitude (decimal degrees)

---

## Part 1: Data Loading and Initial Exploration

### Question 1.1
Load the wind turbine dataset from the CSV file and display the first 10 rows.

### Question 1.2
Explore the dataset by finding:
- The shape of the dataset (number of rows and columns)
- The column names
- The data types of each column

### Question 1.3
Use `.info()` and `.describe()` to get a summary of the dataset. What insights can you gather about the data?

### Question 1.4
Check for missing values in each column. Which columns have missing values and how many?

---

## Part 2: Data Cleaning

### Question 2.1
Clean the dataset by:
- Removing all rows that have any missing values
- Resetting the index
- Checking that there are no missing values remaining

### Question 2.2
Compare the shape of the dataset before and after cleaning. How many rows were removed?

---

## Part 3: Data Selection and Filtering

### Question 3.1
Extract and display only the `p_name`, `t_state`, and `p_cap` columns as a new DataFrame.

### Question 3.2
Filter the dataset to show only projects with a project capacity (`p_cap`) greater than 100 MW. How many projects meet this criteria?

### Question 3.3
Find all turbines that meet BOTH of these conditions:
- Project capacity (`p_cap`) > 50 MW
- Individual turbine capacity (`t_cap`) > 2000 kW

Display the first 5 rows of this filtered data.

### Question 3.4
Use `.loc` to select rows 10 through 20 (inclusive) and display only the columns: `p_name`, `p_year`, and `t_manu`.

### Question 3.5
Filter the dataset to show only turbines from Texas ('TX') that became operational after 2015. How many turbines meet these criteria?

---

## Part 4: Basic Statistics and Analysis

### Question 4.1
Calculate the following statistics for the `t_hh` (hub height) column:
- Mean
- Median  
- Standard deviation
- Minimum and maximum values

### Question 4.2
Find the correlation between `t_hh` (hub height) and `t_ttlh` (total height). What does this correlation tell you?

### Question 4.3
For turbines in Colorado ('CO'), calculate the median hub height (`t_hh`). Round your answer to the nearest whole number.

### Question 4.4
Find the mean and standard deviation of rotor diameter (`t_rd`) for turbines in Iowa ('IA').

---

## Part 5: Categorical Analysis

### Question 5.1
Find the distribution of turbines by state (`t_state`). Which state has the most wind turbines?

### Question 5.2
Find the top 5 most common turbine manufacturers (`t_manu`) in the dataset.

### Question 5.3
Find the project name (`p_name`) that has the highest project capacity (`p_cap`).

### Question 5.4
For projects that became operational in 2015, what was the most common turbine manufacturer (`t_manu`)?

---

## Part 6: Groupby Analysis

### Question 6.1
Group the data by `t_state` and calculate:
- Mean project capacity (`p_cap`) for each state
- Count of turbines for each state
- Maximum hub height (`t_hh`) for each state

### Question 6.2
Group by `p_year` (year operational) and find the mean turbine capacity (`t_cap`) for each year. Which year had the highest average turbine capacity?

### Question 6.3
Group by `t_manu` (manufacturer) and count how many unique states (`t_state`) each manufacturer operates in using `.agg(['nunique'])`. Which manufacturer operates in the most states?

### Question 6.4
Filter the data to include only large projects with more than 10 turbines (`p_tnum` > 10), then group by `t_state` and count how many unique turbine models (`t_model`) are used in each state for these large projects.

---

## Part 7: Advanced Filtering and Analysis

### Question 7.1
Find all turbines that became operational in 2018 (`p_year` == 2018). How many turbines were there?

### Question 7.2
Create a boolean mask to find turbines where:
- Year operational (`p_year`) >= 2017
- Project capacity (`p_cap`) >= 100 MW
- State (`t_state`) is either 'TX',or 'IA'

How many turbines meet all these conditions?

### Question 7.3
For the turbines identified in Question 7.2, calculate the mean hub height (`t_hh`) and display the unique turbine manufacturers (`t_manu`) used in these projects.

### Question 7.4
Find all turbines where the hub height (`t_hh`) is above the overall dataset mean for hub height. How many such turbines are there, and what is the average rotor diameter (`t_rd`) for these tall turbines?

### Question 7.5
Find turbines that have both a rotor diameter (`t_rd`) greater than 100 meters AND a hub height (`t_hh`) greater than 80 meters. What is the most common manufacturer for these large, tall turbines?

---

## Submission Guidelines

1. **File naming**: Save your notebook as `your_name_wind_turbine_analysis.ipynb`

2. **Code requirements**:
   - Include clear comments explaining your approach for each question
   - Show all outputs (don't suppress print statements)
   - Use appropriate variable names
   - Include section headers for each part

3. **Answer format**: 
   - Write the question number as a markdown header
   - Include your code in code cells
   - For questions asking "how many" or requesting specific values, make sure to clearly display the answer
