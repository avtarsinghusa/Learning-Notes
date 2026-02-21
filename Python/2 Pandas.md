# Common Coammnds used in Pandas -- Week 2

### Pandas Series
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
# changing the index of a series
med_price_list_labeled = pd.Series(med_price_list, index = ['Omeprazole','Azithromycin','Metformin','Ibuprofen','Cetirizine'])
print(med_price_list_labeled)

Omeprazole      55
Azithromycin    25
Metformin       75
Ibuprofen       40
Cetirizine      90
```
* We can perform mathematical operations directly on Pandas Series and it will impact all the rows
* The price of each medicine was increased by $2.5. Let's add this to the existing price.
```
# adding 2.5 to existing prices
med_price_list_labeled_updated = med_price_list_labeled + 2.5
# To see the diff between two prices
print(med_price_list_labeled_updated - med_price_list_labeled)
```
### Pandas DataFrame
* Pandas DataFrame is a two-dimensional tabular data structure **with labeled axes (rows and columns)**.
```
# Creating a Pandas DataFrame using a list
student = ['Mary', 'Peter', 'Susan', 'Toby', 'Vishal']
df1 = pd.DataFrame(student,columns=['Student'])

Student
0 	Mary
1 	Peter
2 	Susan
3 	Toby
4 	Vishal

# Creating a Pandas DataFrame using a list
  # defining another list
  grades = ['B-','A+','A-', 'B+', 'C']

# creating the dataframe using a dictionary
df2 = pd.DataFrame({'Student':student,'Grade':grades})

  Student 	Grade
0 	Mary 	B-
1 	Peter 	A+
2 	Susan 	A-
3 	Toby 	B+
4 	Vishal 	C

# Creating a Pandas DataFrame using random values
  # we can create a new dataframe using random values
df4 = pd.DataFrame(np.random.randn(5,2),columns = ['Trial 1', 'Trial 2'])

    Trial 1 	Trial 2
0 	-0.015499 	1.061322
1 	-0.230169 	-0.190214
2 	0.503623 	0.586519
3 	-0.226932 	-1.373368
4 	0.022637 	-0.854181
```
### Accessing DataFrame
* creating the dataframe using dictionary
```
store_data = pd.DataFrame({'CustomerID': ['CustID00','CustID01','CustID02','CustID03','CustID04']
                           ,'location': ['Chicago', 'Boston', 'Seattle', 'San Francisco', 'Austin']
                           ,'gender': ['M','M','F','M','F']
                           ,'type': ['Electronics','Food&Beverages','Food&Beverages','Medicine','Beauty']
                           ,'quantity':[1,3,4,2,1],'total_bill':[100,75,125,50,80]})
store_data

   CustomerID 	location 	gender 	type 	quantity 	total_bill
0 	CustID00 	Chicago 	M 	Electronics 	1 	100
1 	CustID01 	Boston 	  M 	Food&Beverages 	3 	75
2 	CustID02 	Seattle 	F 	Food&Beverages 	4 	125
3 	CustID03 	SFO     	M 	Medicine 	2 	50
4 	CustID04 	Austin   	F 	Beauty 	1 	80
```
* For a DataFrame, **passing a slice : selects matching rows**, excluding the end number
*  Selection by Label using DataFrame.loc() or DataFrame.at().
```
# accessing first row of the dataframe
store_data[:1]
```
#### Using loc and iloc method
* loc method
  * loc is a method to access rows and columns on pandas objects. When using the loc method on a dataframe, we specify which rows and which columns we want by using the format: 
    **dataframe.loc[row selection, column selection]**
  * DataFrame.loc[] method is a method that **takes only index labels** and returns row or dataframe if the index label exists in the data frame.
  * Slicing is inclusive ('A':'C' includes 'C')
  * Supports boolean conditions
 ```
