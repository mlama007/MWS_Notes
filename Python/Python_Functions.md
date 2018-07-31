# Functions
Welcome to this lesson on Functions! You'll learn about:

Defining Functions
Variable Scope
Documentation
Lambda Expressions
Iterators and Generators
You can think about functions as a way to take what you have already learned how to do, and put it in a holder that allows you to use it over and over again in an easy to use container.

# Defining Functions
Example of a function definition:
```python
def cylinder_volume(height, radius):
    pi = 3.14159
    return height * pi * radius ** 2

cylinder_volume(10, 3)
```

```python
def cylinder_volume(height, radius=5):
    pi = 3.14159
    return height * pi * radius ** 2

cylinder_volume(10, 7)  # pass in arguments by position
cylinder_volume(height=10, radius=7)  # pass in arguments by name
```

```python
def readable_timedelta(days):
    weeks = days//7
    days %= 7
    return "{} week(s) and {} day(s).".format(weeks, days)

print(readable_timedelta(15))
```
`2 week(s) and 1 day(s).`

</br>

# Variable Scope
```python
# This will result in an error
def some_function():
    word = "hello"

print(word)
```

```python
# This works fine
def some_function():
    word = "hello"

def another_function():
    word = "goodbye"
```
```python
# This works fine
word = "hello"

def some_function():
    print(word)

some_function()
```


___
A better way to write this would be:
```python
egg_count = 0

def buy_eggs(count):
    return count + 12  # purchase a dozen eggs

egg_count = buy_eggs(egg_count)
```
Compare this with the original code snippet:
```python
egg_count = 0

def buy_eggs():
    egg_count += 12 # purchase a dozen eggs

buy_eggs()
```
This second code snippet causes an UnboundLocalError.
 
 </br>

# Documentation
```python
def population_density(population, land_area):
    """Calculate the population density of an area.

    INPUT:
    population: int. The population of that area
    land_area: int or float. This function is unit-agnostic, if you pass in values in terms
    of square km or square miles the function will return a density in those units.

    OUTPUT: 
    population_density: population / land_area. The population density of a particular area.
    """
    return population / land_area
```


___

# Lambda Expressions

With a lambda expression, this function:
```python
def multiply(x, y):
    return x * y
```
can be reduced to:
```python
multiply = lambda x, y: x * y
```
 
 </br>
 
 </br>


# Iterators And Generators
`Iterables` are objects that can return one of their elements at a time, such as a list. Many of the built-in functions we’ve used so far, like 'enumerate,' return an iterator.

An `iterator` is an object that represents a stream of data. This is different from a list, which is also an iterable, but not an iterator because it is not a stream of data.

`Generators` are a simple way to create iterators using functions. You can also define iterators using classes, which you can read more about [here](https://docs.python.org/3/tutorial/classes.html#iterators).

Here is an example of a generator function called my_range, which produces an iterator that is a stream of numbers from 0 to (x - 1).

```python
def my_range(x):
    i = 0
    while i < x:
        yield i
        i += 1
```
```python
for x in my_range(5):
    print(x)
```
outputs:
```
0
1
2
3
4
```
## Why Generators?

Generators are a lazy way to build iterables. They are useful when the fully realized list would not fit in memory, or when the cost to calculate each list element is high and you want to do it as late as possible. But they can only be iterated over once.

```python
lessons = ["Why Python Programming", "Data Types and Operators", "Control Flow", "Functions", "Scripting"]

def my_enumerate(iterable, start=0):

    # i = 0
    # while i < len(iterable):
    #     yield(start, iterable[i])
    #     i += 1
    #     start += 1
    
    count = start
    for lesson in lessons:
        yield(count, lesson)
        count += 1

for i, lesson in my_enumerate(lessons, 1):
    print("Lesson {}: {}".format(i, lesson))
```

````
Lesson 1: Why Python Programming
Lesson 2: Data Types and Operators
Lesson 3: Control Flow
Lesson 4: Functions
Lesson 5: Scripting
```