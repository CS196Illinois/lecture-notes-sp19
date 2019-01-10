# Python Basics
These notes will provide a brief overview of the fundamentals of Python. Links will be provided throughout for those that wish to learn more. 
## Basic Datatypes
The basic datatypes we will be using in this class are **integers**, **floating point numbers**, **booleans**, and **strings**.
Before we cover datatypes, it is important to understand what a **variable** is. A variable is an entity that can be used to store data.
```python
my_number = 5
my_word = 'Hello'
```
In the code snippet above, both `my_number` and `my_word` are variables that are used to store/reference data. Now, if we wished to print the word, hello, to the screen. We could do either of the following.
```python
print('hello')
print(my_word)
```
We will cover variables more indepth here shortly. 

#### Integers
The integer datatype is just what it sounds like, an integer (whole number). While other languages, such as java, may limit the size of an integer (integers can only be between -2,147,483,648 and 2,147,483,648), there is no such limitation in python. For example,
```python
10
1234343534534343
```
Both of these numbers are considered to be an **int** (Integer) in python.

#### Floating Point Numbers
The `float` type in Python is used for decimal numbers in python. For example, the following are floats:
```python
4.2
.12343434
```
#### Boolean
The `bool` type can take on one of two values, `True` or `False`. Similar to java, `&&`, `||`, and `!`, can be used to define boolean expressions. But the phrases `and`, `or`, and `not` are also available for use in python. For example.
```python
a = True
b = False
```
If I wished to evaluate `a && b`, I could simply do `a and b`. 

#### String
Strings are a sequence of characters. A String, or `str`, can be defined with either using single or double quotes around the desired sequence of characters. The following are valid strings:
```python
'Hello'
"Hello"
```
But the following is not a valid string, as you have to match quotes
```python
'Hello"
```
There are also a series of special characters that hold certain properties in python. For example, `\n` and `\t`, will add a new line and a tab respectively to your string. In general, most of the properties you will have learned about strings in CS125 will carry over to python strings.

**If you wish to learn more about any of these datatypes, you can go [here](https://realpython.com/python-data-types/#boolean-type-boolean-context-and-truthiness)**

### Variables
You may have noticed something odd when I was discussing variables above. In CS125, you will have learned to define an `int` variable `myNumber` as follows.
```java
int myNumber = 5
```
But in python that variable may be defined:
```python
my_number = 5
```
Note that I do not have to specify that the `myNumber` is an `int` in python. This is because python employs dynamic typing for variables while java statically types variables. This means, that once defined, a variable in python can actually change types. For example, the following is an entirely valid bit of code
```python
my_number = 5
my_number = 'Hello'
```
In java, this would throw an error, but in python, it is completely acceptable. This ability to change the type of a variable may seem convenient, but it can become confusing at times where you lose track of types of your variables. Luckily, you can use the `type` method to determine the type of the variable.
```python
type(my_number)
```
While this may seem like a drastic change from java, python variables do share many features with their java counterpart such as scope.

## Data Structures
In this class, we will primarily focus on two datastuctures: lists and dictionaries.

### Lists
Python lists work similar to arrays in java. They can be defined as follows:
```python
list_a = []
list_b = [1,2,3]
```
In the code above, `list_a` is defined to be an empty list while `list_b` holds the values `1,2,3`. Similar to java arrays, python lists are 0-indexed, which means you can access the first element of your list via `list_b[0]`, the second element via `list_b[1]`, and so forth. In python, it is also appropriate to use negative indices. The last element of your list can be indexed via `list_b[-1]`, second to last element via `list_b[-2]`, and so forth.

Lists in python do not have a specific type associated with them, so a list can hold muliple different datatypes, or even other lists for that matter. The following is an entirely legal definition of a list.
```python
list_c = [1,2,'a', ['hello'], 4.2]
```

Another departure from java arrays is that python lists have the ability to change size once they are defined. For example, the `append` method can be used to add an element to the end of a list.
```python
my_list = [1,2,3]
my_list.append(4)
```
This code would result in `my_list` being equal to `[1,2,3,4]`. Several other methods are available for you to work with and manipulate your lists, you can find documentation [here](https://docs.python.org/3/tutorial/datastructures.html)

#### Slicing
For this portion, we will be working with the following list
```python
my_list = [1,2,3,4,5,6,7]
```
There are times where you may wish  to only work with a portion of the list. At these times, it may be useful to employ slicing. A slice can be performed as follows `my_list[first : second]` where `first` and `second` are valid indices. A slice will return to you a subarray (portion of the array) that starts at the `first` index and goes up to but does not include the `second` index. So `my_list[1:3]` will return `[2,3]`. 

You may also choose to omit either index in your slice. Omiting `first`, will start the slice at the start of the array, and omitting `second` will end the slice at the end of the array. So, `my_list[5:]` will produce `[6,7]` and `my_list[:2]` will produce `[1,2]`.

Note, any changes you make to a slice of the list, such as changing a value, will affect the entire list. You can find more documentation [here](https://www.pythoncentral.io/how-to-slice-listsarrays-and-tuples-in-python/).

Another note about python lists is that python strings are treated as lists. Similar to a list, you can index a string. For example
```python
my_string = 'hello'
print(my_string[1])
```
This code will print out 'e' since 'e' is the character at the 1-index. Additionally, strings can be sliced in the same way as lists in order to produce substrings. 
### Dictionaries
Dictionaries work very similarly to Hash Maps in Java. A Dictionary is like a list in that it is a collection of objects, but it differs primarily in the fact that it is unordered. Rather than accessing elements via their numerical index (0,1,2,3... n - 1 where n is the size of the List, Dictionaries function by using key-value pairs. Rather than accessing a certain value by its numerical index, you can access that value via a key. Below is how you can define a dictionary in python.

```python
empty_dict = {}
my_dict = {'a': 'alpha', 'b' : 'bravo'}
```
In this example, `empty_dict` is an empty dictionary and `my_dict` is a dictionary with 2 key-value pairs. In this example, the keys of the dictionary are `a,b` and the values are `alpha, bravo`. If I wished to retreive the value `bravo` from this dictionary, I could do `my_dict['b']` or `my_dict.get('b')` since `'b'` is the key associated with the value `bravo`.
Similar, to a list where you can have invalid indices (like when you enter an index that is greater than the size of the list), the same can happen with dictionaries if you attempt to use a key that is not valid. For example, `my_dict['aba']` would return a `KeyError` because a valid has not been given for the key 'aba'. 
If I wish to add the key value pair `'c': 'charlie'` where 'c' is the key for the value 'charlie', the following could be used:
```python
my_dict['c'] = 'charlie'
```
Similarly, if I wished to change the value associated with 'b' to 'beta', the following could be used.
```python
my_dict['b'] = 'bravo'
```
If I wish to check if a certain key exists in a dictionary, we can use an `if statement` which we will go into more detail later. 
The following can be used to see if the key 'a' exists in the `my_dict`
```python
if 'a' in my_dict:
  # do something
```
Note, that the keys and values in a dictionary are not required to be strings, they can be any datatype, but keep in mind that each key must be unique. While two keys may have the same value associated with them, each key must different. 