df.loc['A']              # row with index label 'A'
df.loc[:, 'age']         # all rows, column named 'age'
df.loc['A':'C']          # rows A through C (inclusive!)
df.loc[df['age'] > 30]   # boolean filtering

# accessing first index value using loc method (indexing starts from 0 in python)
store_data.loc[0 ]

             	0
CustomerID 	CustID00
location 	Chicago
gender 	  M
type 	  Electronics
quantity 	  1
total_bill 	100

# print the first row only with all the columns name without providing the column names in python
store_data.loc[0:0, :]

  CustomerID 	location 	gender 	type 	quantity 	total_bill
0	CustID00 	Chicago 	M 	Electronics 	1 	100

# accessing 1st and 4th index values along with location and type columns
store_data.loc[[1,4],['type', 'location']]
```
* iloc method
    * Slicing is exclusive at the end (like Python)
    * The iloc indexer for Pandas Dataframe is used for integer location-based indexing/selection by position. When using the iloc method on a dataframe, we specify which rows and which columns we want by using the format: 
        **dataframe.iloc[row selection, column selection]**
```
df.iloc[0]               # first row
df.iloc[:, 1]            # second column
df.iloc[0:3]             # rows at positions 0,1,2
df.iloc[2, 3]            # row 3, column 4

# accessing selected rows and columns using iloc method
store_data.iloc[[1,4],[0,2]]

  CustomerID 	gender
1 	CustID01 	M
4 	CustID04 	F
```
* **Difference between loc and iloc indexing methods**
  * loc is label-based, which means that you have to specify rows and columns based on their row and column labels.
  * iloc is integer position-based, so you have to specify rows and columns by their integer position values
  * loc exclude the end index whereas iloc include the end index. e.g. loc[0,2] exclude the index 2 where as iloc includes the index 2. 
* **We can modify entries of a dataframe using loc or iloc too**
```
store_data.loc[4,'type'] = 'Electronics'
store_data.iloc[4,3] = 'Beauty'

# Condition based indexing
store_data['quantity']>1

0    False
1     True
2     True
3     True
4    False

# Wherever the condition of greater than 1 is satisfied in quantity column, 'True' is returned. Let's retrieve the original values wherever the condition is satisfied.

store_data.loc[store_data['quantity']>1]

CustomerID 	location 	gender 	type 	quantity 	total_bill
1 	CustID01 	Boston 	M 	Food&Beverages 	3 	75
2 	CustID02 	Seattle 	F 	Food&Beverages 	4 	125
3 	CustID03 	San Francisco 	M 	Medicine 	2 	50

# Wherever the condition is satisfied we get the original values, and wherever the condition is not satisfied we do not get those records in the output.
```
### Column addition and removal from a Pandas DataFrame
* Adding a new column in a DataFrame
```
# adding a new column in data frame store_data which is a rating (out of 5) given by customer based on their shopping experience
store_data['rating'] = [2,5,3,4,4]

 CustomerID 	location 	gender 	type 	quantity 	total_bill 	rating
0 	CustID00 	Chicago 	M 	Electronics 	1 	    100     	2
1 	CustID01 	Boston 	  M 	Food&Beverages 	3 	  75       	5
2 	CustID02 	Seattle 	F 	Food&Beverages 	4 	  125     	3
3 	CustID03 	San Francisco 	M 	Medicine 	2 	  50       	4
4 	CustID04 	Austin 	F 	Beauty 	          1 	  80       	4
```
* Removing a column from a DataFrame
  * The CustomerID column is a unique identifier of each customer. This unique identifier will not help 24/7 Stores in getting useful insights about their customers. So, they have decided to remove this column from the data frame.
```
store_data.drop('CustomerID',axis=1)

  location 	gender 	type 	quantity 	total_bill 	rating
