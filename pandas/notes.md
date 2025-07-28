# 📊 Pandas Notes

## 1. Series

> A **Series** is the foundational 1D data structure in Pandas.  
> It’s like a smarter, labeled NumPy array—ideal for fast data analysis.

### Introduction

- A **Series** is a one-dimensional, labeled array capable of holding any data type (integers, strings, floats, etc.).
- Unlike NumPy arrays, Series have explicit labels (**indexes**), enabling intuitive data manipulation and referencing.

### Importing Pandas

Always import Pandas with the standard alias:

    import pandas as pd

### Creating a Series

- **From a list (with default integer index):**

    s = pd.Series([10, 20, 30, 40])

- **With a custom index:**

    s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])

### Indexing and Selection

Access elements like lists, but thanks to labels, Series offer more flexibility!

- **Position-based selection (`iloc`):**

      s.iloc[0]       # First item by position  
      s.iloc[1:3]     # Slice by position: 2nd and 3rd elements

- **Label-based selection (`loc`):**

      s.loc['b']         # Value at index label 'b'  
      s.loc['b':'d']     # Slice from 'b' to 'd' (inclusive)

- **Direct index access shortcut:**

      s['c']             # Works if index is str or int

### Working with Index and Names

- **View index labels:**

      s.index            # e.g. Index(['a', 'b', 'c', 'd'], dtype='object')

- **Name your Series:**  
  Helps with labeling outputs and plots.

      s.name = "Quarterly Revenue"  
      print(s.name)      # Outputs: 'Quarterly Revenue'

### Modifying Values

- **Modify single value (by label or position):**

      s['a'] = 99  
      s.iloc[1] = 77

- **Modify multiple values at once:**

      s[['b', 'd']] = 50

### Boolean Filtering

Return elements satisfying conditions quickly:

    mask = s > 50  
    filtered = s[mask]     # All values in s > 50

Or simply:

    filtered = s[s > 50]

### Pro Tips & Best Practices for Series

- Series are built on **NumPy arrays**, so NumPy functions usually apply.
- Use `iloc` for **position-based** and `loc` for **label-based** indexing.
- Naming your Series (`.name`) improves clarity in outputs.
- Label-based slicing with `loc` **includes** the end label.
- Boolean filtering offers fast, vectorized data operations without loops.

---

## 2. DataFrame

> A **DataFrame** is a 2D, tabular data structure with labeled rows and columns.  
> Think of it as a spreadsheet in Python—perfect for flexible and powerful data analysis.

### Introduction

- Central data structure in Pandas.
- Stores heterogeneous, labeled tabular data.
- Each column can have different data types.

### Importing Pandas

    import pandas as pd

### Creating a DataFrame

- **From a dictionary of lists:**

      data = {
          'Name': ['Alice', 'Bob', 'Charlie'],
          'Age': [23, 31, 27],
          'City': ['New York', 'Paris', 'Berlin']
      }
      df = pd.DataFrame(data)

- **From a list of dictionaries:**

      records = [
          {'Name': 'Alice', 'Age': 23, 'City': 'New York'},
          {'Name': 'Bob', 'Age': 31, 'City': 'Paris'},
          {'Name': 'Charlie', 'Age': 27, 'City': 'Berlin'}
      ]
      df = pd.DataFrame(records)

- **Create an empty DataFrame:**

      df_empty = pd.DataFrame()

### Viewing Data in a DataFrame

- Preview rows:

      df.head()      # First 5 rows  
      df.head(3)     # First 3 rows  
      df.tail()      # Last 5 rows

- Inspect shape and structure:

      df.shape       # Tuple (rows, columns)  
      df.columns     # List of columns  
      df.index       # List of index labels  
      df.info()      # Data summary (data types, null counts)  
      df.describe()  # Summary stats on numeric columns

### Selecting Data

- **Select a column (returns Series):**

      df['Age']

- **Select multiple columns (returns DataFrame):**

      df[['Name', 'City']]

