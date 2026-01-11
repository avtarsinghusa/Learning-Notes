# Common Coammnds used in Pandas

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
# Accessing DataFrame
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
 ```
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
    * The iloc indexer for Pandas Dataframe is used for integer location-based indexing/selection by position. When using the iloc method on a dataframe, we specify which rows and which columns we want by using the format: 
        **dataframe.iloc[row selection, column selection]**
```
# accessing selected rows and columns using iloc method
store_data.iloc[[1,4],[0,2]]

  CustomerID 	gender
1 	CustID01 	M
4 	CustID04 	F
```
* **Difference between loc and iloc indexing methods**
  * loc is label-based, which means that you have to specify rows and columns based on their row and column labels.
  * iloc is integer position-based, so you have to specify rows and columns by their integer position values 
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
