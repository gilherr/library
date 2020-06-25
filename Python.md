# Python 3.x

## Things to remember

| Command | Action |
|---------|--------|
|`print(line,end='')` | change end of line char (defaults to "\n") |
|`print(line.strip())` | strips any trailing new lines. |
|`a, b = 0, 1`| a=0; b=1 |
|`print("foo" if a < b else "bar")`| a < b ? print"foo": print"bar" |
|`num = 42 / 9`| (type 'float', 4.66666)|
|`num = 42 // 9`| (type 'float', 4.0) - floor|
|`num = round(42 / 9)`| (type 'float', 5.0) - ceiling|
|`num = round(42 / 9, 2)`| (type 'float', 4.67) - round 2 after dot|
|`num = divmod(42,9)`| class 'tuple' (4, 6) - (div,mod)|
|`int(42.9)`, `float(42)`|casting|
|`x | y, x & y, x ^ y, x >> 4, x << 4, ~x`|bitwise or,and,xor,shift left, right,not|
|`and, or - spelled out`|are boolean operators. opposed to &,| which are doing bitwise arithmetics.|
|`s = "You can use special \ncharacters"`|normal|
|`s = r"a RAW string \n no special chars"`|notice the 'r' in the begining|
|`s = "placeholders {} for vars".format(x)`|insert x in the {}|
|`s = f"placeholders {var_name} for vars"`|insert var_name in the {}|
|`range(0, 4) => 0 1 2 3`| `range()` is non inclusive

When we yield a var, it is returned to the caller but remembers where it stopped. so next time the function is called, it continues after the yield.
This is useful as an iterator as in the example above - the n in the for loop starts running only when primes() yielded (returned) an n that is a prime number.

## JSON Format

