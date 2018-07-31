
# Try Statement
We can use try statements to handle exceptions. There are four clauses you can use (one more in addition to those shown in the video).

`try`: This is the only mandatory clause in a try statement. The code in this block is the first thing that Python runs in a try statement.
`except`: If Python runs into an exception while running the try block, it will jump to the except block that handles that exception.
`else`: If Python runs into no exceptions while running the try block, it will run the code in this block after running the try block.
`finally`: Before Python leaves this try statement, it will run the code in this finally block under any conditions, even if it's ending the program. E.g., if Python ran into an error while running code in 


# Specifying Exceptions
We can actually specify which error we want to handle in an except block like this:
```python
try:
    # some code
except ValueError:
    # some code
```
Now, it catches the ValueError exception, but not other exceptions. If we want this handler to address more than one type of exception, we can include a tuple after the except with the exceptions.
```python
try:
    # some code
except ValueError, KeyboardInterrupt:
    # some code
```
Or, if we want to execute different blocks of code depending on the exception, you can have multiple except blocks.
```python
try:
    # some code
except ValueError:
    # some code
except KeyboardInterrupt:
    # some code
```
```python
def party_planner(cookies, people):
    leftovers = None
    num_each = None

    try:
        num_each = cookies // people
        leftovers = cookies % people
    except ZeroDivisionError:
        print("Oops, you entered 0 people will be attending.")
        print("Please enter a good number of people for a party.")

    return(num_each, leftovers)
```

</br>

# Accessing Error Messages
When you handle an exception, you can still access its error message like this:

try:
```python
    # some code
except ZeroDivisionError as e:
   # some code
   print("ZeroDivisionError occurred: {}".format(e))
```   
This would print something like this:
```python
ZeroDivisionError occurred: integer division or modulo by zero
So you can still access error messages, even if you handle them to keep your program from crashing!
```
If you don't have a specific error you're handling, you can still access the message like this:

try:
```python
    # some code
except Exception as e:
   # some code
   print("Exception occurred: {}".format(e))
```
Exception is just the base class for all built-in exceptions. You can learn more about Python's exceptions [here](https://docs.python.org/3/library/exceptions.html#bltin-exceptions).


</br>

</br>

</br>
___

# Reading and Writing Files
To follow along with the example above, create a new file in Atom, copy the following text into it, and save it as some_file.txt!
```
Hello!!

You've read the contents of this file!
Here's how we read and write files in Python.
```

# Reading a File
```
f = open('my_path/my_file.txt', 'r')
file_data = f.read()
f.close()
```
1. First open the file using the built-in function, open. This requires a string that shows the path to the file. The open function returns a file object, which is a Python object through which Python interacts with the file itself. Here, we assign this object to the variable f.
2. There are optional parameters you can specify in the open function. One is the mode in which we open the file. Here, we use r or read only. This is actually the default value for the mode argument.
3. Use the read method to access the contents from the file object. This read method takes the text contained in a file and puts it into a string. Here, we assign the string returned from this method into the variable file_data.
4. When finished with the file, use the close method to free up any system resources taken up by the file.

# Writing to a File
```
f = open('my_path/my_file.txt', 'w')
f.write("Hello there!")
f.close()
```
1.Open the file in writing ('w') mode. If the file does not exist, Python will create it for you. If you open an existing file in writing mode, any content that it had contained previously will be deleted. If you're interested in adding to an existing file, without deleting its content, you should use the append ('a') mode instead of write.
2. Use the write method to add text to the file.
3. Close the file when finished.


# Too Many Open Files
Run the following script in Python to see what happens when you open too many files without closing them!

```
files = []
for i in range(10000):
    files.append(open('some_file.txt', 'r'))
    print(i)
```

#With
Python provides a special syntax that auto-closes a file for you once you're finished using it.

```
with open('my_path/my_file.txt', 'r') as f:
    file_data = f.read()
```


_____

Let's see this in an example that uses the following file, camelot.txt:
```
We're the knights of the round table
We dance whenever we're able
```
Here's a script that reads in the file a little at a time by passing an integer argument to .read().
```python
with open("camelot.txt") as song:
    print(song.read(2))
    print(song.read(8))
    print(song.read())
```
Outputs:
```
We
're the 
knights of the round table
We dance whenever we're able
```

Conveniently, Python will loop over the lines of a file using the syntax for line in file. I can use this to create a list of lines in the file. Because each line still has its newline character attached, I remove this using .strip().
```python
camelot_lines = []
with open("camelot.txt") as f:
    for line in f:
        camelot_lines.append(line.strip())

print(camelot_lines)
```
Outputs:
```
["We're the knights of the round table", "We dance whenever we're able"]
```

