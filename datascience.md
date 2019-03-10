# Data Science Tools in Python
In this lecture, we will be overviewing some basic tools and packages you can use in python when working with numerical data. We will be going over numpy, scipy, matplotlib, and pandas. Note that these libraries are huge, so these notes will be only a simple introduction. Likely, if you are trying to do something with numerical arrays in python, there exists a numpy function that will do it for you. So, don't be afraid to use Google. All of these libraries are thoroughly documented, so you just look up "how to ... with numpy", the first result is likely to be exactly what you are looking. 

Now, before we can start working with these packages, we need to install them. To do this, we can use pip (or you can go to their respective websites and download them from there). 
```
pip install numpy
pip install scipy
pip install pandas
pip install matplotlib
```
Should do the trick. you may want to use `pip3` instead of `pip`, depending on what you have installed. To use these packages in a python file, we simply have to import them as follows
```python
import numpy as np
import scipy as sp
import matplotlib.pyplot as plt
import pandas as pd
```
When we say `import numpy as np` what that means is that whenever we want to call a function from numpy, rather than typing `numpy.function`, we can just do `np.function`, so the `as` keyword lets us specify a "nickname" for the package. Now, lets gget working with numpy!
## Numpy (numerical python)
The majority of numpy functions perform actions on numpy array. So, lets first discuss how we create a numpy array. One way we can do so by using the `numpy.array` function to convert a python list to a numpy array.
```python
my_arr = [1,2,3,4]
np_arr = np.array(my_arr)
```
will produce a numpy array with the same elements. One warnng though about using numpy arrays, all the elements must have the same data type (so no passing in a list with both strings and integers). Since numpy functions deal with numbers, passing in a list of strings, does not really make much sense. Note that not all numbers are treated equal. There are several different `dtypes` of numbers, such as ints, floats, complex, etc. All the elements of a given numpy array must be of the same type. To get the data type of thispy array, we can do `np_arr.dtype`. If we wanted to change the data type of this array to be complex numbers (or any different `dtype` for that matter, we can do `np_arr.astype(np.complex)`.

Another deviation from python lists is that numpy arrays cannot change size once they are declared. Along with this requirement, any 2d list or higher dimensional list we want to convert to a numpy array must be a matrix, meaning it cannot be jagged (where some rows have more elements than others). We can get the shape of our array by doing `np_arr.shape`, which will return a tuple. If there are mulitple dimensions (such as for a 2d array) it will list the number of elements in each direction. Since, `np_arr` is a 1 array, it will return a tuple of size 1. Note, you can also use `len` here just as you can for a python list. Aside from these differences, numpy arrays behave very similar to python lists (you can still use slicing). 

If you do not need to create a python list first that is later converted to a numpy array, it is encouraged to use one of several numpy functions that will create an array with certain values for you. For example.
```python
np.zeros((3,4))
```
will create a matrix of size 3,4 (3 rows, 4 columns) where all the elements are 0. We can do the same thing with `np.ones` (but this will produce a matrix with all 1s). Other useful ways of creating numpy arrays include `np.linspace` and `np.arange` these will allow you to specify start and end values while choosing how many equally spaced points to take from that range. For example
```python
np.linspace(1.0, 2.0, 5)
```
will produce the array `[1.0, 1.25,1.5,1.75,2]`. If want an array of random values, we can use [np.random](https://docs.scipy.org/doc/numpy/reference/routines.random.html). 

Now, that we have numpy arrays, what can we do with them! Well, pretty much anything you would want to do. You want to take the mean of `np_arr` that we defined above, we can do `np.mean(np_arr)`. We want the max or the min, we can do `np.max(np_arr)` or `np.min(np_arr)`. If we want the index where the max occurs, we can do `np.argmax(np_arr)`. These methods all allow us to specify an axis as well. This axis allows us only to perform the operation along a certain axis. For example.
```python
a = np.array([[1,2],[3,4]]
np.max(a, axis = 0)
```
This would return the array `[3,4]` as it would take the max along the 0th axis. meaning it would get the max element in each column.
There are many more applications for numpy, if you want to learn more (which I highly encourage you do), [this](https://docs.scipy.org/doc/numpy/user/quickstart.html) intro tutorial may be helpful. Remember, numpy offers a ridiculous number of functions for you to use with your numerical arrays, so do not be afraid to google. There is no point in writing a long function in your code when all the work could have been done in 1 line with numpy. 

## Scipy (scientific python)
I am not going to cover scipy in this tutorial specifically, but I recommend checking [this one](https://docs.scipy.org/doc/scipy/reference/tutorial/) out. If there is a numerical function you can't find in numpy, it is likely available in scipy.
