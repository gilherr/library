# Ruby Basics

<!-- TOC -->

- [General Notes](#general-notes)
- [References](#references)
- [Style Guide](#style-guide)
- [Variable Scope Indicators](#variable-scope-indicators)
- [Numbers](#numbers)
- [Strings](#strings)
    - [String Methods](#string-methods)
    - [String Interpolation](#string-interpolation)
    - [Single vs Double Quotes](#single-vs-double-quotes)
- [Arrays](#arrays)
    - [Indexing](#indexing)
    - [Array Methods](#array-methods)
- [Hashes](#hashes)
- [Symbols](#symbols)
- [Ranges](#ranges)
- [Constants](#constants)
- [Conditionals](#conditionals)
    - [if else](#if-else)
    - [unless](#unless)
    - [case](#case)
    - [Or-Equals](#or-equals)
    - [Statement Modifiers](#statement-modifiers)
- [Loops](#loops)
    - [Control Methods](#control-methods)
- [Iterators](#iterators)
- [Input Output](#input-output)
- [Filter - Map - Reduce Methods](#filter---map---reduce-methods)
    - [Filter (Find)](#filter-find)
    - [Map](#map)
    - [Reduce (Inject)](#reduce-inject)
- [Sort](#sort)
- [Merge (hashes)](#merge-hashes)
- [Methods](#methods)
    - [Optional Arguments](#optional-arguments)
    - [Return Value](#return-value)
    - [Return Multiple Values](#return-multiple-values)
- [Classes](#classes)
- [Installing `rbenv`](#installing-rbenv)
    - [Usage](#usage)

<!-- /TOC -->

## General Notes

* `object.class` will return the class of the requested object

## References

* [Lynda - Ruby Essential Training 1](https://www.lynda.com/Ruby-tutorials/Next-steps/769286/807426-4.html?autoplay=true)
* [Ruby For Beginners](http://ruby-for-beginners.rubymonstas.org/index.html)

## Style Guide

* Soft tabs: 2 spaces, convert tabs to spaces.
* class names: **CamelCase**
* file names, method names and variable names: **snake_case**

[github.com/rubocop-hq/ruby-style-guide](https://github.com/rubocop-hq/ruby-style-guide)
[github.com/bbatsov/ruby-style-guide](https://github.com/bbatsov/ruby-style-guide)

## Variable Scope Indicators

| Scope    | Presentation |
| -------- | ------------ |
| Global   | `$variable`  |
| Class    | `@@variable` |
| Instance | `@variable`  |
| Local    | `variable`   |
| Block    | `variable`   |

## Numbers

| Instruction | Description          |
| ----------- | -------------------- |
| `10.to_f`   | cast int to float    |
| `3.0.to_i`  | cast float to int    |
| `123.to_s`  | cast value to string |
| `abs`       | absolut              |
| `round`     |                      |
| `floor`     | round down           |
| `ceil`      | round up             |

## Strings

```ruby
greeting = "Hello" # => "Hello"
target = 'world' # => "world"
greeting + ' ' + target # => "Hello world"

greeting # => Hello
greeting << ' world' # => Hello world
greeting # => Hello world

"Yada " * 3 # => "Yada Yada Yada"
1 * 5 # => 5
'1' * 5 # => "11111"
```

### String Methods

| Method           | Description |
| ---------------- | ----------- |
| `str.length`     |             |
| `str.reverse`    |             |
| `str.capitalize` |             |
| `str.upcase`     |             |
| `str.downcase`   |             |

```ruby
greeting.reverse # => "dlrow olleH"
greeting.capitalize # => "Hello world"
greeting.upcase # => "HELLO WORLD"
greeting.downcase # => "hello world"
greeting.length # => 11
greeting.reverse.capitalize # => "Dlrow olleh"
```

### String Interpolation

```ruby
msg = 'I love books'
puts "I just wanted to say: #{msg}"
# "I just wanted to say: I love books"

puts "1 + 1 = #{1 + 1}" # => 2
puts "shout it: #{msg.upcase}" # => "shout it: I LOVE BOOKS"
```

### Single vs Double Quotes

Single quotes disables string interpolation.

```ruby
puts "\ta\t#{1+1}"
#  a 2
puts '\ta\t#{1+1}'
# "\ta\t#{1+1}"
```

## Arrays

### Indexing

```ruby
>> arr = [0,1,2,3,4,5,6,7,8,9]

>> arr[-1]
=> 9

# arr[x,y] : start at index x and retrieve y items
>> arr[3,5]
=> [3, 4, 5, 6, 7]

>> arr[-2,2]
=> [8, 9]

# retrieve a range of items
>> arr[2..5]
=> [2, 3, 4, 5]

>> arr[5..]
=> [5, 6, 7, 8, 9]

>> arr << 'new_item'
=> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "new_item"]
```

### Array Methods

**Note**:  some methods support the `!` operator at the end of their name (e.g `arr.reverse!`). This runs the method in place, mutating the original object.

```ruby
array = [2, 4, ['a', 'b'], nil, 4, 'c']

array.length          # => 6
array.size            # => 6
array.empty?          # => false
array.reverse!        # => ["c", 4, nil, ["a", "b"], 4, 2]
array.shuffle!        # => ["c", 4, ["a", "b"], nil, 2, 4]
array.uniq!           # => ["c", 4, ["a", "b"], nil, 2]
array.compact!        # => ["c", 4, ["a", "b"], 2]
array.flatten!        # => ["c", 4, "a", "b", 2]
array.include?(2)     # => true
array.include?(1)     # => false
array.delete_at(1)    # => 4
array                 # => ["c", "a", "b", 2]
array.delete('c')     # => "c"
array                 # => ["a", "b", 2]
[1,2,3,4].join(',')   # => "1,2,3,4"
[1,2,3,4].join        # => "1234"
[1,2,3,4].join(' - ') # => "1 - 2 - 3 - 4"
"1,2,3,4".split(',')  # => ["1", "2", "3", "4"]
numbers = [1,2,3,4]   # => [1, 2, 3, 4]
numbers.push(5)       # => [1, 2, 3, 4, 5]
last = numbers.pop    # = 5
numbers               # => [1, 2, 3, 4]
first = numbers.shift # 1
numbers               # => [2, 3, 4]
numbers.unshift(1)    # => [1, 2, 3, 4]

```

## Hashes

An unordered, object-indexed collection of objects.

Much like python dictionary or javascript json.

```ruby
# Basic Hash
car = {
  'brand' => 'Ford',
  'model' => 'Mustang',
  'color' => 'blue',
  'interior_color' => 'tan'
}

# With Symbols
car_s = {
  brand: 'Ford',
  model: 'Mustang',
  color: 'blue',
  interior_color: 'tan'
}

puts car['model'] # Mustang
car.values # => ["Ford", "Mustang", "green", "tan", 2]
car.has_key?('brand') # => true
car_s.has_key?(:brand) # => true
hash.has_value?('Ford') # => true
car.length # => 5
car.size # => 5
car.to_a # to_array => [["brand", "Ford"], ["model", "Mustang"], ...
```

## Symbols

Can be thought of as identities.

Can work as a tag. easier to manage in memory and (probably?) helps with an IDE with completions.

```ruby
"test".object_id # => 70287715030480
"test".object_id # => 70287714953440
:test.object_id # => 371228
:test.object_id # => 371228

person = {:first_name => 'Benjamin', :last_name => 'Franklin'}
# OR
person = {first_name: 'Benjamin', last_name: 'Franklin'}

person[:first_name] # => "Benjamin"

```

## Ranges

| Type| Command|
| --------------- | ------ |
| Inclusive range | `1..10` |
| Exclusive range | `1...10` |

```ruby
inclusive = 1..10 # => 1..10
exclusive = 1...10 # => 1...10
inclusive.class # => Range

1..10.class # ArgumentError: bad value for range
(1..10).class # => Range

inclusive.include?(10) # => true
exclusive.include?(10) # => false
inclusive.begin # => 1
inclusive.first # => 1
inclusive.end # => 10
inclusive.last # => 10
exclusive.begin # => 1
exclusive.end # => 10
array = [*inclusive] # => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
alpha = 'a'..'m' # => "a".."m"
alpha.include?('g') # => true
array = [*alpha] # => ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m"]
```

## Constants

```ruby
MAX_SCORE = 100 # => 100
max_score = 100 # => 100
MAX_SCORE == max_score # => false

MAX_SCORE = 50
# warning: already initialized constant
# => 50
MAX_SCORE # changed after warning => 50

Temp = 72 # => 72
Temp = 68
# warning: already initialized constant
# => 68
```

## Conditionals

### if else

```ruby
if boolean
    # ...
elsif boolean
    # ...
else
    # ...
end
```

### unless

```ruby
unless array.empty?
    # ...
end
```

### case

```ruby
case
when boolean
    # ...
when boolean
    # ...
else
    # ...
end
```

```ruby
case test_value
when value
    # ...
when value
    # ...
else
    # ...
end
```

### Or-Equals

If `x` has no value, assign `y` to it.

```ruby
x ||= y

# same as
unless x
    x = y
end
```

### Statement Modifiers

```ruby
x = y unless x

puts "Hello" if greeting_enabled
score += 10 unless score >= MAX_SCORE
```

## Loops

### Control Methods

| Command| Description|
| --------------- | ------ |
| `break` | Terminate the whole loop |
| `next` | Jump to next loop |
| `redo` | Redo this loop |
| `retry` | Start the whole loop over |

```ruby
# basic loop - very rare
i = 5
loop do
    break if i <= 0
    puts "Countdown: #{i}"
    i -= 1
end
puts "Blast off!"

# use
while boolean
    # ...
end

until boolean
    # ...
end
```

## Iterators

**Notice** the *block variable* that is written between the `|`. This variables scope is only within the `do..end` block.

```ruby
collection.each do |variable|
   code
end
```

By Class

| Class   | Iterators                               |
| ------- | --------------------------------------- |
| Numbers | `times, upto, downto, step`             |
| Range   | `each, step`                            |
| String  | `each_line, each_char, each_byte`       |
| Array   | `each, each_index, each_with_index`     |
| Hash    | `each, each_key, each_value, each_pair` |

Array

```ruby
fruits = ['banana', 'apple', 'pear']
fruits.each do |fruit|
    puts fruit.capitalize
end

# or
for fruit in fruits
    puts fruit.capitalize
end
```

Hash

```ruby
scores = {low: 2, high:8, avg:6}
scores.each do |k, v|
    puts "#{k.capitalize}: #{v}"
end
```

## Input Output

`puts` adds new line while `print` does not.

Use `chop` to remove last character of a string or `chomp` to remove last character *only if its `\n`*.

```ruby
print "What is your name?"
response = gets
puts "Hello, #{response}!" # => Hello, Billy\n!

print "What is your name?"
response = gets.chomp
puts "Hello, #{response}!" # => Hello, Billy!
```

## Filter - Map - Reduce Methods

### Filter (Find)

In ruby, the parallel method for `filter` would be `find_all`.

```ruby
x = (1..10).find {|n| n == 5} # => 5
x = (1..10).find {|n| n % 3 == 0} # => 3
x = (1..10).detect {|n| n % 3 == 0} # => 3

fruits = ['apple', 'banana', 'pear', 'coconut']
fruits.find {|fruit| fruit.length > 5} # => "banana"
fruits.find_all {|fruit| fruit.length > 5} # => ["banana", "coconut"]

pantry = {'apple' => 0, 'banana' => 1, 'pear' => 3}
pantry.find {|k,v| v == 0} # ["apple", 0]

(1..10).find_all {|n| n % 3 == 0} # [3,6,9]
(1..10).select {|n| n % 3 == 0} # [3,6,9]
(1..10).any? {|n| n <= 5} # => true
(1..10).none? {|n| n <= 5} # => false
(1..10).all? {|n| n <= 5} # => false
(1..10).one? {|n| n <= 5} # => false
(1..10).one? {|n| n == 5} # => true

numbers = [*1..10] # => [1,2,3,4,5,6,7,8,9,10]
numbers.delete_if {|n| n <= 5} # => [6, 7, 8, 9, 10]
numbers # => [6, 7, 8, 9, 10]
numbers = [*1..10] # => [1,2,3,4,5,6,7,8,9,10]
evens = numbers.delete_if {|n| n % 2 == 1} # => [2, 4, 6, 8, 10]
```

### Map

Map always returns an **array** with the same amount of items that existed in the original item.

```ruby
x = [1,2,3,4,5]

y = x.map {|n| n * 50 } # => [50, 100, 150, 200, 250]
x # => [1, 2, 3, 4, 5]
y # => [50, 100, 150, 200, 250]

x.map! {|n| n * 50 } # => [50, 100, 150, 200, 250]
x # => [50, 100, 150, 200, 250]

fruits = ['apple', 'banana', 'pear']

cap_fruits = fruits.map do |fruit|
    fruit.capitalize if fruit == 'pear'
end # => [nil, nil, "Pear"]

cap_fruits = fruits.map do |fruit|
    fruit == 'pear' ? fruit.capitalize : fruit
end # => ["apple", "banana", "Pear"]

# this will print the fruits but the return value will be => [nil, nil, nil]
cap_fruits = fruits.map do |fruit|
    puts fruit.capitalize
end

fruits.map! do |fruit|
    fruit.capitalize
end # fruits has mutated! => ["Apple", "Banana", "Pear"]

```

### Reduce (Inject)

```ruby
[1,2,3,4,5].inject {|memo, n| memo + n} # => 15
[1,2,3,4,5].inject {|memo, n| memo * n} # => 120
[1,2,3,4,5].inject {|memo, n| memo ** n} # => 1
[2,3,4,5].inject   {|memo, n| memo ** n} # => 1152921504606846976

fruits = ['apple', 'banana', 'pear', 'orange']
longest = fruits.inject do |memo, fruit|
  if fruit.length > memo.length
    fruit
  else
    memo
  end
end
# => "banana"

# init value
size = fruits.inject(0) do |memo, fruit|
    memo + fruit.length
end
```

## Sort

Comparison Operator

```ruby
value1 <=> value2
# -1 Less than
#  0 Equal
#  1 More than
```

```ruby
array = [5,8,2,6,1,3]
array.sort # => [1, 2, 3, 5, 6, 8]
array.sort {|v1,v2| v1 <=> v2 } # => [1, 2, 3, 5, 6, 8]
array.sort {|v1,v2| v2 <=> v1 } # => [8, 6, 5, 3, 2, 1]

fruits = ['banana', 'apple', 'pear']
fruits.sort # => ["apple", "banana", "pear"]

fruits.sort do |fruit1, fruit2|
  fruit1.length <=> fruit2.length
end # => ["pear", "apple", "banana"]

fruits.sort_by {|fruit| fruit.length} # => ["pear", "apple", "banana"]

# hashes are converted into arrays and then sorted
hash = {a: 4, c: 5, b: 3}
hash.sort {|p1, p2| p1[0] <=> p2[0]} # => [[:a, 4], [:b, 3], [:c, 5]]
hash.sort {|p1, p2| p1[1] <=> p2[1]} # => [[:b, 3], [:a, 4], [:c, 5]]
```

**Reminder**: You can use the `!` operator to sort in place.

## Merge (hashes)

```ruby
h1 = {:a => 2, :b => 4, :c => 6}
h2 = {:a => 3, :b => 4, :d => 8}
```

When keys conflict, the new one wins.

```ruby
h1.merge(h2) # => {:a=>3, :b=>4, :c=>6, :d=>8}
h2.merge(h1) # => {:a=>2, :b=>4, :d=>8, :c=>6}
```

To resolve conflicts manualy, use the following block.
This block will be called only when there is a conflict and its return value will be the resolve value.

```ruby
h1.merge(h2) {|key, old, new| o } # => {:a=>2, :b=>4, :c=>6, :d=>8}
h1.merge(h2) {|key, old, new| o * 100 } # => {:a=>200, :b=>400, :c=>6, :d=>8}
```

## Methods

```ruby
def welcome(greeting, target)
  puts "#{greeting} #{target}!"
end

welcome('Hello', 'world')
welcome 'Hello', 'world' # not recommended
```

### Optional Arguments

```ruby
def welcome(greeting, name='friend', punct='!')
  greeting + ' ' + name + punct
end

puts welcome('Hello', 'neighbor', '!!!')

# A common Ruby pattern is to use an options hash
def welcome(greeting, options={})
  name = options[:name] || 'friend'
  punct = options[:punct] || '!'
  greeting + ' ' + name + punct
end

puts welcome('Hello', {:punct => '!!!'})

```

### Return Value

It's not necessary in Ruby to use an explicit `return` in the last line of the method.

```ruby
def subtract(n1, n2)
  n1 - n2
end

# Consider final operation value carefully
# especially operations that return nil
def subtract(n1, n2)
  result = n1 - n2
  result = 0 if result < 0 # if this is last, the method could return nil.
  result # restating the value makes sure this is what returns
end
```

### Return Multiple Values

```ruby
def add_and_subtract(n1, n2)
  add = n1 + n2
  sub = n1 - n2
  [add, sub]
end

result = add_and_subtract(8,3)
a = result[0] # => 11
s = result[1] # => 5

# multiple assignment using comma-delimited list of variables
a, s = add_and_subtract(8,3)
```

## Classes

```ruby
# Basic
class Person
  @first_name # instance variables

  def to_s
    @first_name
  end

  def first_name=(name)
    @first_name = name
  end

  def first_name
    @first_name
  end

end

giler = Person.new
giler.first_name = "Gil"
puts giler.first_name # => "Gil"

```

```ruby
class Student
  attr_accessor :first_name, :last_name  # auto getter / setter
  attr_reader :id # allow read only

  @first_name
  @last_name
  @id
  @static_var = 130

  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
    @id = 100
  end

  def to_s
    "#{@id}: #{@first_name} #{@last_name}"
  end

  # class method
  def self.what_am_i
    "a Student! with static_var: #{@static_var}"
  end
end

giler = Student.new("Gil", "Herr")
puts giler # => 100: Gil Herr
puts Student.what_am_i # => a Student! with static_var: 130
```

## Installing `rbenv`

[rbenv](https://github.com/rbenv/rbenv#basic-github-checkout), [ruby-build](https://github.com/rbenv/ruby-build#readme)

```bash
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
~/.rbenv/bin/rbenv init
echo 'eval "$(rbenv init -)"' >> ~/.zshrc

# install ruby-build
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build

# test if all ok
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
```

### Usage

```bash
rbenv install --list                 # lists all available versions of Ruby
rbenv install 2.2.0                  # installs Ruby 2.2.0 to ~/.rbenv/versions
```
