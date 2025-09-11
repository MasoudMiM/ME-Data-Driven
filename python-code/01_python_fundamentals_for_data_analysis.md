# Python Fundamentals for Data Analysis

## Learning Objectives
By the end of this module, you will be able to:
- Use Python's essential data types for data analysis
- Work with lists and dictionaries to organize sensor data
- Write simple functions to process datasets
- Handle basic errors when working with data

---

## Essential Python Concepts

### 1. Variables and Data Types

Python has four main data types you'll use constantly in data analysis:

```python
temperature = 23.5          # float
sensor_count = 10           # int


sensor_id = "TEMP_001"      # string with double quotes
status = 'active'           # string with single quotes
description = '''Multi-line
string example'''           # string with triple quotes

my_string = "He is 5' 8\" tall"  # Using escape characters

# True/False for conditions
is_working = True           # boolean
is_offline = False          # boolean

# data types
print(type(temperature))    # <class 'float'>
print(type(sensor_count))   # <class 'int'>
print(type(sensor_id))      # <class 'str'>
print(type(is_working))     # <class 'bool'>
```

### 2. Lists - Your Data Collections

Lists store multiple values - perfect for sensor readings:

```python
temperatures = [22.1, 23.5, 24.2, 23.8, 22.9]

mixed_list = ['sensor1', 'sensor2', 10, 23.5, True]

# accesing data
first_temp = temperatures[0]      # 22.1
last_temp = temperatures[-1]      # 22.9 (negative indexing)
second_last = temperatures[-2]    # 23.8
all_but_first = temperatures[1:]  # [23.5, 24.2, 23.8, 22.9]

# slicing a list with step (every 3rd element starting from index 0)
every_third = temperatures[0::3]  # [22.1, 23.8]

# basic stats
average = sum(temperatures) / len(temperatures)
maximum = max(temperatures)
minimum = min(temperatures)
```

#### List Methods

Lists have many built-in methods for data manipulation:

```python
# adding single and mutiple values to a list
temperatures.append(20)
temperatures.extend([10, 12, 24, 16, 20])

count_20 = temperatures.count(20)  # How many times 20 appears

# removing and returning last item
last_item = temperatures.pop()

# copying lists (this creates an independent copy)
temperatures_backup = temperatures.copy()

# sorting list (NOTE: This modifies original list)
temperatures.sort()              # Ascending order
temperatures.sort(reverse=True)  # Descending order

# Get list length
list_length = len(temperatures)

total = sum(temperatures)
```

### 3. Dictionaries - Structured Data

Dictionaries store related information together using key-value pairs:

```python
sensor_reading = {
    'temperature': 24.3,
    'humidity': 65.8,
    'timestamp': '2024-01-15 14:30:00',
    'sensor_id': 'MULTI_001',
    'status': 'normal'
}

# accesing values
temp = sensor_reading['temperature']
status = sensor_reading['status']

# new data addition
sensor_reading['battery'] = 87

mixed_dict = {
    'key1': [1, 2, 3, 4, 5],      # string key, list value
    10: 'value1',                  # integer key, string value
    True: [12.3, 'value2']         # boolean key, list value
}

# adding new key-value pairs
mixed_dict[20] = 'my_string'

keys = mixed_dict.keys()      # Get all keys
values = mixed_dict.values()  # Get all values
items = mixed_dict.items()    # Get all key-value pairs
```

---

## 📝 IN-CLASS ASSIGNMENT - Data Fundamentals

**Create a new Jupyter notebook** named `your_name_python_fundamentals.ipynb`

### Exercise 1: Air Quality Monitor Setup
1. Create variables for an air quality monitoring system:
   - `monitor_id` (string): "AQ_Monitor_01"
   - `co2_level` (float): 415.8
   - `particle_count` (int): 1250  
   - `system_active` (boolean): True

2. Print each variable and its type using the `type()` function

### Exercise 2: Pollution Data Management
1. Create a list called `weekly_co2` with these 7 readings: `[405.2, 412.8, 418.1, 422.5, 419.7, 408.3, 401.9]`

2. Practice accessing data:
   - Print the third CO2 reading
   - Print the last two readings (using negative indexing)
   - Print readings 1-5 (using slicing)
   - Print every second reading starting from index 1

3. Calculate and print:
   - Total number of readings
   - Average CO2 level
   - Highest and lowest CO2 levels

