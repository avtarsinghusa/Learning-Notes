# Analyzing Text Data -- Week 4
### Checking for missing or duplicate values and removing them 
```
data.isnull().sum()
# checking for duplicate values
data.duplicated().sum()
# keeping only the first occurence of duplicate values and dropping the rest
data = data.drop_duplicates(keep = 'first')
# reseting the index of the dataframe
data = data.reset_index(drop = True)
```

## Text Preporcessing
### Why Remove Special Characters in Text Preprocessing?
* Special characters can introduce unnecessary elements, complicating text analysis.
* Clean text is simpler to work with and understand.
* However, as text become larger and contain various patterns of special characters, manually handling like use of **replace()** becomes tedious.
* In such cases, we need more flexible methods to efficiently identify and remove multiple patterns at once - **this is where advanced tools like regular expressions come in handy**.
* Suppose you have a string, and you are interested in adding a character between each of its characters
  * This is where the **join method** comes to rescue.
    * The **join()** method takes all characters in a string and joins them into one string with a sepataror.
    * A string must be specified as the separator.
    *  Syntax : string.join(list)
```
import re
string = "Regular expressions"
' '.join(string)
# As we can observe, the string 'space' has been added between each character in the string
# output - R e g u l a r   e x p r e s s i o n s
```
#### 
