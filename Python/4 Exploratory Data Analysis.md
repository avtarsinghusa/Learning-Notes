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
```