### Exercise 3: Monitor Information System
1. Create a dictionary called `air_monitor` with these key-value pairs:
   - 'device_id': 'AQM_2024_001'
   - 'building': 'Science Hall'
   - 'floor': 3
   - 'measurements': ['CO2', 'PM2.5', 'temperature']
   - 'calibrated': True

2. Add a new key-value pair: `last_service`:`2024-02-01`

3. Print:
   - Only the measurements list
   - All dictionary keys
   - All dictionary values

**Complete these three exercises in your notebook before proceeding to the next part**

---

### 4. Loops for Processing Data

Process multiple data points efficiently with different loop patterns:

#### Basic For Loops
```python
temperatures = [19.2, 21.5, 23.8, 25.1, 24.6, 22.3, 20.7]

# iteration through values
for temp in temperatures:
    if temp > 25:
        print(f"Alert: High temperature {temp}°C")
```

#### Loops with Position Information
```python
# accessing both index and value using enumerate()
for i, temp in enumerate(temperatures):
    print(f"Day {i+1}: {temp}°C")
    
# Alternative approach using range() and len()
for i in range(len(temperatures)):
    print(f"Reading {i}: {temperatures[i]}°C")
```

### 📝 Exercise 4A: Basic Loop Practice
**Add this to your notebook after learning basic loops:**

Using your `weekly_co2` list from Part 1, write a loop that:
- Classifies each CO2 reading as "Good" (<400 ppm), "Moderate" (400-450 ppm), or "Poor" (>450 ppm)
- Prints the results in this format: "Week 1: 405.2 ppm - Moderate"

---

#### Conditional Processing and Counting
```python
# Count items meeting specific conditions
hot_readings = 0
cold_readings = 0
mild_readings = 0

for temp in temperatures:
    if temp > 24:
        hot_readings += 1
        print(f"Warm temperature: {temp}°C")
    elif temp < 20:
        cold_readings += 1
        print(f"Cold temperature: {temp}°C")
    else:
        mild_readings += 1
        print(f"Mild temperature: {temp}°C")

print(f"Summary: {hot_readings} warm, {mild_readings} mild, {cold_readings} cold")
```

### 📝 Exercise 4B: Counting with Loops
**Add this to your notebook after learning conditional processing:**

1. Modify your code from Exercise 4A to also count how many readings fall into each air quality category
2. Print a summary showing the total count for each category (Good, Moderate, Poor)

---

#### Data Filtering with Loops
```python
# Filter valid data from mixed input
mixed_data = [22.1, "error", 25.3, None, 21.8, "offline", 24.7]
valid_temps = []
invalid_count = 0

for item in mixed_data:
    if isinstance(item, (int, float)) and item is not None:
        valid_temps.append(item)
    else:
        invalid_count += 1
        print(f"Invalid reading: {item}")

print(f"Valid readings: {valid_temps}")
print(f"Invalid count: {invalid_count}")
```

### 📝 Exercise 4C: Data Filtering
**Add this to your notebook after learning data filtering:**

Create a new list called `particle_sensor_data` with mixed data:
```python
particle_sensor_data = [1205, "maintenance", 1350, None, 1180, "calibration", 1420, 1275]
```
Write code that loops through this list and:
- Counts valid numeric readings vs invalid entries
- Creates a new list with only the valid particle count readings

---

### 5. Functions for Reusable Code

Create functions to organize and reuse your code effectively:

#### Basic Function Structure
```python
def function_name(parameters):
    """Function description (docstring)"""
    # some operations...
    return result

# simple classification function
def classify_temperature(temp):
    """Classify a temperature reading"""
    if temp < 20:
        return "Cold"
    elif temp <= 24:
        return "Mild"
    else:
        return "Warm"

# calling the function
classification = classify_temperature(22.5)
print(classification) 
```

### 📝 Exercise 5A: Basic Functions
**Add this to your notebook after learning basic function structure:**

Write a function called `classify_air_quality(co2_ppm)` that:
- Takes a single CO2 reading in ppm as input
- Returns "Good", "Moderate", or "Poor" based on the ranges from Exercise 4A
- Test it with several CO2 values (e.g., 380, 425, 480)

---

