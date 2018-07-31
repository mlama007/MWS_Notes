Arithmetic Operators
Arithmetic operators
+ Addition
- Subtraction
* Multiplication
/ Division
% Mod (the remainder after dividing)
** Exponentiation (note that ^ does not do this operation, as you might have seen in other languages)
// Divides and rounds down to the nearest integer

Variables I
Variables are used all the time in Python! Below is the example you saw in the video where we performed the following:
mv_population = 74728
Variables II
In this video you saw that the following two are equivalent in terms of assignment:
x = 3
y = 4
z = 5


and
x, y, z = 3, 4, 5


Integers and Floats
There are two Python data types that could be used for numeric values:
int - for integer values
float - for decimal or floating point values
You can create a value that follows the data type by using the following syntax:
x = int(4.7)   # x is now an integer 4
y = float(4)   # y is now a float of 4.0


You can check the type by using the type function:
>>> print(type(x))
int
>>> print(type(y))
float


Because the float, or approximation, for 0.1 is actually slightly more than 0.1, when we add several of them together we can see the difference between the mathematically correct answer and the one that Python creates.
>>> print(.1 + .1 + .1 == .3)
False


You can see more on this here.




Booleans, Comparison Operators, and Logical Operators
The bool data type holds one of the values True or False, which are often encoded as 1 or 0, respectively.
There are 6 comparison operators that are common to see in order to obtain a bool value:
Comparison Operators
Symbol Use Case
Bool
Operation
5 < 3
False
Less Than
5 > 3
True
Greater Than
3 <= 3
True
Less Than or Equal To
3 >= 5
False
Greater Than or Equal To
3 == 5
False
Equal To
3 != 5
True
Not Equal To
And there are three logical operators you need to be familiar with:
Logical Use
Bool
Operation
5 < 3 and 5 == 5
False
and - Evaluates if all provided statements are True
5 < 3 or 5 == 5
True
or - Evaluates if at least one of many statements is True
not 5 < 3
True
not - Flips the Bool Value
Here is more information on how George Boole changed the world!


Strings
Strings in Python are shown as the variable type str. You can define a string with either double quotes "or single quotes '. If the string you are creating actually has one of these two values in it, then you need to be careful to assure your code doesn't give an error.
>>> my_string = 'this is a string!'
>>> my_string2 = "this is also a string!!!"


You can also include a \ in your string to be able to include one of these quotes:
>>> this_string = 'Simon\'s skateboard is in the garage.'
>>> print(this_string)


Simon's skateboard is in the garage.


If we don't use this, notice we get the following error:
>>> this_string = 'Simon's skateboard is in the garage.'


 File "<ipython-input-20-e80562c2a290>", line 1
    this_string = 'Simon's skateboard is in the garage.'
                         ^
SyntaxError: invalid syntax


The color highlighting is also an indication of the error you have in your string in this second case. There are a number of other operations you can use with strings as well. In this video you saw a few:
>>> first_word = 'Hello'
>>> second_word = 'There'
>>> print(first_word + second_word)

HelloThere

>>> print(first_word + ' ' + second_word)

Hello There

>>> print(first_word * 5)

HelloHelloHelloHelloHello

>>> print(len(first_word))

5


Unlike the other data types you have seen so far, you can also index into strings, but you will see more on this soon! For now, here is a small example. Notice Python uses 0 indexing - we will discuss this later in this lesson in detail.
>>> first_word[0]

H

>>> first_word[1]

e


The len() function
len() is a built-in Python function that returns the length of an object, like a string. The length of a string is the number of characters in the string. This will always be an integer.
There is an example above, but here's another one:
print(len("ababa") / len("ab"))
2.5


You know what the data types are for len("ababa") and len("ab"). Notice the data type of their resulting quotient here.


Type And Type Conversion
You have seen four data types so far:
int
float
bool
string
You got a quick look at type() from an earlier video, and it can be used to check the data type of any variable you are working with.
>>> print(type(4))
int
>>> print(type(3.7))
float
>>> print(type('this'))
str
>>> print(type(True))
bool


You saw that you can change variable types to perform different operations. For example,
"0" + "5"


provides completely different output than
0 + 5


What do you think the below would provide?
"0" + 5


How about the code here:
0 + "5"


Checking your variable types is really important to assure that you are retrieving the results you want when programming.















________________


# String Methods
```python
len("this")
type(12)
print("Hello world")
```

These three above are functions - notice they use parentheses, and accept one or more arguments. Functions will be studied in much more detail in a later lesson!

A method in Python behaves similarly to a function. Methods actually are functions that are called using dot notation. For example, `lower()` is a string method that can be used like this, on a string called "sample string": `sample_string.lower()`.