[DOCS](https://docs.python.org/2/library/json.html)

```python
# convert string to json
j1 = json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')
# pretty print a json
print(json.dumps(j1, sort_keys=True, indent=4, separators=(',', ': ')))
# print the value 1.0 out of the example json
print(j1[1]["bar"][2])
```

### Write JSON to file

```python
import codecs
import json

# this will write every item in a new line
with codecs.open("file.txt",'w','utf-8') as file:
   for item in arr:
       json.dump(item,file, ensure_ascii=False)
       file.write('\n')

# this will pritty print the entire json
with codecs.open("file.txt",'w','utf-8') as file:
   json.dump(item,file,indent=2,ensure_ascii=False)
```

## Hebrew UTF-8 Decoding

[stackoverflow](http://stackoverflow.com/questions/29850912/decoding-and-encoding-hebrew-string-in-python)

## Switch statements replacement

```python
def main():
   choices = dict(
       one = 'first',
       two = 'second',
       three = 'third',
       four =  'fourth',
       five = 'fifth'
   )
   v = 'one'
   # dict.get(item, default if not found)
   print(choices.get(v, 'other'))
```

## For loop with index

```python
def main():
   s = 'a string'
   for index, char in enumerate(s):
       print(index,char)

(0, 'a')
(1, ' ')
(2, 's')
(3, 't')
(4, 'r')
(5, 'i')
(6, 'n')
(7, 'g')
```

## Reading CLI Arguments

```python
# cli command: py main.py arg1 arg2
import sys
print(sys.argv)
# ["main.py", "arg1", "arg2"]
```

## Serialization - Pickle

[realPython](https://realpython.com/python-pickle-module/)

## Time Complexity

[Link](https://www.ics.uci.edu/~brgallar/week8_2.html)

## Everything is an object

Everything in Python 3 is an object: variables, functions, even code;
Every object has:

* ID: Is a unique identifier that identifies a particular instance of an object, cannot change for the life of the object.
* Type: Identifies the class of an object, cannot change for the life of the object.
* Value: The contents of the object. variables, methods, or properties .

### Mutable and Immutable

* Mutable  objects that can change their value.
* Immutable  objects that cannot change their value.

Some immutable objects at times may look like they are changing their values.
They are not actually changing their values though. The distinction is visible
using the id function.
Integers, container objects, strings, things like these may appear to be
changing values when they are not.

Most fundamental types in Python are immutable: Numbers, strings, and tuples.

Mutable objects include: Lists, dictionaries and some other objects.

```python
"""
Numbers are immutable. The number 42 is an object, and that object has ID, type, value, just like any other object.
x is a reference to that object.
the 'is' operator compares the id of the objects.
"""
>>> x = 42
>>> id(x)
51477364
>>> type(x)
<type 'int'>
>>> id(42)
51477364
>>> type(42)
<type 'int'>
>>> y = 42
>>> id(y)
51477364
>>> x == y
True
>>> x is y
True
```

```python
"""
The Dictionary is a mutable object and can be changed. In this example the value is the same but the object's id are different.
"""
>>> x = dict( x = 42 )
>>> type(x)
<type 'dict'>
>>> id(x)
57909872
>>> y = dict( x = 42 )
>>> id(y)
57913040
>>> x
{'x': 42}
>>> y
{'x': 42}
>>> x == y
True
>>> x is y
False
```

## Regular Expressions

```python
import re

def main():
   fh = open('raven.txt')

   # compile the regex for efficiency
   pattern = re.compile('(Len|Neverm)ore', re.IGNORECASE)

   # print all matched lines
   for line in fh:
       if re.search('(Len|Neverm)ore', line):
           print(line, end='')

   # print matched lines using compiled pattern
   for line in fh:
       if pattern.search(line):
           print(line, end='')

   # print only matched words
   for line in fh:
       match = re.search(pattern, line)
       if match:
           print(match.group())

   # search, replace and print every line
   for line in fh:
       print(re.sub(pattern, '###', line), end='')

   # search, replace and print every line using compiled pattern
   for line in fh:
       print(pattern.sub('###', line), end='')

   # search and replace in two steps
   for line in fh:
       match = pattern.search(line)
       if match:
           print(pattern.sub('###', line), end ='')
```

## Exceptions

### Python Exceptions List

[https://docs.python.org/3/library/exceptions.html](https://docs.python.org/3/library/exceptions.html)

### Catch Exception

```python
def main():
   try:
       fh = open('xlines.txt')
   except IOError as e:
       print('could not open the file: ', e)
   else:
       for line in fh: print(line.strip())
```

or

```python
def main():
   try:
       fh = open('xlines.txt')
       for line in fh: print(line.strip())
   except IOError as e:
       print('could not open the file: ', e)
```

### Raise Exception

```python
def main():
   try:
       for line in readFile('xlines.doc'): print(line.strip())
   except IOError as e:
       print('could not open the file: ', e)
   except ValueError as e:
       print('bad filename: ', e)

def readFile(filename):
   if filename.endswith('.txt'):
       fh = open(filename)
       return fh.readlines()
   else:
       raise ValueError('Filename must end with .txt')
```

## Functions

* Empty Function requiers the pass statement.
* Parameteres that have default value are optional. others are requiered.

```python
def main():
   testfunc()
   anotherfunc(42)

def testfunc():
   pass

def anotherfunc(must, opt = 1, opt2 = None):
   if opt2 is None:
       print('opt2 is None!')

   print('function with parameters: ', must, opt, opt2)

# main() is called after all the function have been declared.
if __name__ == "__main__": main()
```

### Send a list of arguments to a function

```python
def main():
   testfunc(1,2,3,41,42,43)

def testfunc(first, second, third, *args):
   print(first, second, third)
   for i in args: print(i,end=' ')
```

### `**kwargs` - KeyWord Arguments

`**kwargs` is a dictionary passed to a function.
notice - when iterating through it, it wont read in a particular order.

```python
def main():
   testfunc(1,2,3,4,5,6, kone = 11, ktwo = 22, kthree = 33)

# first 3 args are regular, "*args" is a tuple, "**kwargs" is a dictionary
def testfunc(first, second, third, *args, **kwargs):
   print(first, second, third, args, kwargs)
   for i in kwargs: print(i, kwargs[i])
```

## Generator Function

Its a function that returns an iterator object.
Meant to be used in loops.
The yield statement returns "i" but when the generator is called again (in the loop) it continues from the yield statement.

```python
def main():
   for i in inclusive_range(25):
       print(i, end = ' ')

def inclusive_range(*args):
   start = 0
   end   = 0
   step  = 1
   numargs = len(args)

   if numargs == 1:
       end   = args[0]
   elif numargs == 2:
       start = args[0]
       end   = args[1]
   elif numargs == 3:
       start = args[0]
       end   = args[1]
       step  = args[2]
   else: raise TypeError('required at least one argument')

   i = start
   while i <= end:
       yield i
       i += step

if __name__ == "__main__": main()
```

## Function  Decorators

```python
def null_decorator(func):
    return func

def greet():
    return 'Hello!'

greet = null_decorator(greet)

>>> greet()
'Hello!'
```

Putting an `@null_decorator` line in front of the function definition is the same as defining the function first and then running through the decorator. Using the `@` syntax is just syntactic sugar and a shortcut for this commonly used pattern:

```python
@null_decorator
def greet():
    return 'Hello!'

>>> greet()
'Hello!'
```

### Decorating Functions That Accept Arguments

```python
def trace(func):
    def wrapper(*args, **kwargs):
        print(f'TRACE: calling {func.__name__}() '
              f'with {args}, {kwargs}')

        original_result = func(*args, **kwargs)

        print(f'TRACE: {func.__name__}() '
              f'returned {original_result!r}')

        return original_result
    return wrapper

@trace
def say(name, line):
    return f'{name}: {line}'

>>> say('Jane', 'Hello, World')
'TRACE: calling say() with ("Jane", "Hello, World"), {}'
'TRACE: say() returned "Jane: Hello, World"'
'Jane: Hello, World'
```

## OO Python

### Classes

```python
class Duck:

   def __init__(self, color = 'white'):
       self._color = color

   def quack(self):
       print('Quaaack!')

   def walk(self):
       print('Walks like a duck.')

   def set_color(self, color):
       self._color = color

   def get_color(self):
       return self._color

def main():
   donald = Duck()
   print(donald.get_color())
   donald.set_color('blue')
   print(donald.get_color())
```

### Dunder Functions

[Dunder (Magic) functions](https://dbader.org/blog/python-dunder-methods)

### **kwargs Constructor

```python
class Duck:

   def __init__(self, **kwargs):
       self.variables = kwargs

   def quack(self):
       print('Quaaack!')

   def walk(self):
       print('Walks like a duck.')

   def set_variable(self, k, v):
       self.variables[k] = v

   def get_variable(self, k):
       return self.variables.get(k, None)

def main():
   donald = Duck(feet = 2)
   donald.set_variable('color', 'blue')
   print(donald.get_variable('feet'))
   print(donald.get_variable('color'))
```

## Inheritance

```python
class SuperClass:
   def superFunction(self): return self.dict['string']

class SubClass1(SuperClass):
   dict = dict(string = "SubClass1")

class SubClass2(SuperClass):
   dict = dict(string = "SubClass2")
```

## Generator Object

By using the __iter__ method, we can create our own iterator for the class and use it in loops.

```python
class myCounter:
   def __init__(self, count):
       self._count = count

   def __iter__(self):
       i = 0
       while i < self._count:
           yield i
           i += 1

def main():
   for k in myCounter(10):
       print(k)
```

## Class Decorators

Another way to have getter and setters with cleaner code

```python
class Duck:
   def __init__(self, **kwargs):
       self.properties = kwargs

   def get_properties(self):
       return self.properties

   def get_property(self, key):
       return self.properties.get(key, None)

   @property
   def color(self):
       return self.properties.get('color', None)

   @color.setter
   def color(self, c):
       self.properties['color'] = c

   @color.deleter
   def color(self):
       del self.properties['color']

def main():
   donald = Duck()
   donald.color = 'blue'
   print(donald.color)
```

## Strings

### Available String Methods

A string object is immutable. when you call these function on it, they return a new object string that was transformed.

[Python strings docs](https://docs.python.org/3.6/library/string.html)

| Command | Action |
| ------- | ------ |
|`'this is a string'.upper()`|'THIS IS A STRING'|
|`'this is a string'.capitalize()`|'This is a string'|
|`'THIS IS A STRING'.lower()`|'this is a string'|
|`'This Is A String'.swapcase()`|'tHIS iS a sTRING'|
|`'this is a string'.find('is')`|2|
|`'this is a string'.replace('this','that')`|'that is a string'|
|`'   this is a string    \n'.strip()`|'this is a string' strips white space on both ends and new line at the end.|
|`'   this is a string    \n'.rstrip()`|'   this is a string'|
|`'   this is a string    \n'.rstrip('\n')`|'   this is a string    ' strip nl only|
|`'124sadf21fsda'.isalnum()`|True - is all alphaNumeric|
|`'sadfASDCfsda'.isalpha()`|True - ia all alpha|
|`'35125124'.isdigit()`|True - is all digits|
|`'this is {}'.format(x)`|'this is 0' - with .format you dont need to know the type like in the %d %f..|
|`'{1} : {0} : {1}'.format(a,b)`|'b : a : b'|
|`'{bob} and {fred}'.format(bob=a,fred=b)`|'a and b'|
|`d = dict( bob = a, ferd = b); '{bob} and {fred}'.format(**d)`|'a and b'|
|`'This is a string of words'.split()`|['This', 'is', 'a', 'string', 'of', 'words']|
|`'This is a string of words'.split('i')`|['Th', 's ', 's a str', 'ng of words']|
|`':'.join(['Th', 's ', 's a str', 'ng of words'])`|'Th:s :s a str:ng of words'|

## Containers

### Tuple vs List

Tuples are lighter classes, they are simpler and faster. More often than not, you have data that does not need to be changed. You should only use lists when you have to.

### Tuple

Is an immutable object. It cannot be changed.

| Command | Action |
| ------- | ------ |
|`t = (1,2,3,4,5,6,7)`|the ',' is what really makes the tuple.|
|`t[-1]`|7|
|`max(t)`|7|
|`min(t)`|1|
|`len(t)`|7|
|`4 in t`|True|
|`8 not in t`|True|
|`t.count(3)`|1|
|`t.index(3)`|2 - first occurrence|

### The list

Is a mutable object. it is changeable:

| Command | Action |
| ------- | ------ |
|`l = [1,2,3,4,5,6,7]`|can do all of the above plus:|
|`l[4] = 0`|[1,2,3,4,0,6,7]|
|`l.append(10)`|[1,2,3,4,5,6,7,10]|
|`l.extend(range(4))`|[1,2,3,4,5,6,7,0,1,2,3]|
|`l.insert(2,9)`|[1,2,9,4,5,6,7]- insert 9 at index 2|
|`l.remove(6)`|[1,2,3,4,5,7] - removes first occurrence of 6|
|`del l[4]`|[1,2,3,4,6,7] - delete value at index 4|
|`l.pop()`|7 - [1,2,3,4,5,6] - pop last element|
|`l.pop(x)`|pop element at index x|

### List Comprehensions

```python
[ expression for item in list if conditional ]
```

This is equivalent to:

```python
for item in list:
    if conditional:
        expression
```

Example:

```python
squares = [x**2 for x in range(10)]

print squares
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### Slice

```python
list = [0,1,2,3,4,5,6,7,8,9,10]
list[3:9:2]     #[START:END:STEP]
>>> [3, 5, 7]
```

Notice that the slice return an iterator so you can use:

```python
for i in list[2:8:3] : print(i)
```

### Iterators

[Real Python](https://dbader.org/blog/python-iterators)

```python
class BoundedRepeater:
    def __init__(self, value, max_repeats):
        self.value = value
        self.max_repeats = max_repeats
        self.count = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self.count >= self.max_repeats:
            raise StopIteration
        self.count += 1
        return self.value

if __name__ == "__main__":
    repeater = BoundedRepeater("Hello", 3)
    for item in repeater:
        print(item)
```

### The Dictionary

Hash array.

```python
d = {'one': 1, 'two': 2, 'three': 'three'}


d2 = dict(four = 4, five = 5, six = 6)


d3 = dict(one = 1, two = 2, three = 3, **d2)
d3 contains both dicts
for k, v in d.items(): print(k, v)


for k in sorted(d.keys()): print(k,d[k])


d.pop('one') # returns its value and deletes it.
```

#### Iterating Through a Dictionary

[Real Python](https://realpython.com/iterate-through-dictionary-python/#using-some-of-pythons-built-in-functions)

#### Dictionary Comprehension

```python
dict_variable = {key:value for (key,value) in dictonary.items()}

Example:
dict1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
# Double each value in the dictionary
double_dict1 = {k:v*2 for (k,v) in dict1.items()}
```

### Collections.Counter

```python
from collections import Counter

s = 'aaabbbcccddddefgggg'

print(Counter(s))
Counter({'d': 4, 'g': 4, 'a': 3, 'b': 3, 'c': 3, 'e': 1, 'f': 1})

print(Counter(s).most_common())
[('d', 4), ('g', 4), ('a', 3), ('b', 3), ('c', 3), ('e', 1), ('f', 1)]
```

## Files

### Open file

`f = open('lines.txt')` - by default opens file for read only. Available flags:
`r`, `r+` read\write, `rb` binary, `rt` text, `w`, `a` append.

### Write to file

```python
with open('some_file', 'w') as opened_file:
    opened_file.write('Hola!')

# or

print("some string or var", file = f, end = '')
```

### Using a buffer

```python
infile = open('somefile.txt', 'r')
outfile = open('someotherfile.txt', 'w')
bufferSize = 50000 #bytes
buffer = infile.read(bufferSize)
while len(buffer):
   outfile.write(buffer)
   buffer = infile.read(bufferSize)
```

### Open Binary Files

Same as above only with the 'b' flag.
Notice you must use the buffer to copy parts of the file, you can't read lines.

```python
infile = open('somefile.jpg', 'rb')
outfile = open('someotherfile.jpg', 'wb')
bufferSize = 50000 #bytes
buffer = infile.read(bufferSize)
while len(buffer):
   outfile.write(buffer)
   buffer = infile.read(bufferSize)
```

### Path Resolution

```python
import os

path = os.path.abspath(sys.argv[1]) # read cli arg presumed to be a file
base_name = os.path.basename(full_path)
dir_name = os.path.dirname(full_path)
full_path = os.path.join(dir_name , base_name )
```

### Temporary Files and Folders

[docs](https://docs.python.org/3/library/tempfile.html)

```python
import tempfile

with tempfile.TemporaryFile() as fp:
    fp.write(b'Hello world!')
    fp.seek(0)
    fp.read()
# b'Hello world!'

with tempfile.TemporaryDirectory() as tmpdirname:
    print('created temporary directory', tmpdirname)
# directory and contents have been removed when block ends
```

## Concurrency

Rule of thumb:

* I\O  Multithreading
* CPU  Multiprocessing

### The GIL

* [Understanding the Python GIL](https://www.youtube.com/watch?v=Obt-vMVdM8s)
* [Die Threads](https://www.youtube.com/watch?v=U66KuyD3T0M&t=296s)

The GIL (Global Interpreter Lock) allows only one thread to run at a time for a single interpreter.

### Concurrent.Futures

[Real Python Example](https://realpython.com/intro-to-python-threading/#using-a-threadpoolexecutor)

```python
import concurrent.futures
import logging
import threading
import time

def thread_function(name):
    logging.info("Thread %s: starting", name)
    time.sleep(2)
    logging.info("Thread %s: finishing", name)

if __name__ == "__main__":
    format = "%(asctime)s.%(msecs)03d: %(message)s"
    logging.basicConfig(format=format, level=logging.INFO,
                        datefmt="%H:%M:%S")

    # The context manager handles the thread/process join() for you.
    with concurrent.futures.ThreadPoolExecutor(max_workers=10) as executor:
        executor.map(thread_function, range(30))
```

### References

* [Producer-Consumer Using Queue](https://realpython.com/intro-to-python-threading/#producer-consumer-using-queue)

* [Youtube](https://youtu.be/fKl2JW_qrso?t=1037) example using concurrent.futures.{Process,Thread}PoolExecuter

* [An introduction to parallel programming using Python's multiprocessing module](https://sebastianraschka.com/Articles/2014_multiprocessing.html)

* [Real Python](https://realpython.com/intro-to-python-threading/#using-a-threadpoolexecutor) - good article about multi-threading with good examples

* [Tutorialspoint](https://www.tutorialspoint.com/python/python_multithreading.htm) - more threading examples

* [Multithreading Multiprocessing](https://www.toptal.com/python/beginners-guide-to-concurrency-and-parallelism-in-python#article-updates) - tutorial. relatively deep

## Context Manager - The 'with' statement

The with statement is used to wrap the execution of a block with methods defined by a context manager. This allows common `try...except...finally` usage patterns to be encapsulated for convenient reuse.

```python
# Python program creating a
# context manager

class ContextManager():
 def __init__(self):
  print('init method called')
  
 def __enter__(self):
  print('enter method called')
  return self

 def __exit__(self, exc_type, exc_value, exc_traceback):
  print('exit method called')


with ContextManager() as manager:
 print('with statement block')

## Output
# init method called
# enter method called
# with statement block
# exit method called
```

### Context Manager - References

[Docs](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement)

## Logging

In this example we create a logger with 2 handlers, one writes to a file and the
other writes to stdout. Each handlers has its own log level and formatter.

```python
import logging

logger = logging.getLogger('simple_example')
logger.setLevel(logging.DEBUG)

# create file handler which logs even debug messages
fh = logging.FileHandler('spam.log')
fh.setLevel(logging.DEBUG)

# create console handler with a higher log level
ch = logging.StreamHandler()
ch.setLevel(logging.ERROR)

# create formatter and add it to the handlers
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
ch.setFormatter(formatter)
fh.setFormatter(formatter)

# add the handlers to logger
logger.addHandler(ch)
logger.addHandler(fh)

# 'application' code
logger.debug('debug message')
logger.info('info message')
logger.warn('warn message')
logger.error('error message')
logger.critical('critical message')
```

### Logging - References

* [Docs](https://docs.python.org/3/library/logging.html)
* [Logging Cookbook](https://docs.python.org/3.6/howto/logging-cookbook.html#logging-cookbook)

## Testing

### Pytest

#### Fixtures With Setup Teardown

```python
@pytest.fixture
def validPath():
    path = "2030/05"
    yield path
    if os.path.isdir("2030"):
        os.rmdir("2030/05")
        os.rmdir("2030")

def test_create_directories(validPath):
    create_directories(validPath)
    assert os.path.isdir(validPath
```

#### Parametrization: Combining Tests

```python
import pytest

@pytest.mark.parametrize("palindrome", [
    "",
    "a",
    "Bob",
    "Never odd or even",
    "Do geese see God?",
])
def test_is_palindrome(palindrome):
    assert is_palindrome(palindrome)

@pytest.mark.parametrize("non_palindrome", [
    "abc",
    "abab",
])
def test_is_palindrome_not_palindrome(non_palindrome):
    assert not is_palindrome(non_palindrome)
```

### Mock

[Topal Blog - Python Mocking](https://www.toptal.com/python/an-introduction-to-mocking-in-python)