0 	Chicago 	M 	Electronics 	1 	  100     	2
1 	Boston   	M 	Food&Beverages 	3 	75 	      5
2 	Seattle 	F 	Food&Beverages 	4 	125     	3
3 	San Francisco 	M 	Medicine 	2 	50       	4
4 	Austin   	F 	  Beauty 	      1 	80       	4
```
* We sucessfully removed the 'CustomerID' from dataframe. But this change is not permanent in the dataframe, let's have a look at the store_data again.
* To make permanent changes to a dataframe there are two methods will have to use a parameter inplace and set its value to True.
```
store_data.drop('CustomerID',axis=1,inplace=True)

# we can also remove multiple columns simultaneously
# it is always a good idea to store the new/updated data frames in new variables to avoid changes to the existing data frame

# creating a copy of the existing data frame
new_store_data = store_data.copy()

# dropping location and rating columns simultaneously
new_store_data.drop(['location','rating'],axis=1,inplace=True)

  gender 	type 	quantity 	total_bill
0 	M 	Electronics 	    1 	100
1 	M 	Food&Beverages 	  3 	75
2 	F 	Food&Beverages 	  4 	125
3 	M 	Medicine         	2 	50
4 	F 	Beauty           	1 	80
```
* Removing rows from a dataframe
```
store_data.drop(1,axis=0)

  CustomerID 	location 	gender 	type 	      quantity 	total_bill 	rating
0 	CustID00 	Chicago 	M 	   Electronics 	  1 	100 	2
2 	CustID02 	Seattle 	F 	  Food&Beverages 	4 	125 	3
3 	CustID03 	San Francisco 	M 	Medicine 	  2 	50 	4
4 	CustID04 	Austin 	F 	    Beauty 	        1 	80 	4
```
* Notice that **we used axis=0 to drop a row from a data frame**, while **we were using axis=1 for dropping a column from the data frame.**
* Also, to make permanent changes to the data frame we will have to use **inplace=True** parameter.
* We also see that the index are not correct now as first row has been removed. So, we will have to reset the index of the data frame.
```
# resetting the index of data frame
store_data_new.reset_index()

  index 	location 	gender 	type 	quantity 	total_bill 	rating
0 	0 	Chicago 	M 	Electronics 	1 	100 	2
1 	2 	Seattle 	F 	Food&Beverages 	4 	125 	3
2 	3 	San Francisco 	M 	Medicine 	2 	50 	4
3 	4 	Austin 	F 	Beauty 	1 	80 	4
```
* We see that the index of the data frame is now resetted but the index has become a column in the data frame. We do not need the index to become a column so we can simply set the parameter drop=True in reset_index() function.
```
# setting inplace = True to make the changes permanent
store_data_new.reset_index(drop=True,inplace=True)

  location 	gender 	type 	quantity 	total_bill 	rating
0 	Chicago 	M 	Electronics 	1 	100 	2
1 	Seattle 	F 	Food&Beverages 	4 	125 	3
2 	San Francisco 	M 	Medicine 	2 	50 	4
3 	Austin 	F 	Beauty 	1 	80 	4
```
### Pandas - Combining DataFrames
* 3 methods for combining dataframes
1. Concat
2. Merge
3. Join

#### Concat
```
data_cust = pd.DataFrame({"customerID":['101','102','103','104'],
                        'category': ['Medium','Medium','High','Low'],
                        'first_visit': ['yes','no','yes','yes'],
                        'sales': [123,52,214,663]},index=[0,1,2,3])

data_cust_new = pd.DataFrame({"customerID":['101','103','104','105','106'],
                    'distance': [12,9,44,21,4],
                    'sales': [123,214,663,331,221]},index=[4,5,6,7,8])

#Added data at row level
pd.concat([data_cust,data_cust_new],axis=0) 

  customerID 	category 	first_visit 	sales 	distance
