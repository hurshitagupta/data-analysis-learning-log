# Matplotlib Notes

## 1. Introduction

- Matplotlib is Python’s main library for data visualization.
- Commonly used with `matplotlib.pyplot` as `plt`.

## 2. Installation

~~~bash
!pip install matplotlib
~~~

## 3. Importing

~~~python
import matplotlib.pyplot as plt
~~~

## 4. Core Plotting Functions

| Plot Type      | Function Example                   |
|----------------|----------------------------------|
| Line Plot      | `plt.plot(x, y)`                  |
| Bar Chart      | `plt.bar(x, y)`                   |
| Scatter Plot   | `plt.scatter(x, y)`               |
| Histogram      | `plt.hist(data)`                  |
| Pie Chart      | `plt.pie(sizes, labels=labels)`  |

## 5. Basic Plot Example

~~~python
x = [1, 2, 3, 4]
y = [10, 20, 15, 25]

plt.plot(x, y)
plt.xlabel('x-axis')
plt.ylabel('y-axis')
plt.title('Sample Line Plot')
plt.show()
~~~

## 6. Customization

- Color: `plt.plot(x, y, color='red')`
- Marker: `plt.plot(x, y, marker='o')`
- Line Style: `plt.plot(x, y, linestyle='--')`
- Legend:

  ~~~python
  plt.plot(x, y, label='Data')
  plt.legend()
  ~~~

- Grid: `plt.grid(True)`

## 7. Multiple Plots on Same Figure

~~~python
plt.plot(x1, y1, label='Series 1')
plt.plot(x2, y2, label='Series 2')
plt.legend()
plt.show()
~~~

## 8. Subplots

~~~python
fig, ax = plt.subplots(2, 1)  # 2 rows, 1 column
ax[0].plot(x, y1)
ax[1].plot(x, y2)
plt.show()
~~~

## 9. Plot Styling

- Themes/Styles: `plt.style.use('ggplot')`
- Figure Size: `plt.figure(figsize=(8,4))`

## 10. Saving Figures

~~~python
plt.savefig('filename.png')
~~~

## 11. Interactive Mode (Jupyter)

~~~ipython
%matplotlib inline
~~~

## 12. Useful Tips

- Explore colormaps: `plt.cm`
- Axes control: `plt.axis()`, `plt.xlim()`, `plt.ylim()`
- Annotate: `plt.annotate('text', xy=(x, y))`
