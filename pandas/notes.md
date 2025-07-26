# Pandas Notes: Series

> A **Series** is the foundational 1D data structure in Pandas.  
> It’s like a smarter, labeled NumPy array—ideal for fast data analysis.

---

## Introduction

- A **Series** is a one-dimensional, labeled array capable of holding any data type (integers, strings, floats, etc.).
- Unlike NumPy arrays, Series have explicit labels (**indexes**), which makes data manipulation and labeling easier.

---

## Importing Pandas

Always import Pandas with the standard alias:

    import pandas as pd

---

## Creating a Series

- **From a list (default integer index):**

    s = pd.Series([10, 20, 30, 40])

- **With a custom index:**

    s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])

---

## Indexing and Selection

Access elements just like with lists, but indexes add flexibility.

### Position-based (`iloc`)

- Use `iloc` to select by numeric position:

    s.iloc[0]       # first item (by position)  
    s.iloc[1:3]     # slice by position, returns 2nd and 3rd elements

### Label-based (`loc`)

- Use `loc` to select by index label:

    s.loc['b']         # selects the value at index 'b'  
    s.loc['b':'d']     # selects all items from 'b' through 'd' (inclusive)

### Direct Access (Shortcut)

    s['c']             # works if index is string or integer

---

## Working with Index & Names

- **View all index labels:**

    s.index            # Index(['a', 'b', 'c', 'd'], dtype='object')

- **Name your Series:**  
  Naming helps label data in outputs and plots.

    s.name = "Quarterly Revenue"  
    print(s.name)      # Outputs: 'Quarterly Revenue'

---

## Modifying Values

- **Single value modification (by label or position):**

    s['a'] = 99  
    s.iloc[1] = 77

- **Modify multiple values at once:**

    s[['b', 'd']] = 50

---

## Boolean Filtering

Filter a Series by a condition; it returns only elements where the condition is `True`.

    mask = s > 50  
    filtered = s[mask]     # All values in s greater than 50

Or simply:

    filtered = s[s > 50]

---

## 💡 Pro Tips & Best Practices for SERIES

- Pandas Series are **built on top of NumPy arrays**, so many NumPy functions work directly on Series.
- Use `iloc` for **position-based** indexing, and `loc` for **label-based** indexing—do not mix them up.
- Naming your Series (`s.name`) makes analysis and visualization outputs clearer.
- Label-based slicing with `loc` is **inclusive** of the end label (e.g., `s.loc['b':'d']` includes `'d'`).
- Boolean filtering enables **fast, vectorized data extraction** without explicit loops.