0 	101     	Medium 	      yes 	    123 	NaN
1 	102 	    Medium 	    no         	52 	NaN
2 	103 	    High       	yes 	      214 	NaN
3 	104 	    Low 	      yes 	      663 	NaN
4 	101 	    NaN 	      NaN 	      123 	12.0
5 	103 	    NaN 	      NaN 	      214 	9.0
6 	104 	    NaN 	      NaN 	      663 	44.0
7 	105 	    NaN 	      NaN 	      331 	21.0
8 	106 	    NaN 	      NaN 	      221 	4.0

#Added data at column level
pd.concat([data_cust,data_cust_new],axis=1)

  customerID 	category 	first_visit 	sales 	customerID 	distance 	sales
0 	101 	Medium 	yes 	123.0 	NaN 	NaN 	NaN
1 	102 	Medium 	no 	  52.0 	NaN 	NaN 	NaN
2 	103 	High 	yes 	214.0 	NaN 	NaN 	NaN
3 	104 	Low 	yes 	663.0 	NaN 	NaN 	NaN
4 	NaN 	NaN 	NaN 	NaN 	101 	12.0 	123.0
5 	NaN 	NaN 	NaN 	NaN 	103 	9.0 	214.0
6 	NaN 	NaN 	NaN 	NaN 	104 	44.0 	663.0
7 	NaN 	NaN 	NaN 	NaN 	105 	21.0 	331.0
8 	NaN 	NaN 	NaN 	NaN 	106 	4.0 	221.0
```
#### Merge
* Merge combines dataframes **using a column's values** to identify common entries
```
pd.merge(data_cust,data_cust_new,how='outer',on='customerID') # outer merge is union of on

 	customerID 	category 	first_visit 	sales_x 	distance 	sales_y
0 	101 	    Medium 	yes 	123.0 	12.0 	123.0
1 	102 	    Medium 	no 	52.0 	NaN 	NaN
2 	103 	    High 	yes 	214.0 	9.0 	214.0
3 	104 	    Low 	yes 	663.0 	44.0 	663.0
4 	105 	    NaN 	NaN 	NaN 	21.0 	331.0
5 	106 	    NaN 	NaN 	NaN 	4.0 	221.0

pd.merge(data_cust,data_cust_new,how='inner',on='customerID') # inner merge is intersection of on

  customerID 	category 	first_visit 	sales_x 	distance 	sales_y
0 	101 	    Medium 	yes 	123 	12 	123
1 	103 	    High 	yes 	214 	9 	214
2 	104 	    Low 	yes 	663 	44 	663

pd.merge(data_cust,data_cust_new,how='right',on='customerID')

customerID 	category 	first_visit 	sales_x 	distance 	sales_y
0 	101 	Medium 	          yes 	123.0 	          12 	123
1 	103 	High             	yes 	214.0 	          9 	214
2 	104 	Low 	            yes 	663.0 	          44 	663
3 	105 	NaN 	          NaN 	  NaN 	            21 	331
4 	106 	NaN 	          NaN 	  NaN 	            4 	221
```  
#### Join
* join behaves just like merge, except **instead of using the values of one of the columns to combine data frames, it uses the index labels**
```
data_quarters = pd.DataFrame({'Q1': [101,102,103],
                              'Q2': [201,202,203]},
                               index=['I0','I1','I2'])

data_quarters_new = pd.DataFrame({'Q3': [301,302,303],
                                  'Q4': [401,402,403]},
                               index=['I0','I2','I3'])
data_quarters.join(data_quarters_new,how='right') # outer, inner, left, and right work the same as merge

      Q1 	    Q2 	    Q3 	Q4
I0 	101.0 	201.0 	301 	401
I2 	103.0 	203.0 	302 	402
I3 	NaN 	  NaN 	  303 	403
```
### Pandas - Saving and Loading DataFrames
* For Jupyter Notebook -- When the data file and jupyter notebook are in the same folder.
```
# Using pd.read_csv() function will work without any path if the notebook and dataset are in the folder

