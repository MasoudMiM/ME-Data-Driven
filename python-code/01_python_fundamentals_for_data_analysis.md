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
# Numbers for measurements
temperature = 23.5          # float
sensor_count = 10           # int

# Text for labels and categories - Multiple string formats
sensor_id = "TEMP_001"      # string with double quotes
status = 'active'           # string with single quotes
description = '''Multi-line
string example'''           # string with triple quotes

# Handle special characters in strings
my_string = "He is 5' 8\" tall"  # Using escape characters

# True/False for conditions
is_working = True           # boolean
is_offline = False          # boolean

# Check data types
print(type(temperature))    # <class 'float'>
print(type(sensor_count))   # <class 'int'>
print(type(sensor_id))      # <class 'str'>
print(type(is_working))     # <class 'bool'>
```

### 2. Lists - Your Data Collections

Lists store multiple values - perfect for sensor readings:

```python
# Temperature readings over time
temperatures = [22.1, 23.5, 24.2, 23.8, 22.9]

# Lists can contain mixed data types
mixed_list = ['sensor1', 'sensor2', 10, 23.5, True]

# Access data
first_temp = temperatures[0]      # 22.1
last_temp = temperatures[-1]      # 22.9 (negative indexing)
second_last = temperatures[-2]    # 23.8
all_but_first = temperatures[1:]  # [23.5, 24.2, 23.8, 22.9]

# Slice with step (every 3rd element starting from index 0)
every_third = temperatures[0::3]  # [22.1, 23.8]

# Calculate basic stats
average = sum(temperatures) / len(temperatures)
maximum = max(temperatures)
minimum = min(temperatures)
```
#### List Methods

Lists have many built-in methods for data manipulation:

```python
# Add single item
temperatures.append(20)

# Add multiple items
temperatures.extend([10, 12, 24, 16, 20])

# Count occurrences
count_20 = temperatures.count(20)  # How many times 20 appears

# Remove and return last item
last_item = temperatures.pop()

# Copy lists (creates independent copy)
temperatures_backup = temperatures.copy()

# Sort list (modifies original)
temperatures.sort()              # Ascending order
temperatures.sort(reverse=True)  # Descending order

# Get list length
list_length = len(temperatures)

# Sum all numeric values
total = sum(temperatures)
```
### 3. Dictionaries - Structured Data

Dictionaries store related information together using key-value pairs:

```python
# Single sensor reading
sensor_reading = {
    'temperature': 24.3,
    'humidity': 65.8,
    'timestamp': '2024-01-15 14:30:00',
    'sensor_id': 'MULTI_001',
    'status': 'normal'
}

# Access values
temp = sensor_reading['temperature']
status = sensor_reading['status']

# Add new data
sensor_reading['battery'] = 87

# Dictionaries can have various key types and value types
mixed_dict = {
    'key1': [1, 2, 3, 4, 5],      # string key, list value
    10: 'value1',                  # integer key, string value
    True: [12.3, 'value2']         # boolean key, list value
}

# Add new key-value pairs
mixed_dict[20] = 'my_string'

# Access dictionary information
keys = mixed_dict.keys()      # Get all keys
values = mixed_dict.values()  # Get all values
items = mixed_dict.items()    # Get all key-value pairs
```

### 4. Loops for Processing Data

Process multiple data points efficiently:

```python
# Check each temperature
for temp in temperatures:
    if temp > 25:
        print(f"Alert: High temperature {temp}°C")

# Process with position information
for i, temp in enumerate(temperatures):
    print(f"Reading {i+1}: {temp}°C")

# Count conditions
hot_readings = 0
for temp in temperatures:
    if temp > 25:
        hot_readings += 1
```

### 5. Functions for Reusable Code

Create functions to avoid repeating code:

```python
def analyze_temperatures(temp_list):
    """Calculate basic temperature statistics"""
    if not temp_list:  # Check for empty list
        return None
    
    stats = {
        'average': sum(temp_list) / len(temp_list),
        'maximum': max(temp_list),
        'minimum': min(temp_list),
        'count': len(temp_list)
    }
    return stats

# Use the function
temp_stats = analyze_temperatures(temperatures)
print(f"Average: {temp_stats['average']:.1f}°C")
```

### 6. Error Handling

Handle problems gracefully:

```python
def safe_average(numbers):
    """Calculate average with error handling"""
    try:
        if len(numbers) == 0:
            return None
        return sum(numbers) / len(numbers)
    except TypeError:
        print("Error: Invalid data type")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None
```

---

## Assignment: Python Fundamentals Practice

### What to Submit
Create a Jupyter notebook named `your_name_python_fundamentals.ipynb` with the following sections:

### Part 1: Sensor Data Management

Create variables and data structures for a temperature monitoring system:

1. **Variables**:
   - Create variables for: sensor name, current temperature, humidity percentage, and operational status (True/False)

2. **Temperature List**:
   - Create a list with 10 temperature readings between 18-28°C
   - Print the first, last, and middle readings
   - Calculate and print the average temperature

3. **Sensor Dictionary**:
   - Create a dictionary with keys: 'sensor_id', 'location', 'temperature', 'humidity', 'last_maintenance'
   - Add a new key 'battery_level' with value 85
   - Print all keys and values

### Part 2: Data Processing

1. **Temperature Classification**:
   - Write a loop that classifies each temperature as:
     - "Cold" (below 20°C)
     - "Normal" (20-25°C) 
     - "Warm" (above 25°C)
   - Count how many readings fall into each category

2. **Alert System**:
   - Create a list of sensor readings (mix of numbers and some text like "error", "N/A")
   - Write code that:
     - Filters out invalid readings
     - Identifies readings outside normal range (18-26°C)
     - Counts total valid readings vs invalid readings

### Part 3: Functions

1. **Statistics Function**:
   - Write a function `calculate_stats(data_list)` that returns a dictionary with:
     - count, average, minimum, maximum
   - Test it with your temperature data

2. **Validation Function**:
   - Write a function `validate_reading(value, min_val, max_val)` that:
     - Returns True if value is within range
     - Returns False otherwise
     - Handles the case where value is not a number

### Part 4: Error Handling

1. **Robust Processing**:
   - Create a list with mixed data: `[23.5, "error", 25.1, None, 22.8, "maintenance", 24.3]`
   - Write code that safely processes this list to:
     - Extract only valid numeric readings
     - Count how many invalid entries were found
     - Calculate statistics on the valid data only

### Submission Requirements

- **Code Quality**: Include comments explaining what each section does
- **Output**: Show the results of all calculations and classifications
- **Testing**: Demonstrate that your functions work with different inputs

### Grading Criteria

- **Correctness** (65%): Code works as specified
- **Code Quality** (35%): Clean, readable code with comments

### Tips for Success

1. **Start Simple**: Get basic functionality working before adding complexity
2. **Test Frequently**: Run your code often to catch errors early
3. **Use Print Statements**: Help yourself debug by printing intermediate results
4. **Read Error Messages**: They usually tell you exactly what's wrong
5. **Ask for Help**: If stuck for more than 10 minutes, ask questions!