Methods are specific to the data type for a particular variable. So there are some built-in methods that are available for all strings, different methods that are available for all integers, etc.


Each of these methods accepts the string itself as the first argument of the method. However, they also could receive additional arguments, that are passed inside the parentheses. Let's look at the output for a few examples.

```python
my_string.islower()
True
my_string.count('a')
2
my_string.find('a')
3
```

You can see that the count and find methods both take another argument. However, the .islower() method does not accept another argument.

No professional has all the methods memorized, which is why understanding how to use documentation and find answers is so important. Gaining a strong grasp of the foundations of programming will allow you to use those foundations to use documentation to build so much more than someone who tries to memorize all the built-in methods in Python.

## One important string method: `format()`
We will be using the format() string method a good bit in our future work in Python, and you will find it very valuable in your coding, especially with your print statements.

We can best illustrate how to use format() by looking at some examples:

# Example 1
```python
print("Mohammed has {} balloons".format(27))
Mohammed has 27 balloons
```

# Example 2
```python
animal = "dog"
action = "bite"
print("Does your {} {}?".format(animal, action))
Does your dog bite?
```
# Example 3
```python
maria_string = "Maria loves {} and {}"
print(maria_string.format("math","statistics"))
Maria loves math and statistics
```
Notice how in each example, the number of pairs of curly braces {} you use inside the string is the same as the number of replacements you want to make using the values inside format().

