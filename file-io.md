# Working with Files and User Input

So far, we have only been working with one type of program, mainly programs without inputs or parameters. A lot of times it useful to get some information from a user and use that for something. 

In Python, we can get input very easily. 

```python
name = input("what is your name : ")
print("Hello", name)
code = input("give me some python code : ")
print("Input was evaluated to : ", eval(code))
```

What would the result be if we input 
```python
[x*x for x in range(10)]
``` 

Now, do not use eval again since it is a security risk in practically every language. Ask yourself why.

Instead of taking in raw user input, we could do some further automation by taking in files as an input. There are also multiple ways to work with files. 

One thing we can do is open it similarly to how C works with files, is by opening and closing the file, by treating it similary like the input methods above. 

```python
my_file = open("etc.txt", "r")
print("filename : ", my_file.name)
my_file.close()
```

Another thing we can do is read and write to files.

```python
my_file = open("etc.txt", "r+")
my_file.write("this is cs196\n")
print("The first 10 bytes of this file are : ", my_file.read(10))
my_file.close()
```
Note - w and r+ are parameters that tell us what we are doing with the file, such as writing, reading, etc.

Just like regular command line capabilities, we can also do things like creating, renaming, deliting, etc. 

```python
import os
os.rename("etc.txt", "stuff.txt")
os.remove("stuff.txt")
```

There are other things we can do as well, and you can read up on it in the docs - https://www.tutorialspoint.com/python/python_files_io.htm

This was mainly to get a sense of the basics of what we can do in Python relating to files, which is practically everything (except maybe some lower level stuff that we only get in C, not in Python).

## Interesting things

Lets do something that seems pointless at first. We are going to make a new directory, and make some files, write some random 1s and 0s, then read these 1s and 0s as ASCII characters and see what we have. 

```python
import os
import random

os.mkdir("rascii")
os.chdir("rascii")

for i in range(8):
    file_name = str(i) + ".txt"
    f = open(file_name, "w")
    for _ in range(7):
        x = str(random.randint(0, 1))
        f.write(x)
    f.write("\n")

string = ""
for file_name in os.listdir(os.getcwd()):
    with open(file_name) as f:
        ascii = int(f.readline(),2 )
        string += chr(ascii)
    os.remove(file_name)

os.chdir("..")
os.rmdir("rascii")
print(string)
```

Comment the lines `os.chdir("..")` and `os.rmdir("rascii")` if you want to see what the files look like. However, this might cause errors in your program if you want to run it again.

Challenge - Figure out what this does before running it. This means googling some things that you do not know what are doing (this is a chance for you to improve your skills at reading code and googling). 

### Data processing

To transition into a little bit of whay we are going to be doing later on, let us look at some other stuff we can do with fileIO, that is useful. Imagine you are a TA for a class, and you are assigned with inputting all the grades for the semester. This includes 3 midterms, 15 homework assignments, and a final. You have all the raw data as a .csv file, but you also need to calculate the means, medians, maxs, and mins for the entire semester, for each exam and assignment. Since this is UIUC and not a small private school, we have a class size of 1000 students. Doing this by hand is going to take your entire day, or you remember that you took 196 and can do this in 20 minutes. 

```python
import os, csv, random
from statistics import mean, median
# Some code to simulate grades. 

def get_line(index, name, info):
	line = []
	line.append(name)
	if index == -1:
		line.append(info["max"])
		line.append(info["min"])
		line.append(info["mean"])
		line.append(info["median"])
	else: 
		line.append(info["max"])
		line.append(info["min"])
		line.append(info["mean"])
		line.append(info["median"])
	return line

def get_info(scores):
	info = {}
	info["max"] = max(scores)
	info["min"] = min(scores)
	info["mean"] = mean(scores)
	info["median"] = median(scores)
	return info

def main():
	write_files()
	read_files()
	return 

def write_files():
	
	try:
		os.mkdir("final_grades")
		os.chdir("final_grades")
	except :
		os.chdir("final_grades")
		return
	
	assignments = {}
	midterms = {}
	final = []

	for i in range(15):
		assignments[i] = [random.randint(0, 10) for _ in range(1000)]

	for i in range(3):
		midterms[i] = [random.randint(0, 100) for _ in range(1000)]

	final = [random.randint(0,200) for _ in range(1000)]

	for i in range(15):
		file_name = "assignment" + str(i) + ".csv"
		with open(file_name, "w") as f:
			file_writer = csv.writer(f, delimiter=',')

			file_writer.writerow(["NetId", "Grade"])
			for netid in range(1000):
				file_writer.writerow([netid, assignments[i][netid]])
	
	for i in range(3):
		file_name = "midterm" + str(i) + ".csv"
		with open(file_name, "w") as f:	
			file_writer = csv.writer(f, delimiter=',')
			file_writer.writerow(['NetId', 'Grade'])

			for netid in range(1000):
				file_writer.writerow([netid, midterms[i][netid]])

	file_name = "final.csv"
	with open(file_name, "w") as f:
		file_writer = csv.writer(f, delimiter=',')

		for netid in range(1000):
			
			file_writer.writerow([netid, final[netid]])

def read_files():
	assignment_info = {}
	midterm_info = {}
	final_info = {}

	for i in range(15):
		file_name = "assignment" + str(i) + ".csv"
		with open(file_name, "r") as f:
			reader = csv.reader(f)
			next(reader, None)
			scores = [int(row[1]) for row in reader]
			assignment_info[i] = get_info(scores)

	for i in range(3):
		file_name = "midterm" + str(i) + ".csv"
		with open(file_name, "r") as f:
			reader = csv.reader(f)
			next(reader, None)
			scores = [int(row[1]) for row in reader]
			midterm_info[i] = get_info(scores)

	with open("final.csv", "r") as f:
		reader = csv.reader(f)
		next(reader, None)
		scores = [int(row[1]) for row in reader]
		final_info = get_info(scores)

	try:
		os.remove("semester_info.csv")
	except:
		pass

	with open("semester_info.csv", "w") as f:
		file_writer = csv.writer(f, delimiter=",")
		file_writer.writerow(["Work", "max", "min", "mean", "median"])

		for i in range(15):
			file_writer.writerow(get_line(i, "assignment " + str(i), assignment_info[i]))

		for i in range(3):
			file_writer.writerow(get_line(i, "midterm " + str(i), midterm_info[i]))

		file_writer.writerow(get_line(-1, "final", final_info))


if __name__ == "__main__":
	main()
```

Once again, read this and figure out what it is doing. Play around with the code as well to learn some more about it.