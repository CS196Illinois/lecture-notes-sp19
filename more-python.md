# More Python
Rather than covering new material this week, we have instead elected to use this week to ensure that you guys all have a solid grasp on python. We will be moving onto Flask next week, and you will find those concept **extremely** confusing if you are still trying to understand the language. 

Hopefully the Problem of the Days have been going well for you all. From the POTDS, you should have been introduced to several functions that you can use to manipulate lists, strings, such as `split`. Python has many of these useful built-in functions, so don't be afraid to use google before writing your own functions in the case that there is already a built-in one that does the same thing. 

During this lecture, you should have received a new set of problems. By the end of class, you should hopefully be able to solve all of them! Here are some extra miscellaneous notes on some concepts that you may find useful when coding in Python.

### 2D Lists
This is not so much a new concept as it is just understanding a simple data structure in python. I'm sure you are all familiar with 2D arrays in Java or C++, well, python has 2D lists which can be treated as the equivalent of a 2D array. For example:
```python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
```
`matrix` is a 2D list with 3 rows and 3 columns. If I wish to access `4` I can simply do `matrix[1][0]`. This is because I want to access the 0th element in row 1 (r   emember rows and columns are 0-indexed). 

As was true with lists in python, 2D lists do not require that all of their elements be of the same type. Moreover, each row of the list does not to be of the same length. For example:
```python
my_list = []
a = [1,'a']
b = [3,3,3]
my_list.append(a)
my_list.append(b)
```
Here, `my_list` has 2 rows where the first row has 2 elements and the second row has 3. Here `my_list = [[1,'a'],[3,3,3]]`. Note that I used `append` function to create my 2D list. This is because I can start with a empty list and add 2 elements, each of which are a list themselves. if you call `len(my_list)`, you will get 2, the number of rows in the **jagged** list while `len(my_list[0])` will give you the length of the 0th row. You will get more practice with 2D lists today. 


## Functions as Parameters
In python, the parameters you pass into a function are not limited to just values. In fact you can pass in a function as a parameter. This is extremely useful if you are designing a program that may need to call one of several functions based upon what the user wants. For example. Say I have the following functions.
```python
def add(x,y):
  return x + y

def multiply(x,y):
  return x*y
```
I can now design the following calculate function:
```python
def calculate(operation, x,y):
  return operation(x,y)
```
Here the operation to perform is a parameter to the function. I simply need to pass in the name of the function, and that function will be executed using x and y as parameters. For example, I can do `calculate(add, 3,4)` and the add function will be called on 3 and 4. Similarly I can call `calculae(multiply, 5,6)` and the multiply function will be called on 5 and 6. This ability to pass functions in as parameters will become quite useful down the line. 

## Lambdas
A lambda allows you to create an *anonymous* function (function without a name) in python. For example, let us take the `multiply` function.
```python
def multiply(x,y):
  return x*y
```
I can do this same thing using a lambda. 
```python
a = lambda x,y : x*y
print(a(3,4))
```
Here the function is stored in the `a` variable which can then be called using two arguments, x and y, as shown. This code would print 12. Note the format of the lambda here. After the word `lambda`, the parameters are listed separated by commas. There is then a `:` after which the return value of the lambda is specified. lambdas are often useful when you need a simply, short function but do not want to actually define the function.

If you wish to learn more about lambdas, you can visit [this tutorial by w3schools](https://www.w3schools.com/python/python_lambda.asp).

## Testing
Similar to Java or any other coding language you have worked with in the past, you can perform unit tests in Python! 

Testing your code is arguably half the work when it comes to programming. Both in school and in industry, you will be required to test and verify that your code functions as advertised before submitting. At your future job, you will definitely want to thoroughly test your code prior to publishing it as finding a bug yourself is infinitely better than having someone else (worst of all the consumer) finding it. When it comes to testing, there are several different types of testing. Here are a few.

**Unit Tests** are those that test a single element or function of your program. These are useful when testing individual methods/functions to make sure that each works independently.

**Integration Tests** are those that test how multiple functions/methods interact and work together. If you have several functions in your program that work together, an integration test would be used to test how several of these programs work together.

**End to End Tests** are just what they sound like. They are the tests that you perform on your program as a whole to make sure that everything is working properly.

**Load/Stress Tests** are tests designed to see how well your program hands extremely large or unusual inputs. It is often important to design robust programs that won't crash even whlie handling the most ruthless (large) inputs.

In this lecture, we will be focusing on unit-tests. The syntax for unit-tests in python may seem a bit strange, so [here](https://docs.python-guide.org/writing/tests/) is an extra guide to understanding and writing your own unit tests in python. 