# data = pd.read_csv('StockData.csv')
```
* For Google Colab with Google Drive -- First, we have to give google colab access to our google drive:
```
from google.colab import drive
drive.mount('/content/drive')
path="/content/drive/MyDrive/Python Course/StockData.csv"
data=pd.read_csv(path)
```
* Saving the dataset as a csv file
  *To save a dataset as .csv file the syntax used is - **data.to_csv('name of the file.csv', index=False)**
### Pandas - Functions
* **head()** - to check the first 5 rows of the dataset
* **tail()** - to check the last 5 rows of the dataset
* **shape** - to check the number of rows and columns in the dataset
* **info()** - to check the data type of the columns
* **min()** - to check the minimum value of a numeric column -- ``` data['price'].min() ```
* **max()** - to check the maximum value of a numeric column -- ``` data['price'].max() ```
* **unique()** - to check the number of unique values that are present in a column -- ``` data['stock'].unique() ```
* **value_counts()** - to check the number of values that each unique quantity has in a column -- ``` data['stock'].value_counts() ```
*  On setting the **normalize parameter to True**, the **value_counts()** function returns the relative frequencies of unique values within the Series.
```
import pandas as pd

# Creating a Series
data = pd.Series(['Apple', 'Banana', 'Apple', 'Apple', 'Chocolate', 'Banana'])

# Statement A: Standard value_counts()
counts = data.value_counts()

# Statement B: value_counts(normalize=True)
frequencies = data.value_counts(normalize=True)

print("--- Absolute Counts ---")
print(counts)
print("\n--- Relative Frequencies ---")
print(frequencies)

Breakdown of the Output
Value	  Absolute Count (Statement A)	Relative Frequency (Statement B)
Apple	       3	                        0.5 (or 50%)
Banana	     2	                        0.333 (or 33.3%)
Chocolate	   1	                        0.166 (or 16.7%)

# Another Example
# Finding the Majority Value
# Find the majority value in the Purpose column. Store the value in a dictionary named majority where the key is the majority value and the item is its percentage.
majority_value = df['Purpose'].value_counts(normalize=True).idxmax()
majority_percentage = df['Purpose'].value_counts(normalize=True).max() * 100
majority = {majority_value: majority_percentage}
# Explanation: To find the majority value in the Purpose column, you should use the value_counts method with normalize=True to get the relative frequencies. Then, use idxmax() to find the value with the highest frequency and max() to get its percentage. The groupby method is not needed for this task.
```
####   Statistical Functions
* **mean()** - to check the mean (average) value of the column -- ``` data['price'].mean() ```
* **median()** - to check the median value of the column -- ``` data['price'].median() ```
* **mode()** - to check the mode value of the column -- ``` data['price'].mode() ```
* To access a particular mode **when the dataset has more than 1 mode**
```
#to access the first mode
data['price'].mode()[0]
```
##### Group By function
* Pandas dataframe.groupby() function is used to **split the data into groups** based on some criteria.
```
# Here the groupby function is used to split the data into the 4 stocks that are present in the dataset and then the mean price of each of the 4 stock is calculated.
data.groupby(['stock'])['price'].mean()

# similarly we can get the median price of each stock
data.groupby(['stock'])['price'].median()
```
###### Let's create a function to increase the price of the stock by 10%
```
def profit(s):
    return s + s*0.10 # increase of 10%
```
* The Pandas **apply()** function lets you to manipulate columns and rows in a DataFrame.
```
data['price'].apply(profit)
```
* We can now add this updated values in the dataset.
```
ata['new_price'] =data['price'].apply(profit)
```
* Pandas **sort_values()** function sorts a data frame in ascending or descending order of passed column.
```
data.sort_values(by='new_price',ascending=False) # by default ascending is set to True
```
* Replace specific values in the column or in all cloumns
```
df['BuildingArea'] = df['BuildingArea'].replace(['missing', 'inf'], np.nan)
df = df.replace(['inf', 'missing', np.inf, -np.inf], np.nan)
