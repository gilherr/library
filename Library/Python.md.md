# Python 3.x

# Things to remember

  
| Command | Effect |
|--|--|
| `print(line,end='') ` | change end of line char (defaults to `\n`)   |
|`print(line.strip())` |strips any trailing new lines. |
|`a, b = 0, 1` | `a=0; b=1`|
|`print("foo" if a < b else "bar")` | `a < b ? print"foo": print"bar"`|
|`num = 42 / 9`|`(<type 'float'>, 4.66666)`|
|`num = 42 // 9`|`(<type 'float'>, 4.0) - floor`|
|`num = round(42 / 9`)|`(<type 'float'>, 5.0) - ceiling`|
|`num = round(42 / 9, 2)`|`(<type 'float'>, 4.67) - round 2 after dot`|
|`num = divmod(42,9)`|`<class 'tuple'> (4, 6) - (div,mod)`|

| | |
| | |
| | |











## JSON Format

[DOCS](https://docs.python.org/2/library/json.html)

# convert string to json

j1 = json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')

# pretty print a json

print(json.dumps(j1, sort_keys=True, indent=4, separators=(',', ': ')))

# print the value 1.0 out of the example json

print(j1[1]["bar"][2])

  

### Write JSON to file

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

  

  
  

## Hebrew UTF-8 Decoding

[stackoverflow](http://stackoverflow.com/questions/29850912/decoding-and-encoding-hebrew-string-in-python)

## Switch statements replacement

  

def main():

choices = dict(

one = 'first',

two = 'second',

three = 'third',

four = 'fourth',

five = 'fifth'

)

v = 'one'

# dict.get(item, default if not found)

print(choices.get(v, 'other'))
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzk3MjU5OTQsLTc0NzMyNzUzMF19
-->