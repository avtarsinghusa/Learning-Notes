# Exploratory Data Analysis Techniques -- Week 3
* When we know what kind of values to consider as anomalies in the data, We can do the replacement of **missing** and **inf** to NaN while loading the data.
```
data = pd.read_csv('/content/drive/MyDrive/Melbourne_Housing.csv',na_values=['missing','inf'])

# Checking for missing values i.e null in the data
data.isnull().sum()

# Checking for non null values in the data, identify rows without null values
df.notna().all(axis=1).sum()

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

# Example 2 : Find Unique Values
# Find the unique values of each categorical column (e.g., Sex, Job, Housing, Saving accounts, Checking account, Purpose).
# Store these unique values in a new DataFrame named unique_values_df with columns Column and Unique Values.
import pandas as pd
df = pd.read_csv('data.csv')
columns = ['Sex', 'Job', 'Housing', 'Saving accounts', 'Checking account', 'Purpose']
unique_values = {col: df[col].unique() for col in columns}
unique_values_df = pd.DataFrame(list(unique_values.items()), columns=['Column', 'Unique Values'])
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

### Bivariate / Mulitvariate Analysis
* Bivariate analysis involves the simultaneous analysis of **two variables**.
* Its primary purpose is to determine if there is a **relationship, correlation, or association** between them.
* While univariate analysis tells you what a single variable looks like, bivariate analysis tells you how they interact.

#### Types of Bivariate Analysis
The methods you use depend on the types of data (numerical or categorical) you are comparing.

| Type of Variables           | Purpose                 | Recommended Visualization |

| **Numerical vs. Numerical** | Study correlation/trend | **Scatter Plot** |

| **Numerical vs. Categorical** | Compare means/spread across groups | **Boxplot** or **Violin Plot** |

| **Categorical vs. Categorical** | Study association/proportion | **Stacked Bar Chart** or **Heatmap** |


* Examples
#### 1. Numerical vs. Numerical: Scatter Plot
* **Example:** Analyzing the relationship between a car's **Horsepower** (X) and its **Price** (Y).
* **What to look for:** If points move upward to the right, there is a positive relationship.

#### 2. Numerical vs. Categorical: Boxplot
* **Example:** Comparing the **Price** (numerical) of cars across different **Fuel Types** (categorical: Diesel, Petrol, Electric).
* **What to look for:** Which fuel type has the highest median price, and which has the most variance?

#### 3. Categorical vs. Categorical: Heatmap
* **Example:** Comparing **Car Brand** (categorical) vs. **Body Style** (categorical) to see which brands produce which styles most often.

* The **pd.cut() function** in pandas is used to **bin** continuous numerical data into discrete intervals (categorical data).
* It is perfect for transforming a continuous variable like "Age" or "Price" into categorical groups like "Child", "Teen", "Adult", or "Low", "Medium", "High".

#### How it works
You specify the edges of the bins, and `pd.cut()` assigns each data point to the corresponding bin.

#### Code Example
```
import pandas as pd

# Sample data: Age of people
ages = pd.Series([5, 12, 17, 21, 28, 35, 45, 60, 75])

# Define bin edges: 0-13, 13-19, 19-60, 60+
bins = [0, 13, 19, 60, 100]

# Define labels for the bins
labels = ['Child', 'Teen', 'Adult', 'Senior']

# Use pd.cut to segment the data
age_groups = pd.cut(ages, bins=bins, labels=labels)

