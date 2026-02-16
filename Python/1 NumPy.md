# Common Coammnds used in NumPy

### Array
* An array is a data structure that stores values of same data type.
* While python lists can contain values corresponding to different data types, arrays in python can only contain values corresponding to the same data type.
```
# defining a list of different car companies or string elements
arr_str = ['Mercedes', 'BMW', 'Audi', 'Ferrari', 'Tesla']
# connverting the list arr_str to a NumPy array
np_arr_str = np.array(arr_str)
```
### Functions to Create Array
There are different ways to create NumPy arrays using the functions available in NumPy library
* Using **np.arange()** function  
  * The np.arange() function returns an array with evenly spaced elements as per the interval. The interval mentioned is half-opened i.e. start is included but stop is excluded.
  * It has the following paramaters:
        start : start of interval range. By default start = 0
        stop : end of interval range
        step : step size of interval. By default step size = 1

```
arr2  = np.arange(start = 0, stop = 10) # 10 will be excluded from the output
# or
arr2  = np.arange(0,10)
arr2 = np.arange(0,101,10)
```
* Using **np.linspace()** function
  * The np.linspace() function returns numbers which are evenly distributed with respect to interval. Here the start and stop both are included.
  * It has the following parameters:
    start: start of interval range. By default start = 0
    stop: end of interval range
    num : No. of samples to generate. By default num = 50
```
matrix2 = np.linspace(0,5) # by default 50 evenly spaced values will be generated between 0 and 5
# generating 10 evenly spaced values between 10 and 20
matrix3 = np.linspace(10,20,10)
```
### NumPy Matrix
* A matrix is a two-dimensional data structure where elements are arranged into rows and columns.
* A matrix can be created by using list of lists
```
# let's say we have information of different number of cylinders in a car and we want to display them in a matrix format
matrix = np.array([[1,2,1],[4,5,9],[1,8,9]])
```
### Functions to create Matrix
Similarly we can create matrices using the functions available in NumPy library
* Using **np.zeros()**
    * The np.zeros() It returns a matrix filled with zeros of the given shape.
    * It has the following parameters:
        shape : Number of rows and columns in the output matrix.
        dtype: data type of the elements in the matrix, by default the value is set to float.
* Using **np.ones()**
    * It returns a matrix of given shape and type, filled with ones.
    * It has the following parameters:
        shape : Number of rows and columns in the output matrix.
        dtype: data type of the elements in the matrix, by default the value is set to float.
* Using **np.eye()**
    * **It returns a matrix with ones on the diagonal and zeros elsewhere.**
    * It has the following parameters:
        n: Number of rows and columns in the output matrix
        dtype: data type of the elements in the matrix, by default the value is set to float.
* We can also **convert a one dimension array to a matrix.** This can be done by using the **np.reshape()** function.
  * The shape of an array basically tells the number of elements and dimensions of the array.
  * **Reshaping a Numpy array simply means changing the shape of the given array.**
  * By reshaping an array we can add or remove dimensions or change number of elements in each dimension.
  * In order to reshape a NumPy array, we use the reshape method with the given array.
    Syntax: **array.reshape(shape)**
        shape: a tuple given as input, the values in tuple will be the new shape of the array.
```
matrix4 = np.zeros([3,5])
matrix5 = np.ones([3,5])
matrix6 = np.eye(5)
# defining an array with values 0 to 9
arr4 = np.arange(0,10)
# reshaping the array arr4 to a 2 x 5 matrix
arr4_reshaped = arr4.reshape((2,5))
```


      



