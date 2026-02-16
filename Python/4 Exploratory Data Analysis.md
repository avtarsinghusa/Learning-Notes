# Exploratory Data Analysis Techniques -- Week 3
* When we know what kind of values to consider as anomalies in the data, We can do the replacement of **missing** and **inf** to NaN while loading the data.
```
data = pd.read_csv('/content/drive/MyDrive/Melbourne_Housing.csv',na_values=['missing','inf'])

# Checking for missing values in the data
data.isnull().sum()

# Checking for duplicate entries in the data
data.duplicated().sum()

# dropping duplicate entries from the data
data.drop_duplicates(inplace=True)

# resetting the index of data frame since some rows will be removed
data.reset_index(drop=True,inplace=True)

# This forces pandas to analyze all columns, regardless of their data type (numerical, categorical/object, datetime, etc.).
df.describe(include='all').T
```
* **unique()** -- method returns an array of the actual unique values found in the Series, in the order they first appeared.
* **nunique()** -- method returns the count of unique values in the Series.
```
import pandas as pd

# Creating a Series with repeating values
data = pd.Series(['Apple', 'Banana', 'Apple', 'Orange', 'Banana', 'Banana'])

# Get the actual unique values
unique_values = data.unique()

# Get the count of unique values
count_unique = data.nunique()

print("Unique Values:", unique_values)
print("Count of Unique Values:", count_unique)

# Output--
# Unique Values: ['Apple' 'Banana' 'Orange']
# Count of Unique Values: 3
```


### Univariate Analysis
* Univariate analysis is the simplest form of analyzing data. It focuses on **one variable at a time** to describe its distribution, central tendency, and spread (variability).
Here is the explanation with a concrete example.
Example Scenario
Imagine you have a dataset of 100 students and their scores on a recent math test (ranging from 0 to 100). The variable we are analyzing is **`Score`**.

#### 1. Assessing Central Tendency (Where is the middle?)
Central tendency measures tell us where the bulk of the data lies.
* **Mean (Average):** The sum of all scores divided by the number of students.
* **Median:** The exact middle score when all scores are listed in order.
* **Mode:** The score that appears most frequently.
  * **Example:** If the mean score is **75**, it gives us a quick snapshot of how the class performed overall.

#### 2. Assessing Variability (How spread out is the data?)
Variability measures tell us how different the scores are from each other and from the mean.
* **Range:** The difference between the highest and lowest score.
* **Standard Deviation:** A measure of how much, on average, each score differs from the mean.
* **Interquartile Range (IQR):** The range of the middle 50% of the data.
  * **Example:**
  * **Case A:** The scores are 70, 75, 80. The **mean is 75**, and the **variability is low**.
  * **Case B:** The scores are 40, 75, 100. The **mean is still 75**, but the **variability is very high**.
  
### Summary Table

| Metric | What it tells you | Example in "Scores" context |
| --- | --- | --- |
| **Mean** | The average value | "The average score was 75." |
| **Median** | The middle value | "Half the students scored above 78." |
| **Range** | Total spread | "Scores ranged from 40 to 100." |
| **Std Dev** | Average distance from mean | "Scores differed from the average by  points." |

* The **visualization method used** for Univariate Analysis are Histogram, Boxplot, Bargraph.  

### Next Step

Would you like me to show you the Python code using **pandas** to calculate these exact metrics for a sample dataset?
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