More advanced students can learn more about the formal syntax for using the format() string method [here](https://docs.python.org/3.6/library/string.html#format-string-syntax).


</br>

# Lists!
You saw here that you can create a list with square brackets. Lists can contain any mix and match of the data types you have seen so far.
```python
list_of_random_things = [1, 3.4, 'a string', True]
```

This is a list of 4 elements. All ordered containers (like lists) are indexed in python using a starting index of 0. Therefore, to pull the first value from the above list, we can write:
```python
>>> list_of_random_things[0]
1
```
It might seem like you can pull the last element with the following code, but this actually won't work:

```python
>>> list_of_random_things[len(list_of_random_things)] 
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-34-f88b03e5c60e> in <module>()
----> 1 lst[len(lst)]

IndexError: list index out of range
```

However, you can retrieve the last element by reducing the index by 1. Therefore, you can do the 
following:

```python
>>> list_of_random_things[len(list_of_random_things) - 1] 
True
```

Alternatively, you can index from the end of a list by using negative values, where -1 is the last element, -2 is the second to last element and so on.

```python
>>> list_of_random_things[-1] 
True
>>> list_of_random_things[-2] 
a string
```

</br>

# Slice and Dice with Lists
You saw that we can pull more than one value from a list at a time by using slicing. When using slicing, it is important to remember that the lower index is inclusive and the upper index is exclusive.

Therefore, this:
```python
>>> list_of_random_things = [1, 3.4, 'a string', True]
>>> list_of_random_things[1:2]
[3.4]
```
will only return 3.4 in a list. Notice this is still different than just indexing a single element, because you get a list back with this indexing. The colon tells us to go from the starting value on the left of the colon up to, but not including, the element on the right.

If you know that you want to start at the beginning, of the list you can also leave out this value.

```python
>>> list_of_random_things[:2]
[1, 3.4]
```

or to return all of the elements to the end of the list, we can leave off a final element.

```python
>>> list_of_random_things[1:]
[3.4, 'a string', True]
```

This type of indexing works exactly the same on strings, where the returned value will be a string.

## Are you `in` OR `not in`?

You saw that we can also use in and not in to return a bool of whether an element exists within our list, or if one string is a substring of another.

```python
>>> 'this' in 'this is a string'
True
>>> 'in' in 'this is a string'
True
>>> 'isa' in 'this is a string'
False
>>> 5 not in [1, 2, 3, 4, 6]
True
>>> 5 in [1, 2, 3, 4, 6]
False
```


# Mutability and Order
Mutability is about whether or not we can change an object once it has been created. If an object (like a list or string) can be changed (like a list can), then it is called mutable. However, if an object cannot be changed with creating a completely new object (like strings), then the object is considered immutable.

```python
>>> my_lst = [1, 2, 3, 4, 5]
>>> my_lst[0] = 'one'
>>> print(my_lst)
['one', 2, 3, 4, 5]
```

As shown above, you are able to replace 1 with 'one' in the above list. This is because lists are mutable.

However, the following does not work:

```python
>>> greeting = "Hello there"
>>> greeting[0] = 'M'
```

This is because strings are immutable. This means to change this string, you will need to create a completely new string.

There are two things to keep in mind for each of the data types you are using:

1. Are they mutable?
2. Are they ordered?


Both strings and lists are ordered. However, you will see some data types in the next sections that will be unordered. For each of the upcoming data structures you see, it is useful to understand how you index, are they mutable, and are they ordered. Knowing this about the data structure is really useful!

Additionally, you will see how these each have different methods, so why you would use one data structure vs. another is largely dependent on these properties, and what you can easily do with it!


# Useful Functions for Lists I
1. `len()` returns how many elements are in a list.
2. `max()` returns the greatest element of the list. How the greatest element is determined depends on what type objects are in the list. The maximum element in a list of numbers is the largest number. The maximum elements in a list of strings is element that would occur last if the list were sorted alphabetically. This works because the the max function is defined in terms of the greater than comparison operator. The max function is undefined for lists that contain elements from different, incomparable types.
3. `min()` returns the smallest element in a list. min is the opposite of max, which returns the largest element in a list.
4. `sorted()` returns a copy of a list in order from smallest to largest, leaving the list unchanged.


# Useful Functions for Lists II

`join method`
Join is a string method that takes a list of strings as an argument, and returns a string consisting of the list elements joined by a separator string.

```python
new_str = "\n".join(["fore", "aft", "starboard", "port"])
print(new_str)
```

Output:
```
fore
aft
starboard
port
```
In this example we use the string "\n" as the separator so that there is a newline between each element. We can also use other strings as separators with .join. Here we use a hyphen.
```python
name = "-".join(["García", "O'Kelly"])
print(name)
```
Output:
```
García-O'Kelly
```
It is important to remember to separate each of the items in the list you are joining with a comma (,). Forgetting to do so will not trigger an error, but will also give you unexpected results.

`append method`

A helpful method called append adds an element to the end of a list.
```python
letters = ['a', 'b', 'c', 'd']
letters.append('z')
print(letters)
```
Output:
```
['a', 'b', 'c', 'd', 'z']
```

```python
names = ["Carol", "Albert", "Ben", "Donna"]
names.append("Eugenia")

print(" & ".join(sorted(names)))

print(sorted(names))

print(" & ".join(sorted(names)))
```
`Albert & Ben & Carol & Donna`

``` ['Albert', 'Ben', 'Carol', 'Donna', 'Eugenia'] ```

`Albert & Ben & Carol & Donna`


----
# Tuples
A tuple is another useful container. It's a data type for immutable ordered sequences of elements. They are often used to store related pieces of information. Consider this example involving latitude and longitude:
```python
location = (13.4125, 103.866667)
print("Latitude:", location[0])
print("Longitude:", location[1])
```

Tuples are similar to lists in that they store an ordered collection of objects which can be accessed by their indices. Unlike lists, however, tuples are immutable - you can't add and remove items from tuples, or sort them in place.

Tuples can also be used to assign multiple variables in a compact way.
```python
dimensions = 52, 40, 100
length, width, height = dimensions
print("The dimensions are {} x {} x {}".format(length, width, height))
```

The parentheses are optional when defining tuples, and programmers frequently omit them if parentheses don't clarify the code.

In the second line, three variables are assigned from the content of the tuple dimensions. This is called tuple unpacking. You can use tuple unpacking to assign the information from a tuple into multiple variables without having to access them one by one and make multiple assignment statements.

If we won't need to use dimensions directly, we could shorten those two lines of code into a single line that assigns three variables in one go!

```python
length, width, height = 52, 40, 100
print("The dimensions are {} x {} x {}".format(length, width, height))
```

---
# Sets
A set is a data type for mutable unordered collections of unique elements. One application of a set is to quickly remove duplicates from a list.

numbers = [1, 2, 6, 3, 1, 1, 6]
unique_nums = set(numbers)
print(unique_nums)
This would output:

```python
{1, 2, 3, 6}
```

Sets support the in operator the same as lists do. You can add elements to sets using the add method, and remove elements using the pop method, similar to lists. Although, when you pop an element from a set, a random element is removed. Remember that sets, unlike lists, are unordered so there is no "last element".

```python
fruit = {"apple", "banana", "orange", "grapefruit"}  # define a set

print("watermelon" in fruit)  # check for element

fruit.add("watermelon")  # add an element
print(fruit)

print(fruit.pop())  # remove a random element
print(fruit)
```
This outputs:
```
False
{'grapefruit', 'orange', 'watermelon', 'banana', 'apple'}
grapefruit
{'orange', 'watermelon', 'banana', 'apple'}
```
Other operations you can perform with sets include those of mathematical sets. Methods like union, intersection, and difference are easy to perform with sets, and are much faster than such operators with other containers.

---
# Dictionaries And Identity Operators
Dictionaries
A dictionary is a mutable data type that stores mappings of unique keys to values. Here's a dictionary that stores elements and their atomic numbers.

```python
elements = {"hydrogen": 1, "helium": 2, "carbon": 6}
```

Dictionaries can have keys of any immutable type, like integers or tuples, not just strings. It's not even necessary for every key to have the same type! We can look up values or insert new values in the dictionary using square brackets that enclose the key.

```python
print(elements["helium"])  # print the value mapped to "helium"
elements["lithium"] = 3  # insert "lithium" with a value of 3 into the dictionary
```

We can check whether a value is in a dictionary the same way we check whether a value is in a list or set with the in keyword. Dicts have a related method that's also useful, get. get looks up values in a dictionary, but unlike square brackets, get returns None (or a default value of your choice) if the key isn't found.

```python
print("carbon" in elements)
print(elements.get("dilithium"))
```
This would output:
```
True
None
```

Carbon is in the dictionary, so True is printed. Dilithium isn’t in our dictionary so None is returned by get and then printed. If you expect lookups to sometimes fail, get might be a better tool than normal square bracket lookups because errors can crash your program.

## Identity Operators
Keyword	    |              Operator
	    | 

| Keyword       | Operator      
| ------------- |:-------------
| `is`          | evaluates if both sides have the same identity
| `is not`      | evaluates if both sides have different identities

</br>

You can check if a key returned None with the is operator. You can check for the opposite using is not.

```python
n = elements.get("dilithium")
print(n is None)
print(n is not None)
```
This would output:
```
True
False
```

---
# Compound Data Structures
We can include containers in other containers to create compound data structures. For example, this dictionary maps keys to values that are also dictionaries!
```python
elements = {"hydrogen": {"number": 1,
                         "weight": 1.00794,
                         "symbol": "H"},
              "helium": {"number": 2,
                         "weight": 4.002602,
                         "symbol": "He"}}
```
We can access elements in this nested dictionary like this.

helium = elements["helium"]  # get the helium dictionary
hydrogen_weight = elements["hydrogen"]["weight"]  # get hydrogen's weight
You can also add a new key to the element dictionary.

```python
oxygen = {"number":8,"weight":15.999,"symbol":"O"}  # create a new oxygen dictionary 
elements["oxygen"] = oxygen  # assign 'oxygen' as a key to the elements dictionary
print('elements = ', elements)
```
Output is:
```
elements =  {"hydrogen": {"number": 1,
                          "weight": 1.00794,
                          "symbol": 'H'},
               "helium": {"number": 2,
                          "weight": 4.002602,
                          "symbol": "He"}, 
               "oxygen": {"number": 8, 
                          "weight": 15.999, 
                          "symbol": "O"}}
```


# [Python challenges](https://www.hackerrank.com/domains/python)

# Data Structures
There are a number of built in python data structures that you will use all the time when programming. You can find a table of them available below:


| Data       | Ordered      | Mutable    | Constructor    | Example      
| ----------|:-------------|:-------------|:-------------|:-------------
int	| NA	| NA	| int()	| 5
float	|NA|	NA	| float()	|6.5
string	| Yes|	No | ' ' or " " or str()	|"this is a string"
bool	|NA	|NA	|NA	|True or False
list    |Yes	|Yes	|[ ] or list()	|[5, 'yes', 5.7]
tuple|	|Yes	|No	|( ) or tuple()	|(5, 'yes', 5.7)
set	    |No	    |Yes	|{ } or set()	|{5, 'yes', 5.7}
dictionary	|No	    |Keys: No	|{ } or dict()	|{'Jun':75, 'Jul':89}

</br>
----
# Control Flow
Welcome to this lesson on Control Flow! Control flow is the sequence in which your code is run. Here, we'll learn about several tools in Python we can use to affect our code's control flow:

Conditional Statements
Boolean Expressions
For and While Loops
Break and Continue
Zip and Enumerate
List Comprehensions


# If Statement
An if statement is a conditional statement that runs or skips code based on whether a condition is true or false. Here's a simple example.

```python
if phone_balance < 5:
    phone_balance += 10
    bank_balance -= 10
```

Let's break this down.

1 . An if statement starts with the if keyword, followed by the condition to be checked, in this case phone_balance < 5, and then a colon. The condition is specified in a boolean expression that evaluates to either True or False.
2. After this line is an indented block of code to be executed if that condition is true. Here, the lines that increment phone_balance and decrement bank_balance only execute if it is true that phone_balance is less than 5. If not, the code in this if block is simply skipped.

## Use Comparison Operators in Conditional Statements
You have learned about Python's comparison operators (e.g. == and !=) and how they are different from assignment operators (e.g. =). In conditional statements, you want to use comparison operators. For example, you'd want to use if x == 5 rather than if x = 5. If your conditional statement is causing a syntax error or doing something unexpected, check whether you have written == or =!

# If, Elif, Else
In addition to the if clause, there are two other optional clauses often used with an if statement. For example:

```python
if season == 'spring':
    print('plant the garden!')
elif season == 'summer':
    print('water the garden!')
elif season == 'fall':
    print('harvest the garden!')
elif season == 'winter':
    print('stay indoors!')
else:
    print('unrecognized season')
```

1. if: An if statement must always start with an if clause, which contains the first condition that is checked. If this evaluates to True, Python runs the code indented in this if block and then skips to the rest of the code after the if statement.

2. elif: elif is short for "else if." An elif clause is used to check for an additional condition if the conditions in the previous clauses in the if statement evaluate to False. As you can see in the example, you can have multiple elif blocks to handle different situations.

3. else: Last is the else clause, which must come at the end of an if statement if used. This clause doesn't require a condition. The code in an else block is run if all conditions above that in the if statement evaluate to False.

# Indentation
Some other languages use braces to show where blocks of code begin and end. In Python we use indentation to enclose blocks of code. For example, if statements use indentation to tell Python what code is inside and outside of different clauses.

In Python, indents conventionally come in multiples of four spaces. Be strict about following this convention, because changing the indentation can completely change the meaning of the code. If you are working on a team of Python programmers, it's important that everyone follows the same indentation convention!

## Spaces or Tabs?
The Python Style Guide recommends using 4 spaces to indent, rather than using a tab. Whichever you use, be aware that "Python 3 disallows mixing the use of tabs and spaces for indentation."

# Complex Boolean Expressions
If statements sometimes use more complicated boolean expressions for their conditions. They may contain multiple comparisons operators, logical operators, and even calculations. Examples:
```python
if 18.5 <= weight / height**2 < 25:
    print("BMI is considered 'normal'")

if is_raining and is_sunny:
    print("Is there a rainbow?")

if (not unsubscribed) and (location == "USA" or location == "CAN"):
    print("send email")
```
For really complicated conditions you might need to combine some ands, ors and nots together. Use parentheses if you need to make the combinations clear.

However simple or complex, the condition in an if statement must be a boolean expression that evaluates to either True or False and it is this value that decides whether the indented block in an if statement executes or not.


# Good and Bad Examples
Here are some things to keep in mind while writing boolean expressions for your if statements.

1. Don't use True or False as conditions
## Bad example
```python
if True:
    print("This indented code will always get run.")
```
While "True" is a valid boolean expression, it's not useful as a condition since it always evaluates to True, so the indented code will always get run. Similarly, if False is not a condition you should use either - the statement following this if statement would never be executed.

### Another bad example
```python
if is_cold or not is_cold:
    print("This indented code will always get run.")
```

Similarly, it's useless to use any condition that you know will always evaluate to True, like this example above. A boolean variable can only be True or False, so either is_cold or not is_cold is always True, and the indented code will always be run.

2. Be careful writing expressions that use logical operators
Logical operators and, or and not have specific meanings that aren't quite the same as their meanings in plain English. Make sure your boolean expressions are being evaluated the way you expect them to.

## Bad example
```python
if weather == "snow" or "rain":
    print("Wear boots!")
```

This code is valid in Python, but it is not a boolean expression, although it reads like one. The reason is that the expression to the right of the or operator, "rain", is not a boolean expression - it's a string! Later we'll discuss what happens when you use non-boolean-type objects in place of booleans.

3. Don't compare a boolean variable with == True or == False
This comparison isn’t necessary, since the boolean variable itself is a boolean expression.

## Bad example
```python
if is_cold == True:
    print("The weather is cold!")
```
This is a valid condition, but we can make the code more readable by using the variable itself as the condition instead, as below.

## Good example
```python
if is_cold:
    print("The weather is cold!")
```
If you want to check whether a boolean is False, you can use the not operator.


# Truth Value Testing
If we use a non-boolean object as a condition in an if statement in place of the boolean expression, Python will check for its truth value and use that to decide whether or not to run the indented code. By default, the truth value of an object in Python is considered True unless specified as False in the documentation.

Here are most of the built-in objects that are considered False in Python:

constants defined to be false: None and False
zero of any numeric type: 0, 0.0, 0j, Decimal(0), Fraction(0, 1)
empty sequences and collections: '"", (), [], {}, set(), range(0)
Example:

```python
errors = 3
if errors:
    print("You have {} errors to fix!".format(errors))
else:
    print("No errors to fix!")
```

In this code, errors has the truth value True because it's a non-zero number, so the error message is printed. This is a nice, succinct way of writing an if statement.

</br>

</br>

----
# For Loops
Python has two kinds of loops - for loops and while loops. A for loop is used to "iterate", or do something repeatedly, over an iterable.

An iterable is an object that can return one of its elements at a time. This can include sequence types, such as strings, lists, and tuples, as well as non-sequence types, such as dictionaries and files.

Example
Let's break down the components of a for loop, using this example with the list cities:
```python
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']
for city in cities:
    print(city)
print("Done!")
```

## Components of a For Loop
1. The first line of the loop starts with the for keyword, which signals that this is a for loop
2. Following that is city in cities, indicating city is the iteration variable, and cities is the iterable being looped over. In the first iteration of the loop, city gets the value of the first element in cities, which is “new york city”.
3. The for loop heading line always ends with a colon :
4. Following the for loop heading is an indented block of code, the body of the loop, to be executed in each iteration of this loop. There is only one line in the body of this loop - print(city).
5. After the body of the loop has executed, we don't move on to the next line yet; we go back to the for heading line, where the iteration variable takes the value of the next element of the iterable. In the second iteration of the loop above, city takes the value of the next element in cities, which is "mountain view".
6. This process repeats until the loop has iterated through all the elements of the iterable. Then, we move on to the line that follows the body of the loop - in this case, print("Done!"). We can tell what the next line after the body of the loop is because it is unindented. Here is another reason why paying attention to your indentation is very important in Python!


Executing the code in the example above produces this output:
```
new york city
mountain view
chicago
los angeles
```

Done!

You can name iteration variables however you like. A common pattern is to give the iteration variable and iterable the same names, except the singular and plural versions respectively (e.g., 'city' and 'cities').

Using the Range() Function with For Loops
range() is a built-in function used to create an iterable sequence of numbers. You will frequently use range() with a for loop to repeat an action a certain number of times, as in this example:
```python
for i in range(3):
    print("Hello!")
```
Output:
```
Hello!
Hello!
Hello!
```
` range(start=0, stop, step=1)`

The range() function takes three integer arguments, the first and third of which are optional:

* The 'start' argument is the first number of the sequence. If unspecified, 'start' defaults to 0.
* The 'stop' argument is 1 more than the last number of the sequence. This argument must be specified.
* The 'step' argument is the difference between each number in the sequence. If unspecified, 'step' defaults to 1.

Notes on using range():

* If you specify one integer inside the parentheses withrange(), it's used as the value for 'stop,' and the defaults are used for the other two.

    `e.g. - range(4) returns 0, 1, 2, 3`

* If you specify two integers inside the parentheses withrange(), they're used for 'start' and 'stop,' and the default is used for 'step.'

    `e.g. - range(2, 6) returns 2, 3, 4, 5`

* Or you can specify all three integers for 'start', 'stop', and 'step.'

    `e.g. - range(1, 10, 2) returns 1, 3, 5, 7, 9`

Creating and Modifying Lists
In addition to extracting information from lists, as we did in the first example above, you can also create and modify lists with for loops. You can create a list by appending to a new list at each iteration of the for loop like this:

# Creating a new list
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']
capitalized_cities = []
```python
for city in cities:
    capitalized_cities.append(city.title())
```
Modifying a list is a bit more involved, and requires the use of the range() function.

We can use the range() function to generate the indices for each value in the cities list. This lets us access the elements of the list with cities[index] so that we can modify the values in the cities list in place.
```python
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']

for index in range(len(cities)):
    cities[index] = cities[index].title()
```

# Iterating Through Dictionaries with For Loops
When you iterate through a dictionary using a for loop, doing it the normal way (for n in some_dict) will only give you access to the keys in the dictionary - which is what you'd want in some situations. In other cases, you'd want to iterate through both the keys and values in the dictionary. Let's see how this is done in an example. Consider this dictionary that uses names of actors as keys and their characters as values.

```python
cast = {
           "Jerry Seinfeld": "Jerry Seinfeld",
           "Julia Louis-Dreyfus": "Elaine Benes",
           "Jason Alexander": "George Costanza",
           "Michael Richards": "Cosmo Kramer"
       }
```

Iterating through it in the usual way with a for loop would give you just the keys, as shown below:

```python
for key in cast:
    print(key)
```

This outputs:
```
Jerry Seinfeld
Julia Louis-Dreyfus
Jason Alexander
Michael Richards
```

If you wish to iterate through both keys and values, you can use the built-in method items like this:

```python
for key, value in cast.items():
    print("Actor: {}    Role: {}".format(key, value))
```

This outputs:
```
Actor: Jerry Seinfeld    Role: Jerry Seinfeld
Actor: Julia Louis-Dreyfus    Role: Elaine Benes
Actor: Jason Alexander    Role: George Costanza
Actor: Michael Richards    Role: Cosmo Kramer
```

items is an awesome method that returns tuples of key, value pairs, which you can use to iterate over dictionaries in for loops.

```python
result = 0
basket_items = {'apples': 4, 'oranges': 19, 'kites': 3, 'sandwiches': 8}
fruits = ['apples', 'oranges', 'pears', 'peaches', 'grapes', 'bananas']

for key, value in basket_items.items():
    if key in fruits:
        result += value

print(result)
```
`23 `

# While Loops
For loops are an example of "definite iteration" meaning that the loop's body is run a predefined number of times. This differs from "indefinite iteration" which is when a loop repeats an unknown number of times and ends when some condition is met, which is what happens in a while loop. Here's an example of a while loop.
```python
card_deck = [4, 11, 8, 5, 13, 2, 8, 10]
hand = []

# adds the last element of the card_deck list to the hand list
# until the values in hand add up to 17 or more
while sum(hand)  < 17:
    hand.append(card_deck.pop())
```
This example features two new functions. sum returns the sum of the elements in a list, and pop is a list method that removes the last element from a list and returns it.

## Components of a While Loop
1. The first line starts with the while keyword, indicating this is a while loop.
2. Following that is a condition to be checked. In this example, that's sum(hand) <= 17.
3. The while loop heading always ends with a colon :.
4. Indented after this heading is the body of the while loop. If the condition for the while loop is true, the code lines in the loop's body will be executed.
5. We then go back to the while heading line, and the condition is evaluated again. This process of checking the condition and then executing the loop repeats until the condition becomes false.
6. When the condition becomes false, we move on to the line following the body of the loop, which will be unindented.

The indented body of the loop should modify at least one variable in the test condition. If the value of the test condition never changes, the result is an infinite loop!

```python
print_str = "Water falls"

i =  0

while i < len(print_str):
    print(print_str[i])
    i += 1
```
```
W
a
t
e
r

f
a
l
l
s
```

```python
number = 6
product = number
result = number

for i in range(1, number):
    result *= i

print(result)
```
`720`

```python
number = 6    

product = number

while number > 1:
    number -= 1
    product *= number
    

print(product)
```
`720`


# Break, Continue
Sometimes we need more control over when a loop should end, or skip an iteration. In these cases, we use the break and continue keywords, which can be used in both for and while loops.

* break terminates a loop
* continue skips one iteration of a loop

```python
# HINT: modify the headlines list to verify your loop works with different inputs
headlines = ["Local Bear Eaten by Man",
             "Legislature Announces New Laws",
             "Peasant Discovers Violence Inherent in System",
             "Cat Rescues Fireman Stuck in Tree",
             "Brave Knight Runs Away",
             "Papperbok Review: Totally Triffic"]

news_ticker = ""

# write your loop here
for headline in headlines:
    headline = headline + " "
    news_ticker += headline
    if len(news_ticker) >= 140:
        news_ticker = news_ticker[:140]
        break
    
print(news_ticker)
```
`Local Bear Eaten by Man Legislature Announces New Laws Peasant Discovers Violence Inherent in System Cat Rescues Fireman Stuck in Tree Brave`

___
# Zip and Enumerate
zip and enumerate are useful built-in functions that can come in handy when dealing with loops.

Zip
zip returns an iterator that combines multiple iterables into one sequence of tuples. Each tuple contains the elements in that position from all the iterables. For example, printing

`list(zip(['a', 'b', 'c'], [1, 2, 3]))` would output `[('a', 1), ('b', 2), ('c', 3)]`.

Like we did for range() we need to convert it to a list or iterate through it with a loop to see the elements.

You could unpack each tuple in a for loop like this.
```python
letters = ['a', 'b', 'c']
nums = [1, 2, 3]

for letter, num in zip(letters, nums):
    print("{}: {}".format(letter, num))
```
In addition to zipping two lists together, you can also unzip a list into tuples using an asterisk.
```python
some_list = [('a', 1), ('b', 2), ('c', 3)]
letters, nums = zip(*some_list)
```
This would create the same letters and nums tuples we saw earlier.

Enumerate
enumerate is a built in function that returns an iterator of tuples containing indices and values of a list. You'll often use this when you want the index along with each element of an iterable in a loop.
```python
letters = ['a', 'b', 'c', 'd', 'e']
for i, letter in enumerate(letters):
    print(i, letter)
```
This code would output:
```
0 a
1 b
2 c
3 d
4 e
```

```python
x_coord = [23, 53, 2, -12, 95, 103, 14, -5]
y_coord = [677, 233, 405, 433, 905, 376, 432, 445]
z_coord = [4, 16, -6, -42, 3, -6, 23, -1]
labels = ["F", "J", "A", "Q", "Y", "B", "W", "X"]

points = []
# write your for loop here
for point in zip(labels, x_coord, y_coord, z_coord):
    points.append("{}: {}, {}, {}".format(*point))

for point in points:
    print(point)
```
```
F: 23, 677, 4
J: 53, 233, 16
A: 2, 405, -6
Q: -12, 433, -42
Y: 95, 905, 3
B: 103, 376, -6
W: 14, 432, 23
X: -5, 445, -1
```

```python
cast_names = ["Barney", "Robin", "Ted", "Lily", "Marshall"]
cast_heights = [72, 68, 72, 66, 76]

cast = dict(zip(cast_names, cast_heights))
print(cast)
```
`{'Marshall': 76, 'Robin': 68, 'Lily': 66, 'Barney': 72, 'Ted': 72}`

Enumerate
```python
cast = ["Barney Stinson", "Robin Scherbatsky", "Ted Mosby", "Lily Aldrin", "Marshall Eriksen"]
heights = [72, 68, 72, 66, 76]

for i, character in enumerate(cast):
    cast[i] = character + " " + str(heights[i])

print(cast)
```
Output:

`['Barney Stinson 72', 'Robin Scherbatsky 68', 'Ted Mosby 72', 'Lily Aldrin 66', 'Marshall Eriksen 76']`

___
# List Comprehensions
In Python, you can create lists really quickly and concisely with list comprehensions. This example from earlier:
```python
capitalized_cities = []
for city in cities:
    capitalized_cities.append(city.title())
can be reduced to:
```
capitalized_cities = [city.title() for city in cities]
List comprehensions allow us to create a list using a for loop in one step.

You create a list comprehension with brackets [], including an expression to evaluate for each element in an iterable. This list comprehension above calls city.title() for each element city in cities, to create each element in the new list, capitalized_cities.

## Conditionals in List Comprehensions
You can also add conditionals to list comprehensions (listcomps). After the iterable, you can use the if keyword to check a condition in each iteration.

```python
squares = [x**2 for x in range(9) if x % 2 == 0]
```

The code above sets squares equal to the list [0, 4, 16, 36, 64], as x to the power of 2 is only evaluated if x is even. If you want to add an else, you will get a syntax error doing this.
```python
squares = [x**2 for x in range(9) if x % 2 == 0 else x + 3]
```
If you would like to add else, you have to move the conditionals to the beginning of the listcomp, right after the expression, like this.
```python
squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```
List comprehensions are not found in other languages, but are very common in python.

</br>
</br>

## Extract First Names
```python
names = ["Rick Sanchez", "Morty Smith", "Summer Smith", "Jerry Smith", "Beth Smith"]

first_names = [name.split()[0].lower() for name in names]
print(first_names)
```
Output:
```
['rick', 'morty', 'summer', 'jerry', 'beth']
```

## Multiples of Three
```python
multiples_3 = [x * 3 for x in range(1, 21)]
print(multiples_3)
```
Output:
```
[3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60]
```
## Filter Names by Scores
```python
scores = {
             "Rick Sanchez": 70,
             "Morty Smith": 35,
             "Summer Smith": 82,
             "Jerry Smith": 23,
             "Beth Smith": 98
          }

passed = [name for name, score in scores.items() if score >= 65]
print(passed)
```
Output:
```
The order of elements in this output may vary since dictionaries are unordered.

['Beth Smith', 'Summer Smith', 'Rick Sanchez']
```
```python
names = input("Enter names separated by commas: ").title().split(",")
assignments = input("Enter assignment counts separated by commas: ").split(",")
grades = input("Enter grades separated by commas: ").split(",")

message = "Hi {},\n\nThis is a reminder that you have {} assignments left to \
submit before you can graduate. You're current grade is {} and can increase \
to {} if you submit all assignments before the due date.\n\n"

for name, assignment, grade in zip(names, assignments, grades):
    print(message.format(name, assignment, grade, int(grade) + int(assignment)*2))
```

```
Hi [insert student name],

This is a reminder that you have [insert number of missing assignments] assignments left to submit before you can graduate. Your current grade is [insert current grade] and can increase to [insert potential grade] if you submit all assignments before the due date.
```

____
