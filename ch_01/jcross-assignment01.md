# James Cross - Assignment 01

---

## Task 1 - Settings up the environment

I already had Anaconda installed on my system, so I just ended up having to create a new environment to use for this class with the reccomended library version installs. I named my environment `msit` instead of `book_env` because I will want to reuse this in later courses and it was easier this way. I am also running all of this in VSC using Jupyter Notebook plugins.

```conda
(msit) C:\Users\James>conda --version
conda 4.12.0

(msit) C:\Users\James>python --version
Python 3.8.17
```

## Task 2 - Downloading the assignments

I will be using WSL (where I can) or command prompt (where I have to) to complete tasks outside of Jupyter Notebook. I am using the conda plugin `m2-base` to have some increased Linux functionality within the cmd prompt.

```terminal
cd \Users\James\Desktop\Masters\6720 - Prog for Data Science\
git clone https://github.com/stefmolin/Hands-On-Data-Analysis-with-Pandas-2nd-edition.git
```

I did end up copying this over into my own GitHub repository so I can more easily store it on git and swap between my desktop and laptop. This can be found at [ottter/Hands-On-Data-Analysis-with-Pandas-2nd-edition](https://github.com/ottter/Hands-On-Data-Analysis-with-Pandas-2nd-edition)

## Task 3 - Checking my environment

The actual notebook file will also be provided with my submission. I am going to be using markdown to create the writeups and then use another tool to convert that to a pdf.

```python
from check_environment import run_checks
run_checks()
```

```python
Using Python in C:\Users\James\anaconda3\envs\msit:
[ OK ] Python is version 3.8.17 (default, Jul  5 2023, 20:44:21) [MSC v.1916 64 bit (AMD64)]

[ OK ] graphviz
[ OK ] imblearn
[ OK ] ipympl
[ OK ] jupyterlab
[ OK ] matplotlib
[ OK ] numpy
[ OK ] pandas
[ OK ] requests
[ OK ] sklearn
[ OK ] scipy
[ OK ] seaborn
[ OK ] sqlalchemy
[ OK ] statsmodels
[ OK ] wheel
[ OK ] login_attempt_simulator
[ OK ] ml_utils
[ OK ] stock_analysis
[ OK ] visual_aids
```

## Task 3 - Exercises

---

### Mean

```py
def as_money(input):
    # Format the input as USD since the input is salaries
    return f"${input:,.2f}"

sal_mean = sum(salaries) / len(salaries)
print(as_money(sal_mean))
```

```py
#output
$585,690.00
```

---

### Median

```py
from statistics import median
# I hope it's okay to use statistics to complete some of these, since it's built-in to Python
# https://docs.python.org/3/library/statistics.html

print(as_money(median(salaries)))
```

```py
#output
$589,000.00
```

---

### Mode

```py
from statistics import mode
# https://docs.python.org/3/library/statistics.html#statistics.mode
print(as_money(mode(salaries)))
```

```py
#output
$477,000.00
```

---

### Sample Variance

```py
from statistics import variance

# Bessel's correction is using n-1 instead of n which is included in statistics.variance
# https://docs.python.org/3/library/statistics.html#statistics.variance
print(variance(salaries))
```

```py
#output
70664054444.44444
```

---

### Sample Standard Deviation

```py
from statistics import stdev
# https://docs.python.org/3/library/statistics.html#statistics.stdev

print(stdev(salaries))
```

```py
#output
265827.11382484
```

---

### Range

```py
sal_range = max(salaries) - min(salaries)
# max = built-in function to find highest number in a list
# min = built-in function to find lowest number in a list
print(sal_range)
```

```py
#output
995000.0
```

---

### Coefficient of Variation

```py
from statistics import mean, stdev
# cv = sample stdev / mean * 100
cv = (stdev(salaries) / mean(salaries)) *100
print(cv)
```

```py
#output
45.38699889443903
```

---

### Interquartile Range

```py
from numpy import percentile
# iqr = q3 (75%) - q1 (25%)
# numpy.percentile is the best way to find the quartiles of a list
iqr = percentile(salaries, 75) - percentile(salaries, 25)
print(iqr)
```

```py
#output
413250.0
```

---

### Quartile Coefficient of Dispersion

```py
from numpy import percentile
# https://www.statisticshowto.com/coefficient-of-dispersion/
# qcd = (q3 - q1) / (q3 + q1)
q1 = percentile(salaries, 25)
q3 = percentile(salaries, 75)
qcd = (q3 - q1) / (q3 + q1)
print(qcd)
```

```py
#output
0.338660110633067
```

---

### Min-Max Scaling

```py
# min-max scaling = sal_scaled
# sal_scaled = (x - min(x)) / range(x) where x = each data point
# this formula will scale the data to the range [0,1] to normalize it

sal_range = max(salaries) - min(salaries)      # get range of salaries
sal_scaled = [(x - min(salaries)) / sal_range for x in salaries]

# I prefer to use list comprehensions. as a regular loop it would look something like:
# sal_list = []
# for x in salaries
#   sal_scaled = (x - min(x)) / range(x)
#   sal_list.append(sal_scaled)

print(sal_scaled[:10])
```

```py
#output
[0.0, 0.01306532663316583, 0.07939698492462312, 0.0814070351758794, 0.08944723618090453, 0.10050251256281408, 0.10854271356783919, 0.18693467336683417, 0.18894472361809045, 0.19095477386934673]
```

---

### Standardizing

```py
from statistics import mean, stdev
# z-score = ( datapoint - (mean of dataset)) / stdev )

sal_mean = mean(salaries)
sal_stdev = stdev(salaries)
z_score = [(x - sal_mean) / sal_stdev for x in salaries]
# similar to min-max scaling, this list comp as a loop looks something like:
# z_score = []
# for x in salaries
#     score = (x - sal_mean) / sal_stdev
#     z_score.append(score)

print(z_score[:10])
```

```py
#output
[-2.199512275430514, -2.150608309943509, -1.9023266390094862, -1.8948029520114855, -1.8647082040194827, -1.8233279255304788, -1.7932331775384762, -1.4998093846164489, -1.4922856976184482, -1.4847620106204475]
```

---

### Covariance

```py
from numpy import cov
from statistics import mean

# cov(X, Y) = E[(X - E[X])(Y - E[Y])]
# cov(X, Y) = covariance
# E[X] = expected value of X = sum of all  possible values of X * probability
# covariance of x and y = mean of ((dp - mean of x set)(dp - mean of y set))
# dp = datapoint, I will have to loop through each list
# https://numpy.org/doc/stable/reference/generated/numpy.cov.html

x = sal_scaled      # Min Max Scaling from previous exercise
y = z_score         # Standardization from previous exercise

sal_cov = cov(x, y)
print(f"numpy solution:\n{sal_cov}")

# Since using numpy for everything feels like a cop out, this is (kind of) what it's doing
def covariance(x, y):
    # x_dp and y_dp = datapoints of x and y
    # zip pairs the two lists (x and y) together based on index position
    # note that the lists MUST be equal length
    return mean([(x_dp - mean(x)) * (y_dp - mean(y)) for x_dp, y_dp in zip(x, y)])

print(f"function solution:\n{covariance(x, y)}")
```

```py
#output
numpy solution:
[[ 7.06640544e+10 -6.84572688e+10]
 [-6.84572688e+10  7.06640544e+10]]
function solution:
-67772696100.0
```

---

### Pearson Correlation Coefficient

```py
from statistics import stdev

# p = cov(x, y) / (stdev(x) * stdev(y))

x = sal_scaled
y = z_score
sal_pearson = covariance(x, y) / (stdev(x) * stdev(y))
print(sal_pearson)
```

```py
#output
-0.9590830392173774
```
