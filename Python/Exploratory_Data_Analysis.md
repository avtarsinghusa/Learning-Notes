# Exploratory Data Analysis Techniques
* When we know what kind of values to consider as anomalies in the data, We can do the replacement of **missing** and **inf** to NaN while loading the data.
```
data = pd.read_csv('/content/drive/MyDrive/Melbourne_Housing.csv',na_values=['missing','inf'])

# **Checking for missing values in the data**
data.isnull().sum()

# Checking for duplicate entries in the data
data.duplicated().sum()

# dropping duplicate entries from the data
data.drop_duplicates(inplace=True)

# resetting the index of data frame since some rows will be removed
data.reset_index(drop=True,inplace=True)
```
### Univariate Analysis

### Bivariate / Mulitvariate Analysis
* Pandas Series is a one-dimensional **labeled array/list** capable of holding data of any type (integer, string, float, python objects, etc.).
* The labels are collectively called index.
* Pandas Series can be thought as a single column of an excel spreadsheet and each entry in a series corresponds to an individual row in the spreadsheet.
```
# importing the libraries
import numpy as np
import pandas as pd

# creating a list of price of different medicines
med_price_list = [55,25,75,40,90]

# converting the list into a Pandas Series object
series_list = pd.Series(med_price_list)

0    55
1    25
2    75
3    40
4    90
```
* We can see that the list and array have been converted to a Pandas Series object.
* We also see that the series has automatically got index labels. Let's see how these can be modified.
```
