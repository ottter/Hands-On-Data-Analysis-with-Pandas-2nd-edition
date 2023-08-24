# James Cross - Assignment 03 Task 01

## Setup

## 1 - Wide vs Long

```python
wide_df.head(6)

wide_df.describe(include='all', datetime_is_numeric=True)

long_df.head(6)

long_df.describe(include='all', datetime_is_numeric=True)
```

```python
wide_df.plot(
    x='date', y=['TMAX', 'TMIN', 'TOBS'], figsize=(15, 5), 
    title='Temperature in NYC in October 2018'
).set_ylabel('Temperature in Celsius')
plt.show()
```

```python
import seaborn as sns

sns.set(rc={'figure.figsize': (15, 5)}, style='white')

ax = sns.lineplot(
    data=long_df, x='date', y='value', hue='datatype'
)
ax.set_ylabel('Temperature in Celsius')
ax.set_title('Temperature in NYC in October 2018')
plt.show()
```

```python
sns.set(
    rc={'figure.figsize': (20, 10)}, style='white', font_scale=2
)

g = sns.FacetGrid(long_df, col='datatype', height=10)
g = g.map(plt.plot, 'date', 'value')
g.set_titles(size=25)
g.set_xticklabels(rotation=45)
plt.show()
```

## 2 - Cleaning Data

```python
response = make_request('datasets', {'startdate': '2018-10-01'})

response.status_code
response.ok
```

```python
payload = response.json()
payload.keys()

payload['metadata']

payload['results'][0].keys()

[(data['id'], data['name']) for data in payload['results']]
```

```python
# get data category id
response = make_request(
    'datacategories', payload={'datasetid': 'GHCND'}
)
response.status_code

response.json()['results']
```

```python
# get data type id
response = make_request(
    'datatypes',
    payload={
        'datacategoryid': 'TEMP', 
        'limit': 100
    }
)
response.status_code

[(datatype['id'], datatype['name']) for datatype in response.json()['results']][-5:] # look at the last 5
```

## 3 - Cleaning Data

## 4 - Reshaping Data

## 5 - Handling Data Issues
