# Numpy Notes 

This document summarizes the essential concepts, methods, and practical patterns of Numpy as introduced in the FCC Data Analysis course. These notes are designed for quick reference, revision, and future upskilling.

---

## What is Numpy?

- **Numpy** is a foundational Python library for numerical computing.
- Its core offering is the **n-dimensional array object (`ndarray`)**, which enables fast, vectorized computations.

---

## Key Concepts

### 1. Importing Numpy

import numpy as np    # Standard import alias used throughout the Python ecosystem

---

### 2. Creating Arrays

1. Create a 1D array from a list

    arr1 = np.array([1,2,3,4])

2. Create a 2D array (matrix) from a list of lists

    arr2 = np.array([[1,2][3,4])

3. Arrays of zeros and ones (shape: rows x columns)

    zeros = np.zeros((2, 3))   # 2 rows, 3 columns filled with 0

    ones = np.ones((3,))       # 1D array of three ones

4. Sequential data: Range and evenly spaced values

    range_arr = np.arange(0, 10, 2)      # Start: 0, Stop: 10 (exclusive), Step: 2

---

### 3. Array Attributes & Types

- `arr1.shape`    — Shape of the array, e.g., (4,)
- `arr2.dtype`    — Data type of the array elements, e.g., int64, float64
- `arr2.size`     — Total number of elements
- `arr2.ndim`     — Number of dimensions (1 for vector, 2 for matrix)

Example:

print(arr1.shape)

print(arr2.dtype)

print(arr2.size)

print(arr2.ndim)

---

### 4. Indexing & Slicing

#### A. Slicing 1D arrays:
    
  - print(arr1[1:3])         # Elements at indices 1 and 2 (excluding 3)

  - print(arr1[-1])          # Last element

#### B. For 2D arrays (matrices):
  
  - print(arr2[0,)           # Element at first row, second column

  - print(arr2[:, 0])        # All rows, first column

---

### 5. Changing Shape

reshaped = arr1.reshape((2, 2))       # Reshape 1D array to 2x2 matrix

flattened = arr2.flatten()            # Flatten 2D matrix to 1D array

---

### 6. Mathematical Operations

#### Arithmetic operations are vectorized and applied elementwise.

  - add = arr1 + 5         # Add 5 to each element in arr1

  - subtract = arr2 - 1    # Subtract 1 from each element in arr2

  - multiply = arr1 * 2    # Multiply each element of arr1 by 2

  - divide = arr1 / 1.5    # Divide each element of arr1 by 1.5

#### Element wise operations with arrays of compatible shape (Broadcasting)
  - arr3 = arr1 + np.array([10,10,10,10])

### 7. Aggregations & Statistics

Common aggregation methods:

  - print(arr1.sum())         # Sum of all elements

  - print(arr1.mean())        # Arithmetic mean (average)

  - print(arr2.max())         # Maximum value

  - print(arr2.min())         # Minimum value

  - print(arr1.std())         # Standard deviation

### 8. Boolean Indexing / Filtering
You can filter arrays based on conditions:

mask = arr1 > 2          # Boolean mask: array of True/False

filtered = arr1[mask]    # Elements of arr1 where condition is True

#### Equivalent short form:
filtered = arr1[arr1 > 2]

### 9. Copy vs. View
arr.copy() creates a new, independent copy.

Simple assignment only creates a reference (view), meaning changes affect both variables.

#### Example:

arr1_copy = arr1.copy()

arr1_copy = 100              # Does not change arr1

arr1_view = arr1

arr1_view[1] = 200           # Changes arr1 as well


### Essential Numpy Tips
  - Always use import numpy as np for consistency and readability.

  - Master indexing and slicing—they are powerful tools to manipulate data.

  - Avoid Python loops for elementwise operations: use native Numpy vectorized operations for performance.

  - Refer to the official Numpy documentation for deeper learning.