```python
Flying Circus Cast List
def create_cast_list(filename):
    cast_list = []
    with open(filename) as f:
        for line in f:
            name = line.split(",")[0]
            cast_list.append(name)

    return cast_list

cast_list = create_cast_list('flying_circus_cast.txt')
for actor in cast_list:
    print(actor)
```
Output:
```
Graham Chapman
Eric Idle
Terry Jones
Michael Palin
Terry Gilliam
John Cleese
Carol Cleveland
Ian Davidson
```


____

# Importing Local Scripts

```python
import useful_functions
```

It's the standard convention for import statements to be written at the top of a Python script, each one on a separate line.

```python
import useful_functions
useful_functions.add_five([1, 2, 3, 4])
```

We can add an alias to an imported module to reference it with a different name.

```python
import useful_functions as uf
uf.add_five([1, 2, 3, 4])
```

# Try It Out!
Here's the code I used in the video above. Create these scripts in the same directory and run them in your terminal! Experiment with the if main block and accessing objects from the imported module!

```python
# demo.py

import useful_functions as uf

scores = [88, 92, 79, 93, 85]

mean = uf.mean(scores)
curved = uf.add_five(scores)

mean_c = uf.mean(curved)

print("Scores:", scores)
print("Original Mean:", mean, " New Mean:", mean_c)

print(__name__)
print(uf.__name__)
```
```python
# useful_functions.py

def mean(num_list):
    return sum(num_list) / len(num_list)

def add_five(num_list):
    return [n + 5 for n in num_list]

def main():
    print("Testing mean function")
    n_list = [34, 44, 23, 46, 12, 24]
    correct_mean = 30.5
    assert(mean(n_list) == correct_mean)

    print("Testing add_five function")
    correct_list = [39, 49, 28, 51, 17, 29]
    assert(add_five(n_list) == correct_list)

    print("All tests passed!")

if __name__ == '__main__':
    main()
```

Importing password and choose 3 random ones

```python
# Use an import statement at the top
import random
    
word_file = "words.txt"
word_list = []

#fill up the word_list
with open(word_file,'r') as words:
	for line in words:
		# remove white space and make everything lowercase
		word = line.strip().lower()
		# don't include words that are too long or too short
		if 3 < len(word) < 8:
			word_list.append(word)

# Add your function generate_password here
# It should return a string consisting of three random words 
# concatenated together without spaces
num = 0
def generate_password():
    string = ""
    string = random.choice(word_list) + random.choice(word_list) + random.choice(word_list)
    # string = "".join(random.sample(word_list,3))
    return string


# test your function
print(generate_password())
```

</br>
# Our favourite modules
The Python Standard Library has a lot of modules! To help you get familiar with what's available, here are a selection of our favourite Python Standard Library modules and why we use them!

`csv`: very convenient for reading and writing csv files

`collections`: useful extensions of the usual data types including OrderedDict, defaultdict and namedtuple

`random`: generates pseudo-random numbers, shuffles sequences randomly and chooses random items

`string`: more functions on strings. This module also contains useful collections of letters like string.digits (a string containing all characters which are valid digits).

`re`: pattern-matching in strings via regular expressions

`math`: some standard mathematical functions

`os`: interacting with operating systems

`os.path`: submodule of os for manipulating path names

`sys`: work directly with the Python interpreter

`json`: good for reading and writing json files (good for web work)


______

# Techniques for Importing Modules
There are other variants of import statements that are useful in different situations.

1. To import an individual function or class from a module:

    `from module_name import object_name`

2. To import multiple individual objects from a module:

    `from module_name import first_object, second_object`

3. To rename a module:

    `import module_name as new_name`

4. To import an object from a module and rename it:

    `from module_name import object_name as new_name`

5. To import every object individually from a module (DO NOT DO THIS):

    `from module_name import *`

6. If you really want to use all of the objects from a module, use the standard import module_name statement instead and access each of the objects with the dot notation.

    `import module_name`

</br>

# Modules, Packages, and Names
In order to manage the code better, modules in the Python Standard Library are split down into sub-modules that are contained within a package. A package is simply a module that contains sub-modules. A sub-module is specified with the usual dot notation.

Modules that are submodules are specified by the package name and then the submodule name separated by a dot. You can import the submodule like this.

`import package_name.submodule_name`


</br>

# [Useful Third-Party Packages](https://docs.google.com/document/d/1g6ll5HzrxIM4rrdaXMvISCAGmrNDaCQLqNLUi0U0soU/edit#heading=h.i3sovhpbc4la)

To install a package using pip, just enter "pip install" followed by the name of the package in your command line like this: 

`pip install package_name`