- **Select rows by integer position (`iloc`):**

      df.iloc[0]        # First row  
      df.iloc[1:3]      # Rows 2 and 3 (0-based indexing)

- **Select rows by label (`loc`):**

      df.loc[0]         # Row with label/index 0  
      df.loc[0:2]       # Rows with labels 0, 1, and 2 inclusive

### Modifying DataFrames

- Add a column:

      df['Age in 5 Years'] = df['Age'] + 5

- Modify a column (example: uppercase cities):

      df['City'] = df['City'].str.upper()

- Remove a column:

      del df['Age in 5 Years']  
      # or  
      df.drop('Age in 5 Years', axis=1, inplace=True)

- Add a new row (using loc for the next index):

      df.loc[len(df)] = ['Dan', 29, 'Madrid']

### Basic Statistical Methods

    df['Age'].mean()    # Average age  
    df['Age'].max()     # Max age  
    df['Age'].min()     # Min age  
    df['Age'].sum()     # Total  
    df['Age'].std()     # Standard deviation

### Conditional Selection (Boolean Filtering)

- Filter rows for age >= 30:

      adults = df[df['Age'] >= 30]

- Multiple conditions (remember parentheses):

      subset = df[(df['Age'] > 25) & (df['City'] == 'PARIS')]

### Pro Tips for DataFrames

- Use `.copy()` when creating slices to avoid overwriting warnings.
- Regularly check your DataFrame using `.head()` after changes.
- Remember:  
  - `iloc` = position-based integer indexing  
  - `loc` = label-based indexing
- Boolean filtering avoids slow loops and accelerates your code.

# 3. Missing Data 

> Handling missing (null/NaN) values is a core data cleaning task in real-world data analysis.
> Pandas provides powerful, easy-to-use tools to detect, remove, or fill missing data.

---

## Introduction

- Real datasets often have missing or corrupt values (represented as `NaN`, `None`, or `NULL`).
- Pandas treats missing data as `NaN` (Not a Number), which is a float type.

---

## Detecting Missing Data

- **Detect missing values in DataFrame or Series:**

      df.isnull()         # Returns DataFrame of True/False for each cell
      df.notnull()        # Opposite of isnull()

- **Count missing values per column:**

      df.isnull().sum()

---

## Removing Missing Data

- **Drop rows with any missing values:**

      df_clean = df.dropna()

- **Drop columns with any missing values:**

      df_clean = df.dropna(axis=1)

- **Drop rows only if all values are missing:**

      df_clean = df.dropna(how='all')

- **Drop rows if too many values are missing (threshold):**

      df_clean = df.dropna(thresh=2)   # Keep rows with at least 2 non-NaN

- **Option to modify DataFrame in place:**

      df.dropna(inplace=True)

---

## Filling (Imputing) Missing Data

- **Fill missing values with a constant:**

      df_filled = df.fillna(0)         # Replace all NaNs with 0

- **Fill using forward-fill (propagate last valid):**

      df_ffill = df.fillna(method='ffill')   # Copy down previous value

- **Fill using backward-fill:**

      df_bfill = df.fillna(method='bfill')   # Copy up next value

- **Fill with the mean, median, or another computation:**

      df['col'] = df['col'].fillna(df['col'].mean())
      df['col'] = df['col'].fillna(df['col'].median())

- **Update in place:**

      df['col'].fillna(0, inplace=True)

---

## Replacing Specific Values

- Replace certain values (e.g., -99 or 'unknown') with NaN before cleaning:

      import numpy as np
      df.replace(-99, np.nan, inplace=True)
      df.replace('unknown', np.nan, inplace=True)

---

## Checking the Effect

- After handling missing data, always verify:

      df.info()
      df.isnull().sum()    # Confirm all missing values handled

---

## Pro Tips

- Always inspect data with `df.head()` and `df.info()` before and after cleaning.
- For most real analyses, fill strategy depends on context: only use mean/median etc. if justified.
- Dropping missing data can lead to data loss; document your workflow and choices.

---





