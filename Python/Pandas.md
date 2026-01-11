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

# converting the med_price_list to an array
med_price_arr = np.array(med_price_list)

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
```