print(age_groups)
```

**Output:**
```text
0     Child
1     Child
2      Teen
3     Adult
4     Adult
5     Adult
6     Adult
7    Senior
8    Senior
dtype: category
Categories (4, object): ['Child' < 'Teen' < 'Adult' < 'Senior']
```
#### Key Parameters
* **`x`**: The input array/Series to be binned.
* **`bins`**: Defines the edges of the bins. If an integer is passed, it defines the number of equal-width bins.
* **`labels`**: Specifies labels for the resulting bins.
* **`right`**: Boolean. If `True` (default), intervals include the right edge (e.g., ). If `False`, they include the left edge (e.g., ).

### Missing Value Treatment
**How to treat missing values?**
* One of the commonly used method to deal with the missing values is to impute them with the central tendencies - mean, median, and mode of a column.
 * **`Replacing with mean`**: In this method the missing values are imputed with the mean of the column. Mean gets impacted by the presence of outliers, and in such cases where the column has outliers using this method may lead to erroneous imputations.
 * **`Replacing with median`**: In this method the missing values are imputed with the median of the column. In cases where the column has outliers, median is an appropriate measure of central tendency to deal with the missing values over mean.
 * **`Replacing with mode`**: In this method the missing values are imputed with the mode of the column. **This method is generally preferred with categorical data**.
 * Other methods include k-NN, MICE, SMOTE, deep learning, ...

```
# Lets see the count and the percentage of missing values in each column
# data.shape[0] will give us the number of rows in the dataset
# selecting the instances where missing value is greater than 0
pd.DataFrame({'Count':data.isnull().sum()[data.isnull().sum()>0],'Percentage':(data.isnull().sum()[data.isnull().sum()>0]/data.shape[0])*100})
```
### Fill missing values
* We will use **fillna() function** and transform method of pandas to impute the missing values.
* fillna() Function - The fillna() function is used to fill NaN values using the provide input value.
 * Syntax of fillna(): **data['column'].fillna(value = x)**
* **transform function** - The transform() function works on each value of a DataFrame and allows to execute a specified function on each value.
 * Sytanx of transform function: **data.transform(func = function name)**
 * func - A function to be executed on the values of the DataFrame.

 * **Example 1** : oop through each column in the DataFrame and use fillna() to fill missing values. If the column is **numeric, use the mean**; if it's **categorical, use the mode**. 
```
# 
import pandas as pd
import numpy as np

# 1. Create a sample DataFrame with missing values
data = {
    'Age': [25, np.nan, 30, 22, np.nan],
    'Salary': [50000, 60000, np.nan, 80000, 55000],
    'City': ['New York', 'Los Angeles', np.nan, 'New York', 'Chicago'],
    'Department': ['HR', 'IT', 'IT', np.nan, 'HR']
}
df = pd.DataFrame(data)
print("Original DataFrame:")
print(df)
print("-" * 20)

# 2. Loop through each column and impute
for col in df.columns:
    if df[col].dtype == 'object':
        # Categorical: Use Mode (most frequent value)
        # Note: Mode returns a Series, so we take the first element [0]
        mode_val = df[col].mode()[0]
        df[col].fillna(mode_val, inplace=True)
    else:
        # Numeric: Use Mean
        mean_val = df[col].mean()
        df[col].fillna(mean_val, inplace=True)

print("DataFrame after Imputation:")
print(df)
```
* **Example 2** : Use groupby() and transform() to fill missing values in the 'Credit amount' column using the mean value of the grouped 'Purpose' column.
```
import pandas as pd
df = pd.read_csv('data.csv')
df['Credit amount'] = df['Credit amount'].fillna(value = 
df.groupby(['Purpose'])['Credit amount'].transform('mean'))
------
# This line of code is a powerful way to handle missing data by using **conditional imputation** (also known as Grouped Imputation).
# Instead of replacing missing values in `Credit amount` with the average of the *entire* column,
# it replaces them with the average credit amount for their specific `Purpose` group (e.g., "Car", "Education", "Business").
#  Breakdown of the Code
# df.groupby(['Purpose'])['Credit amount']: This groups the data based on the categorical column Purpose. It selects the Credit amount column to work with within those groups.
# .transform('mean'): This is the key part. It calculates the mean Credit amount for each Purpose group. Unlike .aggregate() or .apply(), which would reduce the number of rows, .transform() calculates the group mean and then maps that mean back to the original row index. Result: A new Series of the same length as the original DataFrame, where every row contains the mean value of its corresponding Purpose group.
# .fillna(value = ...): This takes the original Credit amount column and looks for NaN values. When it finds a NaN, it replaces it with the corresponding value from the Series generated by the .transform('mean') step.
# df['Credit amount'] = ...: This assigns the resulting imputed column back to the original DataFrame.
```
* **Example 3** : Dropping columns where the percentage of null values exceeds 25%
```
df = pd.read_csv('data.csv')
missing_percentage = df.isnull().mean() * 100
columns_to_drop = list(df.columns[missing_percentage > 25])
df = df.drop(columns=columns_to_drop)
# Alternatively, using axis=1
# df = df.drop(columns_to_drop, axis=1)
```
* **Example 4** : Counting Missing Values using isnull and sum
```
missing_counts = df.isnull().sum()
# The variable missing_counts becomes a Pandas Series where:
  Index: The names of your columns.
  Values: The total count of missing values in each corresponding column.
```
* **Example 5** : Handling Null Values in Pandas
```
# Write function to detect missing values. Store the result in a variable named null_records  which is a DataFrame containing only those rows that have null values.
null_records = df[df.isnull().any(axis =1)]