#### Functions with Multiple Parameters
```python
def validate_temperature(temp, min_temp=0, max_temp=50):
    """Check if temperature is within valid range"""
    if not isinstance(temp, (int, float)):
        return False
    return min_temp <= temp <= max_temp

# Test the function
print(validate_temperature(25))      # True
print(validate_temperature("error")) # False
print(validate_temperature(-10))     # False
```

### 📝 Exercise 5B: Functions with Parameters
**Add this to your notebook after learning about function parameters:**

Write a function called `is_valid_particle_count(count, min_count=0, max_count=2000)` that:
- Takes a particle count and optional min/max bounds
- Returns True if the count is a number within the valid range
- Returns False otherwise
- Test it with various inputs including strings and numbers

---

#### Functions Returning Dictionaries
```python
def analyze_temperatures(temp_list):
    """Calculate comprehensive temperature statistics"""
    if not temp_list:  # Check for empty list
        return {
            'error': 'No data provided',
            'count': 0
        }
    
    stats = {
        'count': len(temp_list),
        'average': sum(temp_list) / len(temp_list),
        'min': min(temp_list),
        'max': max(temp_list),
        'range': max(temp_list) - min(temp_list)
    }
    return stats

# calling the function
temp_data = [19.2, 21.5, 23.8, 25.1, 24.6]
results = analyze_temperatures(temp_data)
print(f"Average: {results['average']:.1f}°C")
print(f"Range: {results['range']:.1f}°C")
```

### 📝 Exercise 5C: Functions Returning Dictionaries
**Add this to your notebook after learning about dictionary returns:**

Write a function called `co2_statistics(co2_list)` that:
- Takes a list of CO2 readings as input
- Returns a dictionary with keys: 'count', 'average', 'min', 'max', 'range'
- Test it with your `weekly_co2` data from Part 1
- Print the results in a user-friendly format

---

#### Functions with Data Processing
```python
def process_sensor_data(raw_data):
    """Process mixed sensor data and return clean results"""
    valid_readings = []
    invalid_count = 0
    
    for reading in raw_data:
        if isinstance(reading, (int, float)) and reading is not None:
            valid_readings.append(reading)
        else:
            invalid_count += 1
    
    return {
        'valid_data': valid_readings,
        'invalid_count': invalid_count,
        'total_count': len(raw_data)
    }
```

### 📝 Exercise 5D: Data Processing Functions
**Add this to your notebook after learning data processing functions:**

Write a function called `clean_particle_data(mixed_data)` that:
- Takes a list of mixed data (numbers, strings, None values)
- Returns a dictionary with 'valid_particles' (list) and 'invalid_count' (int)
- Test it with the `particle_sensor_data` from Exercise 4C

---

### 6. Error Handling

Handle problems gracefully using try/except blocks:

#### Basic Error Handling
```python
def safe_division(a, b):
    """Divide two numbers safely"""
    try:
        result = a / b
        return result
    except ZeroDivisionError:
        print("Error: Cannot divide by zero")
        return None
    except TypeError:
        print("Error: Invalid data types for division")
        return None
```

### 📝 Exercise 6A: Basic Error Handling
**Add this to your notebook after learning basic error handling:**

Write a function called `safe_co2_percentage(current_co2, baseline_co2)` that:
- Calculates percentage change: ((current - baseline) / baseline) * 100
- Uses try/except to handle division by zero and invalid inputs
- Returns the percentage change or an error message
- Test with both valid numbers and problematic inputs like zero baseline

---

#### Handling Different Types of Errors
```python
def safe_temperature_stats(temp_list):
    """Calculate temperature statistics with error handling"""
    try:
        # if input is a list
        if not isinstance(temp_list, list):
            raise TypeError("Input must be a list")
            
        # if list is empty
        if len(temp_list) == 0:
            return {'error': 'Empty list provided'}
        
        # filtering only numeric values
        numeric_temps = []
        for temp in temp_list:
            if isinstance(temp, (int, float)):
                numeric_temps.append(temp)
        
        # if any valid numbers found
        if len(numeric_temps) == 0:
            return {'error': 'No valid numeric data found'}
        
        # statistics
        stats = {
            'count': len(numeric_temps),
            'average': sum(numeric_temps) / len(numeric_temps),
            'min': min(numeric_temps),
            'max': max(numeric_temps)
        }
        return stats
        
    except TypeError as e:
        return {'error': f'Type error: {e}'}
    except Exception as e:
        return {'error': f'Unexpected error: {e}'}
```

