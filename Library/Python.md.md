# Python 3.x

# Things to remember

  
| Command | Effect |
|--|--|
| `print(line,end='') ` | change end of line char (defaults to `\n`)   |
|`print(line.strip())` |strips any trailing new lines. |
|`a, b = 0, 1` | `a=0; b=1`|
|`print("foo" if a < b else "bar")` | `a < b ? print"foo": print"bar"`|

|num = 42 / 9|
|num = 42 // 9|
|num = round(42 / 9)|
|num = round(42 / 9, 2)|
|num = divmod(42,9)

| | |
| | |
| | |




+---------------+---------------+--------------------+
| Fruit         | Price         | Advantages         |
+===============+===============+====================+
| Bananas       | first line\   | first line\        |
|               | next line     | next line          |
+---------------+---------------+--------------------+
| Bananas       | first line\   | first line\        |
|               | next line     | next line          |
+---------------+---------------+--------------------+





a, b = 0, 1

a=0; b=1

print("foo" if a < b else "bar")

a < b ? print"foo": print"bar"

num = 42 / 9

num = 42 // 9

num = round(42 / 9)

num = round(42 / 9, 2)

num = divmod(42,9)

(<type 'float'>, 4.66666)

(<type 'float'>, 4.0) - floor

(<type 'float'>, 5.0) - ceiling

(<type 'float'>, 4.67) - round 2 after dot

<class 'tuple'> (4, 6) - (div,mod)

int(42.9)

float(42)

casting

x | y, x & y, x ^ y, x >> 4, x << 4, ~x

bitwise or,and,xor,shift left, right,not

and, or - spelled out

True and False = False

are boolean operators. opposed to &,| which are doing bitwise arithmetics.

s = "You can use special \ncharacters"

s = r"a RAW string \n no special chars"

s = "placeholders {} for vars".format(x)

normal

notice the 'r' in the begining

insert x int the {}

'''\

triple lets you

write line after line

after line ''''

notice that the \ is there to escape the new-line char. it must be at the end to escape it.

range(0, 4) => 0 1 2 3

l[0:5] => l[0] l[1] l[2] l[4]

ranges in python are non inclusive

  

When we yield a var, it is returned to the caller but remembers where it stopped. so next time the function is called, it continues after the yield.

This is useful as an iterator as in the example above - the n in the for loop starts running only when primes() yielded (returned) an n that is a prime number.
<!--stackedit_data:
eyJoaXN0b3J5IjpbODcyODM1NTAyLC03NDczMjc1MzBdfQ==
-->