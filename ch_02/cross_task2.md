# James Cross - Assignment 02 Task 2

## Pre. Setting up

`cross_task2exercises.ipynb` shows the commands used to create `parsed_place` from the chapter.

---

## 1. Find the 95th percentile of earthquake magnitude in Japan using the mb magnitude type

Only used data that matches `parsed_place == Japan` and `magType == mb`. From that data, take the `mag` column and use the `quantile` option to find 0.95.

```python
df[(df.parsed_place == 'Japan') 
    & (df.magType =='mb')].mag.quantile(0.95)
```

`...mag.describe(percentiles=[0.95])` can also be used to find the same data.

### Output

```python
4.9
```

---

## 2. Find the percentage of earthquakes in Indonesia that were coupled with tsunamis

Find the number of Indonesia + Tsunami earthquakes, divifed by number of Indonesia earthquakes

```python
per = (df[(df['parsed_place'] == 'Indonesia') 
    & (df['tsunami'] == True)].shape[0] 
 / df[df['parsed_place'] == 'Indonesia'].shape[0])
f"{per:.2%}"
```

### Output

```python
'23.13%'
```

---

## 3. Calculate summary statistics for earthquakes in Nevada

`describe` gives summary info of columns

```python
df[df.parsed_place == 'Nevada'].describe(include='all')
```

### Output

```python
# Theres a lot of stuff here, its in the .ipynb
```

---

## 4. Add a column indicating whether the earthquake happened in a country or US state that is on the Ring of Fire

### Use Alaska, Antarctica (look for Antarctic), Bolivia, California, Canada, Chile, Costa Rica, Ecuador, Fiji, Guatemala, Indonesia, Japan, Kermadec Islands, Mexico (be careful not to select New Mexico), New Zealand, Peru, Philippines, Russia, Taiwan, Tonga, and Washington

```python
ring_of_fire =  ['Alaska', 'Antarctic', 'Bolivia', 'California', 'Canada', 'Chile', 'Costa Rica', 
'Ecuador', 'Fiji', 'Guatemala', 'Indonesia', 'Japan', 'Kermadec Islands', '(?<!New\s)Mexico', 
'New Zealand', 'Peru', 'Philippines', 'Russia', 'Taiwan', 'Tonga', 'Washington']

df['ring_of_fire'] = df.parsed_place.str.contains(r'|'.join(ring_of_fire), case=False, regex=True)

df.ring_of_fire.value_counts()
```

### Output

```python
True     7188
False    2144
Name: ring_of_fire, dtype: int64
```

---

## 5. Calculate the number of earthquakes in the Ring of Fire locations and the number outside of them

Booleans are 1 for True and 0 for False, so getting a sum works

```python
print(f"inside of RoF: {df['ring_of_fire'].sum()}")
print(f"outside of RoF: {len(df) - df['ring_of_fire'].sum()}")
```

This is probably the smarter way :)

```python
df.ring_of_fire.value_counts()
```

### Output

```python
inside of RoF: 7188
outside of RoF: 2144

True     7188
False    2144
Name: ring_of_fire, dtype: int64
```

---

## 6. Find the tsunami count along the Ring of Fire

```python
df[df['ring_of_fire'] & df['tsunami']].shape[0]
```

### Output

```python
45
```
