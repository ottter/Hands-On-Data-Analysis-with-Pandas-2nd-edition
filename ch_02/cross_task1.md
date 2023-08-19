# James Cross - Assignment 02 Task 1

## Pandas Data Structures

---
Data can be read by NumPy in multiple different formats, in this example it is a csv file.

```python
import numpy as np

data = np.genfromtxt(
    'data/example_data.csv', delimiter=';', 
    names=True, dtype=None, encoding='UTF'
)
data
```

---
This is a way to display the dimensions of the data, displayed as a tuple. A tuple is immutable, meaning it can not be changed.

```python
data.shape
```

---
`dtype` is a way to provide the data type. Because it is a tuple, it will give the data type of each along with the name given by the csv. Numpy arrays can only be a single data type, but the way this is more of a structured array which allows multiple types.

```python
data.dtype
```

---
This will measure the time it takes to execute finding the maximum value of the fourth entry of each row in data, in this case the 'mag' value.

```python
%%timeit
max([row[3] for row in data])
```

---

This creates a dictionary ({key: value}) of the name of the data along with the value

```python
array_dict = {
    col: np.array([row[i] for row in data])
    for i, col in enumerate(data.dtype.names)
}
array_dict
```

---

Calculate the time to calculate the same as the previous nax of mag. This results in a quicker result on average.

```python
%%timeit
array_dict['mag'].max()
```

---

This creates an array from the dict created earlier of just the maximum mag value entry.

```python
np.array([
    value[array_dict['mag'].argmax()] 
    for key, value in array_dict.items()
])
```

---

Create a series named "place"

```python
import pandas as pd

place = pd.Series(array_dict['place'], name='place')
place
```

---

Give the name of the series, 'place'

```python
place.name
```

---

Give the data type of place, 'O' (for object)

```python
place.dtype
```

---

The shape is still (5,) because the series was made on the original data strcture, but with the 'place' name

```python
place.shape
```

---

Output the values of place series

```python
place.values
```

---

Another way to get the number of values in the series.

```python
place_index = place.index
place_index
```

---

This gets the array of the number of values

```python
place_index.values
```

---

... and also the data type, which was also provided by place.values

```python
place_index.dtype
```

---

... and the shape of the series, showing it is still (5,)

```python
place_index.shape
```

---

Check if the values are unique

```python
place_index.is_unique
```

---

It is possible to do math with arrays of equal size

```python
np.array([1, 1, 1]) + np.array([-1, 0, 1])
```

---

since `y` is iven a custom index, `x[0]` has nothing to add to, and neither does `y[5]` so they result in `NaN`

```python
numbers = np.linspace(0, 10, num=5) # makes numpy array([0, 2.5, 5, 7.5, 10])
x = pd.Series(numbers) # index is [0, 1, 2, 3, 4]
y = pd.Series(numbers, index=pd.Index([1, 2, 3, 4, 5]))
x + y
```

---

Create a dataframe

```python
df = pd.DataFrame(array_dict) 
df
```

---

list the data types of each data entry, which are a mix of objects, floats, and ints

```python
df.dtypes
```

---

give the values of the entries. this only contains the values, not the names of them

```python
df.values
```

---

give the names of the data points which correspond to `df.values`

```python
df.columns
```

---

find the rows and columns of the dataframe

```python
df.shape
```

---

dataframes can be added together, but the data type  determines if they are appended or *actually* added (or subtracted, multiplied, etc)

```python
df + df
```

---

## Creating DataFrames

I'm going to merge a lot of these code snippets together and add comments to make it a bit more concise than above.

```python

```

---

## Making Dataframes from API


---

## Inspecting Dataframe


---

## Subsetting Data


---

## Adding and REmoving Data


---