# Breakdown of the Code
# df.isnull():This generates a DataFrame of the same shape as df, filled with True where a cell is missing and False otherwise.
# .any(axis=1): This reduces the DataFrame from the first step into a single Series of True/False values (one for each row).
 axis=1 tells Pandas to look across the columns to check if any value in that row is True.
 If a row has even one missing value (True), the result for that row is True. If all values are present, it is False.
# df[...]: This takes the True/False Series from step 2 and uses it to filter the original DataFrame.
  It keeps only the rows where the corresponding value in the Series is True.
```
### Outlier Detection and Treatment
* Some of the commonly methods to deal with the data points that we actually flag as outliers are:
 * Replacement with null values - We can consider these data points as missing data and replace the abnormal values with NaNs.
 * IQR method - Replace the data points with the lower whisker (Q1 - 1.5 * IQR) or upper whisker (Q3 + 1.5 * IQR) value.
 * We can also drop these observations, but we might end up with losing other relevant observations as well.

**Treating outliers**
* We will cap/clip the minimum and maximum value of these columns to the lower and upper whisker value of the boxplot found using  **Q1 - 1.5*IQR** and **Q3 + 1.5*IQR**, respectively.
* **Note**: Generally, a value of 1.5 * IQR is taken to cap the values of outliers to upper and lower whiskers but any number (example 0.5, 2, 3, etc) other than 1.5 can be chosen. The value depends upon the business problem statement.
```
# to find the 25th percentile and 75th percentile for the numerical columns.
Q1 = data[numeric_columns].quantile(0.25)
Q3 = data[numeric_columns].quantile(0.75)

IQR = Q3 - Q1                   #Inter Quantile Range (75th percentile - 25th percentile)

lower_whisker = Q1 - 1.5*IQR    #Finding lower and upper bounds for all values. All values outside these bounds are outliers
upper_whisker = Q3 + 1.5*IQR
---------------------------------
def treat_outliers(df, col):
    """
    treats outliers in a variable
    col: str, name of the numerical variable
    df: dataframe
    col: name of the column
    """
    Q1 = df[col].quantile(0.25)  # 25th quantile
    Q3 = df[col].quantile(0.75)  # 75th quantile
    IQR = Q3 - Q1                # Inter Quantile Range (75th perentile - 25th percentile)
    lower_whisker = Q1 - 1.5 * IQR
    upper_whisker = Q3 + 1.5 * IQR

    # all the values smaller than lower_whisker will be assigned the value of lower_whisker
    # all the values greater than upper_whisker will be assigned the value of upper_whisker
    # the assignment will be done by using the clip function of NumPy
    df[col] = np.clip(df[col], lower_whisker, upper_whisker)

    return df

outlier_columns = ['Ad Spend','Profit Margin', 'Revenue']
for col in outlier_columns:
    df = treat_outliers(df, col)
-------------
# Another Example
# Identify columns where the percentage of values outside the bounds is greater than 11%, and assign them to a list
import pandas as pd
df = pd.read_csv('data.csv')

for col in df.columns:
    if df[col].dtype != 'object':
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3- Q1
        lower_bound = Q1 - 1.5 * IQR
        upper_bound = Q3 + 1.5 * IQR
        if ((df[col] < lower_bound) | (df[col] > upper_bound)).sum() / df.shape[0] > 0.11:
            outlier_columns.append(col)
#Explanation: You need to calculate the percentage of values outside the bounds for each numerical column and check if it exceeds 11%. If it does, append the column name to the outlier_columns list.
import pandas as pd

# Step 2: Read Dataset
df = pd.read_csv('data.csv')

# Step 3: Calculate Q1 and Q3
# We select numeric columns first to avoid errors with text columns
numeric_df = df.select_dtypes(include=['number'])
Q1 = numeric_df.quantile(0.25)
Q3 = numeric_df.quantile(0.75)

# Step 4: Calculate IQR
# This creates a Series, allowing the test script to use .to_numpy()
iqr = Q3 - Q1

# Step 5: Calculate Upper and Lower bounds
upper_bound = Q3 + 1.5 * iqr
lower_bound = Q1 - 1.5 * iqr

# Step 6: Identify Columns with Outliers
# 1. Compare the whole dataframe to the bounds
# 2. .sum() counts outliers per column
# 3. Divide by total rows (df.shape[0]) to get the percentage
outlier_percentages = ((numeric_df < lower_bound) | (numeric_df > upper_bound)).sum() / df.shape[0]

# Filter for percentages > 11% and convert the index to a list
outlier_columns = outlier_percentages[outlier_percentages > 0.11].index.tolist()
# Vectorization: By calling df.quantile() on the whole DataFrame, Q1, Q3, and iqr become Pandas Series.
```
