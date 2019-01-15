# Python Basics
These notes will provide a brief overview of the fundamentals of Python. Links will be provided throughout for those that wish to learn more. 

Reminder: Make sure to sign up for the piazza for the class. You can do so by going to piazza and searching for CS196 Spring 2019 or clicking [here](piazza.com/illinois/spring2019/cs196). Make sure to also join the class slack channel. You can do so by clicking [this](https://join.slack.com/t/cs196spring2019/shared_invite/enQtNTEyODg4NDE2NjQ1LTgwODRjZjA3M2U1NDNhMWM0MjhmMzI0ZjQ1MDQzZWJlNWIzYzQwNGFmNWE3ZDI0NWM4NDc3MWQxMGZlOTY0ZGI) link. 

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

#### Strings
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
You may have noticed something odd when I was discussing variables above. In CS125, you will have learned to define an `int` variable `myNumber` as follows in java.
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
In this class, we will primarily focus on two datastructures: lists and dictionaries.

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
#### Some extra notes on Strings
Another note about python lists is that python strings are treated as lists. Similar to a list, you can index a string. For example
```python
my_string = 'hello'
print(my_string[1])
```
This code will print out 'e' since 'e' is the character at the 1-index. 

Additionally, strings can be sliced in the same way as lists in order to produce substrings. 
```python
my_string = 'Hello World'
print(my_string[:5])
```
This code will print `'hello'` as each character in the string is treated as an element in the list. The character at index 5 is a ' ', so the slice will produce all the characters before that. 

Another interesting property of Strings is that a string can be reversed as follows:
```python
my_string = 'hello'
reversed_string = my_string[::-1]
print(reversed_string)
```
This code will print `'elloh'`. This will work with any list!

Some other string methods you may find useful are `find` and `join`.

The find method can be used to determine if a string is contained in another string.
```python
big_string = 'hello world'
small_string = 'world'
print(big_string.find(small_string))
```
The `find` method will return the index where `small string` starts. So, for this example, it would return 6. If the `small_string` was not present inside of `big_string` the method would return -1. Keep in mind that strings are case-sensitive, so if `small_string = 'World'`, `big_string.find(small_string`) would return -1. The `find` method also can accept to optional arguments, `beg` and `end`, which specify the beginning and ending index to start searching for the string. 
```python
big_string.find(small_string, 2, len(big_string))
```
would only check to see if `small_string` was in `big_string[2:len(big_string)]` (The `len` method provides the length of the string). More information on the `find` method can be found [here](https://www.tutorialspoint.com/python/string_find.htm).

Another useful method is the `join` method. This method takes 1 parameter, an iterable object (for example a string or list). This method joins the items of the iterable object together as 1 string while inserting the string this method is called upon between each item. The code below demonstrates this. 
```python
a = ','
b = 'world'
c = a.join(b)
d = '123'
e = d.join(b)
```
In this code, `c` holds `'w,o,r,l,d'` and `e` holds `'w123o123r123l123d'`.

This can also be used for a list
```python
my_list = ['hello', 'world']
print(a.join(my_list))
```
This code will print `'hello,world'` as it joins the elements of `my_list` together in a string but semesters the elements using `a`. 
More documentation on the join method can be found [here](https://www.programiz.com/python-programming/methods/string/join).

There are many other string manipulation methods you may find useful during this. You are encouraged to look further into the string documentation.

### Dictionaries
Dictionaries work very similarly to Hash Maps in Java. A Dictionary is like a list in that it is a collection of objects, but it differs primarily in the fact that it is unordered. Rather than accessing elements via their numerical index (0,1,2,3... n - 1 where n is the size of the List), Dictionaries function by using key-value pairs. Rather than accessing a certain value by its numerical index, you can access that value via a key. Below is how you can define a dictionary in python.

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

You can find more documentation regarding dictionaries [here](https://www.w3schools.com/python/python_dictionaries.asp)

## If statements
An if statement can be used to execute a block of code only when a certain condition is true. For example,
```python
value = True
if value:
  print('hello')
```
In this situation, since `value = True`, `'hello'` will be printed to output, but if `value = False`, then the block of code belonging to an if-statement would not be executed. When looking at if-statements it is important to understand that can be any boolean expression. For example, we discussed the following regarding dictionaries
```python
my_dict = {'key': 'value'}
if key in my_dict:
  print('valid key')
```
In this case, `valid key` will be printed because the if-statement evaluates to true. For those familiar with java or most other language, you may notice that one key element is missing. the { } to determine what bit of code belongs to the if-statement and will execute only if the statement is true. In python, the only thing that determines what belongs to the if-statement is spacing. Notice how the code belonging to the if-statement is tabbed over. The first line that is not tabbed after the if-statement marks the end of the statement
```python
if variable:
  print(1)
  print(2)
print(3)
```
For this code, 3 will always be printed but 1 and 2 will only print if variable is true. 

Along with the if-statement, it is also important to understand `elif` (the equilavent of an `else if` in java) and `else`. An `elif` condition allows you to provide an additional conditional statement to test if the if-statement evaluates to false. In the case the original if-statement is false, the `elif` condition will be tested and it is is true, then perform the action in the elif block. The `else` path is the one that will be taken if none of the `if` or `elif` conditions hold. Note that you cannot have an `else` or `elif` without the original if-statement. An example is as follows.
```python
if number == 1:
  print('hello')
elif number == 2:
  print('world')
elif number == 3:
  print('hi')
else:
  print('bye')
```
In this code, if number is 1, then 'hello' is printed, if it is 2 then 'world' is printed, if it is 3 then 'hi' is printed, if `number` is any other value, then 'bye' will be printed. 

If-statements can also be **nested**, meaning that an if-statement can be placed inside of another if statement
```python
if a:
  if b:
    print('wow')`
```
In this case, 'wow' will only be printed if both if-statements evaluate to true. 
If you want a more detailed explanation on if-statements, you can go [here](http://anh.cs.luc.edu/handsonPythonTutorial/ifstatements.html)

## Loops
The final concept for these notes are loop. There are two fundamental types of loops we will be focusing on `for` and `while` loops.
Loops allow us to repeatedly execute a block of code.

### While Loops
A while loop can be used to repeatedly execute a block of code while a certain condition is true.
```python
while boolean_value:
  print('hello')
```
This code will keep printing 'hello' as long as the boolean_value is true. As soon as it is set to false, the loop will end.

An example of this use in practice is this simple program that prints the numbers from 1-10
```python
number = 1
while number <= 10:
  print(number)
  number += 1
```

In this program, the while loop will continue as long as number is less than or equal to 10. And, each iteration, number is incremented by 1, so it will reach 10 after 10 interations. 

### For loops
For loops allow us to repeat a bit of code a certain number of times.
```python
for i in range(100):
  print('hello')
```
This code will print 'hello' 100 times. Note here that `i` is a variable and this code will change the value of `i` during each iteration of the for loop. The first iteration, `i` will equal 0, and the last iteration it will equal 99. You may find it useful to use the value of `i` inside the loop, in the case that you wish your coding to behave differently during certain iterations of the loop.
I would recommend looking into the documentation for the `range` function [here](https://pynative.com/python-range-function/).

For loops have a wide range of applications, for example, you may find it useful to iterate over the items in a list.
```python
my_list = [1,2,3,4]
for item in my_list:
  print(item)
```
This code will print out the number 1,2,3,4 each on a new line (the `print` function adds a new line after it prints). On the first iteration of the loop, `my_list[0]` is stored in the `item` variable, in the second iteration `my_list[1]` is stored in `item` and so forth. 

Loops can also be used to iterate over the keys in a dictionary.
```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
for element in my_dict:
  print(my_dict[element])
```
Here, `element` will be given a key in the dictionary, so if we wish to print out all the values in the dictionary we must do `my_dict[element]` to get the value associated with `element`. 

You can find more notes on for loops [here](https://www.w3schools.com/python/python_for_loops.asp)

Similar to if-statements, loops can also be nested!

## Functions
Functions are python's equivalent of methods in java. A function can be used to group together a set of instructions so that they may be repeatedly called. A function often groups a set of instructions that work together to perform a specific task. So, rather than rewriting those instructinos everytime you wish to perform the task, you may simply invoke your functions. You have already seen several examples of function in the notes above such as `print`, `join`, `len`, `find` etc. These are examples of built-in functions since you do not have to define them in order to use them.

### User Defined Functions
In python, a user can define a function by using the `def` keyword. Here is an example of a function that will print out all the numbers from 0 to 99 each on a new line
```python
def print_numbers():
  for i in range(100):
    print(i)
```
If I wish to invoke this method, I would simply have to add `print_numbers()` in my program and this function will be executed. 

You may notice that there is a set of empty () after the name of my function. The () allow us to pass parameters into our functinos. A parameter is a value you can pass into the function. Here is an example
```python
def print_numbers(number_of_times):
  for i in range(number_of_times):
    print(i)
```
In this case, `number_of_times` is a parameter. When calling this function, I could do the following:
```python
print_numbers(10)
```
And this will print the numbers from 0 to 9. Note that you can also pass in multiple parameters to a function.
```python
def print_numbers(start_number, end_number):
  for i in range(start_number, end_number):
    print(i)
```
This function will print all the numbers from `start_number` up to but not including `end_number`. 

All the functions above simply perform an action but do not actually return a value. The keyword `return` can be used to end a function and pass back a value to whomever called the function. For example
```
def add(num1, num2):
  return num1 + num2
```
This function returns the sum of the two numbers. A person could call the function as follows:
```
value = add(2, 3)
print(value)
```
In this case, the value being returned by the add function is being stored in the value variable. 

We will go more in-depth regarding functions in lecture. You can find a more in-depth tutorial regarding functions [here](https://www.datacamp.com/community/tutorials/functions-python-tutorial?utm_source=adwords_ppc&utm_campaignid=1565261270&utm_adgroupid=67750485268&utm_device=c&utm_keyword=&utm_matchtype=b&utm_network=g&utm_adpostion=1t1&utm_creative=295208661496&utm_targetid=dsa-473406571355&utm_loc_interest_ms=&utm_loc_physical_ms=9022185&gclid=EAIaIQobChMI3OvDh5rw3wIVBbnACh27BQ6dEAAYASAAEgJkrvD_BwE).




This will conclude this week's pre-lecture notes, if you have any further questions, you are encouraged to Google them (the internet is your friend!) or ask them on piazza.