### 📝 Exercise 6B: Comprehensive Error Handling
**Add this to your notebook after learning about different error types:**

Modify your `co2_statistics` function from Exercise 5C to handle errors:
- Check if the input is empty and return an appropriate message
- Handle cases where the list contains non-numeric values
- Use try/except blocks to catch and handle errors gracefully
- Test with these problematic inputs:
  ```python
  test_data_1 = []  # Empty list
  test_data_2 = ["sensor_error", "offline", None]  # No valid numbers
  test_data_3 = [410.5, "error", 425.8, 398.2]  # Mixed valid/invalid
  ```

---

#### Using Error Handling with Data Validation
```python
def validate_and_process_reading(reading):
    """Validate a single sensor reading"""
    try:
        # Try to convert to float
        temp = float(reading)
        
        # Check reasonable range for temperature
        if -50 <= temp <= 60:
            return {'valid': True, 'value': temp, 'error': None}
        else:
            return {'valid': False, 'value': None, 'error': 'Temperature out of range'}
            
    except (ValueError, TypeError):
        return {'valid': False, 'value': None, 'error': 'Invalid data type'}
    except Exception as e:
        return {'valid': False, 'value': None, 'error': f'Unexpected error: {e}'}

# Example usage
test_readings = [25.3, "error", None, "22.1", 150, -100]
for reading in test_readings:
    result = validate_and_process_reading(reading)
    if result['valid']:
        print(f"Valid: {result['value']}°C")
    else:
        print(f"Invalid '{reading}': {result['error']}")
```

### 📝 Exercise 6C: Data Validation with Error Handling
**Add this to your notebook after learning about data validation:**

Write a function called `validate_co2_reading(reading)` that:
- Takes a single reading (could be any data type)
- Uses try/except to safely convert it to a float
- Checks if it's in a reasonable CO2 range (200 to 800 ppm)
- Returns a dictionary with 'valid' (True/False), 'value', and 'error' keys
- Test it with: `[415.5, "sensor_fault", None, "420.8", 1200, 150]`

---

#### Comprehensive Data Processing Function
```python
def comprehensive_weather_processor(sensor_readings):
    """Complete weather data processing with error handling"""
    results = {
        'valid_readings': [],
        'invalid_count': 0,
        'error_types': [],
        'statistics': None
    }
    
    try:
        # Process each reading
        for i, reading in enumerate(sensor_readings):
            validation = validate_and_process_reading(reading)
            
            if validation['valid']:
                results['valid_readings'].append(validation['value'])
            else:
                results['invalid_count'] += 1
                results['error_types'].append(f"Position {i}: {validation['error']}")
        
        # Calculate statistics if we have valid data
        if results['valid_readings']:
            results['statistics'] = {
                'count': len(results['valid_readings']),
                'average': sum(results['valid_readings']) / len(results['valid_readings']),
                'min': min(results['valid_readings']),
                'max': max(results['valid_readings'])
            }
        
        return results
        
    except Exception as e:
        return {'error': f'Processing failed: {e}'}
```

### 📝 Exercise 6D: Final Comprehensive Exercise
**Add this to your notebook:**

Create a comprehensive air quality data processor by writing a function called `process_air_quality_data(sensor_readings)` that:
- Takes a list of mixed CO2 sensor readings (numbers, strings, None values)
- Uses your validation function from Exercise 6C to check each reading
- Collects valid readings and counts invalid ones
- Calculates statistics on valid readings using error handling
- Returns a summary dictionary with both the statistics and count of invalid readings

Test your function with this dataset:
```python
monthly_data = [412.5, "maintenance", 418.7, 422.1, None, "calibration", 408.9, 415.3, 420.8, "offline", 425.6, 410.2]
```

Your function should return something like:
```python
{
    'valid_readings': [412.5, 418.7, 422.1, 408.9, 415.3, 420.8, 425.6, 410.2],
    'invalid_count': 4,
    'statistics': {'count': 8, 'average': 417.0, 'min': 408.9, 'max': 425.6}
}
```

## Submission Instructions

**Submit your completed Jupyter notebook** (`your_name_python_fundamentals.ipynb`). Make sure your notebook includes:

- Clear section headers for each exercise
- Well-commented code explaining your approach
- Output from running each code cell
- Any observations or insights about your results
