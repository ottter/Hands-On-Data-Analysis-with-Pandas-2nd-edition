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

I have added descriptive code comments to describe what is being done in each exercise, which are included in the attached file.
