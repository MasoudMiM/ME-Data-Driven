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

# Text for labels and categories
sensor_id = "TEMP_001"      # string
status = "active"           # string

# True/False for conditions
is_working = True           # boolean
```

### 2. Lists - Your Data Collections

Lists store multiple values - perfect for sensor readings:

```python
# Temperature readings over time
temperatures = [22.1, 23.5, 24.2, 23.8, 22.9]

# Access data
first_temp = temperatures[0]      # 22.1
last_temp = temperatures[-1]      # 22.9
all_but_first = temperatures[1:]  # [23.5, 24.2, 23.8, 22.9]

# Add new data
temperatures.append(24.1)

# Calculate basic stats
average = sum(temperatures) / len(temperatures)
maximum = max(temperatures)
minimum = min(temperatures)
```

### 3. Dictionaries - Structured Data

Dictionaries store related information together:

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
sensor_reading['battery'] = 87  # Add new data
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

