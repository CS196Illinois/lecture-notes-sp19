# Python Basics
These notes will provide a brief overview of the fundamentals of Python. Links will be provided throughout for those that wish to learn more. 
## Basic Datatypes
The basic datatypes we will be using in this class are **integers**, **floating point numbers**, **booleans**, and **strings**.
Before we cover datatypes, it is important to understand what a **variable** is. A variable is an entity that can be used to store data.
```python
myNumber = 5
myWord = 'Hello'
```
In the code snippet above, both **myNumber** and **myWord** are variables that are used to store/reference data. Now, if we wished to print the word, hello, to the screen. We could do either of the following.
```python
print('hello')
print(myWord)
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
myNumber = 5
```
Note that I do not have to specify that the `myNumber` is an `int` in python. This is because python employs dynamic typing for variables while java statically types variables. This means, that once defined, a variable in python can actually change types. For example, the following is an entirely valid bit of code
```python
myNumber = 5
myNumber = 'Hello'
```
In java, this would throw an error, but in python, it is completely acceptable. This ability to change the type of a variable may seem convenient, but it can become confusing at times where you lose track of the type of the variable in question. Luckily, you can use the `type` method to determine the type of the variable.
```python
type(myNumber)
```
While this may seem like a drastic change from java, python variables do share many features with their java counterpart such as scope.

