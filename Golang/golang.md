# Go

> Following [freeCodeCamp.org - Learn Go Programming
](https://www.youtube.com/watch?v=YS4e4q9oBaU&feature=youtu.be&t=7766) on youtube.

- [Go](#go)
  - [Dev Tools](#dev-tools)
  - [Variables](#variables)
    - [Visibility](#visibility)
    - [Casting](#casting)
  - [Primitives](#primitives)
    - [Int](#int)
    - [String](#string)
      - [Rune vs Bytes](#rune-vs-bytes)
  - [Constants](#constants)
    - [Enumarator](#enumarator)
  - [Arrays](#arrays)
  - [Slices](#slices)
  - [Maps](#maps)
  - [Struct](#struct)
    - [Anonymous Struct](#anonymous-struct)
    - [Embedding](#embedding)
    - [Tags](#tags)
  - [Control Flow](#control-flow)
    - [If Else](#if-else)
    - [Switch Statement](#switch-statement)
    - [Loops](#loops)
    - [Defer](#defer)
    - [Panic](#panic)
    - [Recover](#recover)
  - [Pointers](#pointers)
  - [Functions](#functions)
    - [Variadic function](#variadic-function)
    - [Returning a pointer from a function](#returning-a-pointer-from-a-function)
    - [Named return value](#named-return-value)
    - [Multiple Return Values](#multiple-return-values)
    - [Anonymous Function](#anonymous-function)
    - [Methods](#methods)
  - [Interfaces](#interfaces)
    - [Composition of Interfaces](#composition-of-interfaces)
    - [The Empty Interface](#the-empty-interface)
    - [Valiuse vs Pointers](#valiuse-vs-pointers)
    - [Best Practices](#best-practices)
  - [Go Routines](#go-routines)
    - [Wait Group](#wait-group)
    - [Mutex](#mutex)
    - [Summary](#summary)
  - [Channels](#channels)
    - [For Range Over Channels](#for-range-over-channels)
    - [Select Statements](#select-statements)

## Dev Tools

- [watcher](https://github.com/canthefason/go-watchr) - monitor `.go` files and rebuild them on change.

## Variables

All assignment operations in Go are *copy* operations. `slice`s and `map`s contain internal pointers, so copies point to same underlying data.

```go
var foo int         // declare
var foo int = 42    // declare, init
foo := 42           // declare, init, auto type

// var definition block
var (
    varName string = "just a string"
    varNam2 int    = 13
)
```

### Visibility

- Lowercase first letter for package scope
- Uppercase first letter to export
- No private scope

### Casting

Use `strconv` package for strings

```go
// destinationType(variabel)

var foo int = 42
var barf float32
barf = float32(i)
```

## Primitives

### Int

An integer of unspecified size. Every platform can choose to implement an int in a different size. It will be *at least* 32bit.

You can specify the size of by declaring: `int8, uint8, int16, uint16, int32, uint32, int64`

### String

Any utf-8 charecter. there are other text types that can handle different encodings.

```go
s := "this is a string"
fmt.Printf("%v, %T", s[2], s[2])            // output: 105, uint8
fmt.Printf("%v, %T", string(s[2]), s[2])    // output: i  , uint8
```

You can convert a string into a slice of bytes. Useful when sending the string over the network.

```go
s := "this is a string"
b := []byte(s)
fmt.Printf("%v, %T", b, b)
// output: [116 104 105 115 32 105 115 32 97 32 115 116 114 105 110 103], []uint8
```

#### Rune vs Bytes

> A string is a sequence of bytes, not runes.

A string can hold UTF8 encoded charecters using more than one byte to represent a single character.

The rune type is an alias for int32. It can hold the full "translation" of the UTF8 encoding, combining the encoding bytes into a single int32.

**Example:**

In the string `café` the character é is encoded using two bytes

```go
fmt.Println([]byte("café")) // [99 97 102 195 169]
fmt.Println([]rune("café")) // [99 97 102 233]
```

`é` is represented with 2 bytes [195 169], their binary representation is: `11000011 10101001`. If you seperate the UTF8 prefix with an `x` it will look like this: `110x00011 10x101001`. removing the prefix will leave you with `00011 101001` which is the binary representation of the decimal `233` (the rune).

[UTF-8](https://research.swtch.com/utf8)

## Constants

### Enumarator

- Immutable, but can be shadowed
- Replaced by the compiler at compile time
- Named like variables (PascalCase for exported, camelCase for internal)
- Typed constants are immutable variables
- Untyped constants work like literals (replaced during compile time)

Defined using `iota`. The compiler will infer the formula for the rest of the constants in the same block according to the first formula given. If only `iota` is given, it will count from 0 and up.

```go
// simple enums decleration
const (
    errorSpecialist = iota  // = 0
    catSpecialist           // = 1
    dogSpecialis            // = 2
    snakeSpecialis          // = 3
)
```

```go
// using bit shifting to allow easy bitwise operations later
const (
    isAdmin = 1 << iota
    isHeadquarters
    canSeeFinancials

    canSeeAfrica
    canSeeAsia
    canSeeEurope
)

func main() {
    var roles bye = isAdmin | canSeeFinancials | canSeeEurope
    fmt.Printf("%b\n", roles) // 100101
    fmt.Printf("Is Admin? %v\n", isAdmin & roles == isAdmin) // true
    fmt.Printf("Is HQ? %v\n", isHeadquarters & roles == isHeadquarters) // true
}
```

## Arrays

Arrays are *value* types

```go
func main() {
    grades := [3]int{97, 85, 93}

    sizes := [...]int{32, 21, 19} // size is inferred

    var students [3]string // empty array of size 3

    var identityMatrix [3][3]int
    identityMatrix[0] = [3]int{1, 0, 0}
    identityMatrix[1] = [3]int{0, 1, 0}
    identityMatrix[2] = [3]int{0, 0, 1}
}
```

Reassigning an array creates a *copy*

```go
a := [...]int{1, 2, 3}
b := a
// b := &a // assign the address of the array
b[1] = 5
fmt.Println(a) // [1 2 3]
fmt.Println(b) // [1 5 3]
```

## Slices

Slices are *reference* types

```go
a := []int{1, 2, 3}
b := a
b[1] = 5
fmt.Println(a) // [1 5 3]
fmt.Println(b) // [1 5 3]
fmt.Printf("Length: %v\n", len(a)) // Length: 3
fmt.Printf("Capacity: %v\n", len(a)) // Capacity: 3
```

Slice operations. Slice operations can also use an array as their source.

```go
a := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
b := a[:]   // [1 2 3 4 5 6 7 8 9]  slice of all elements
c := a[3:]  // [4 5 6 7 8 9]        slice from 4th elemnt to end
d := a[:6]  // [1 2 3 4 5 6]        slice first 6 elements
```

A slice can grow dynamically as you append elements to it. If the slice does not have the capacity to append a new element, it will reallocated to a bigger underlying array (double the size? not sure about that).

```go
a := []int{}
a = append(a, 1, 2, 3, 4)
a = append(a, []int{5, 6, 7, 8}...) // like js spread operator, concat slices.
```

You can specify the Capacity in advance by using the `make` function

```go
a := make([]int, 3, 100) // make(type, length, capacity)
fmt.Println(a) // [0 0 0]
len(a)) // Length : 3
cap(a)) // Capacity: 100
```

## Maps

Maps are *reference* types

Creating a map using `make`

```go
commits := make(map[string]int)
```

Map examples

```go
commits := map[string]int{ // literal map creation
    "rsc": 3711,
    "r":   2138,
    "gri": 1908,
    "adg": 912,
}
commits["rsc"] = 2222 // update
delete(commits, "rsc") // delete

missing := commits["notThere"]
fmt.Println(missing) // 0

// to overcome the confusion of missing / misspelled key, use second return value.
pop, ok := commits["gri"] // 1908, true
pop, ok := commits["notThere"] // 0, false
_, ok := commits["adg"] // use ok to check if key exists

```

## Struct

Allows you to mix types to aggregate data together.

Structs are *value* types


```go
type Doctor struct {
  number int
  actorName string
  companions []string
}

aDoctor := Doctor {
  number: 3,
  actorName: "Jon Pertwee",
  companions: []string {
    "Liz Shaw",
    "Jo Grant",
    "Sarah Jane Smith",
  },
}

aDoctor // {3 Jon Pertwee [Liz Shaw Jo Grant Sarah Jane Smith]}
aDoctor.actorName // Jon Pertwee
aDoctor.companions[1] // Jo Grant

/* optional declartion by position. not recommended.
  aDoctorPositional := Doctor {
    3,
    "Jon Pertwee",
    []string {
      "Liz Shaw",
      "Jo Grant",
      "Sarah Jane Smith",
    },
  }
*/
```

Note on naming conventions - its the same as other variable but note that if you want the fields of struct to be exported, you need to make them uppercase as well as the name of the struct itself.

### Anonymous Struct

```go
aDoctor := struct{name string}{name: "John Pertwee"}
aDoctor.name // John Pertwee
```

### Embedding

Structs doesn't have inheritance, but can use composition via embedding

```go
type Animal struct {
  Name string
  Origin string
}

type Bird struct {
  Animal
  SpeedKPH float32
  CanFly bool
}

func main() {
  b := Bird{}
  b.Name      = "Emu"
  b.Origin    = "Australia"
  b.SpeedKPH  = 48
  b.CanFly    = false

  c := Bird{
    Animal:   Animal{Name: "Emu", Origin: "Australia"},
    SpeedKPH: 48,
    CanFly:   false,
  }
}
```

### Tags

Tags can be added to struct fields to describe a field.

Used by validation programs or json for example

```go
import (
  "fmt"
  "reflect"
)

type Animal struct {
  Name   string `required max:"100"`
  Origin string
}

func main() {
  t := reflect.TypeOf(Animal{})
  field, _ := t.FieldByName("Name")
  fmt.Println(field.Tag)
}
```

## Control Flow

### If Else

```go
if someBool {
  ...
} else if someOtherBool {
  ...
} else {
  ...
}
```

If with a short statement

```go
if pop, ok := someMap["someKey"]; ok {
  fmt.Println("key exists, ok is true")
  // pop is scoped to this if block only
}

func pow(x, n, lim float64) float64 {
  if v := math.Pow(x, n); v < lim {
    return v
  }
  return lim
}
```

### Switch Statement

switch with initializer and multiple cases per case

```go
switch i := 2 + 3; i {
  case 1, 5, 10:
    ...
  case 2, 4, 6:
    ...
  default:
    ...
}
```

Another example using the cases for the logic and using the `fallthrough` statement to allow the functionallity of ommiting the `break` statement in other c based languages. Note that you can still use `break` if you need it.

```go
i := 10
switch i {
  case i <= 10:
    ...
    fallthrough
  case i <= 20:
    ...
  default:
    ...
}
```

Switch on a type

```go
var i interface{} = 1
switch i.(type) {
  case int:
    ...
  case float64:
    ...
  case string:
    ...
  case [3]int:
    ...
  default:
    ...
}
```

### Loops

basic for loop

```go
for i:=0; i<4; i++ {
  ...
}
```

for loop with multiple variables

```go
for i, j := 0, 0; i < 4; i ,j = i+1, j+1, {
  ...
}
```

`for` as a `while`

```go
i := 0
for i < 5 {
  i++
}

// forever
for {
  if someBool {
    break
  }
}
```

`break` to a label

```go
OuterLoop:
    for i := 0; i < 10; i++ {
        for j := 0; j < 10; j++ {
            fmt.Printf(“i=%v, j=%v\n”, i, j)
            break OuterLoop
        }
    }
// i=0, j=0
```

Loop Over Collections

```go
arr := []string{"Foo", "Bar"}
for index, value := range arr {
    fmt.Println(index, value)
}

// 0 Foo
// 1 Bar

m := map[string]int{
    "one":   1,
    "two":   2,
    "three": 3,
}
for k, v := range m {
    fmt.Println(k, v)
}

// two 2
// three 3
// one 1
```

String iteration - runes

```go
for i, ch := range "日本語" {
    fmt.Printf("%#U starts at byte position %d\n", ch, i)
}

// U+65E5 '日' starts at byte position 0
// U+672C '本' starts at byte position 3
// U+8A9E '語' starts at byte position 6
```

String iteration - bytes

```go
const s = "日本語"
for i := 0; i < len(s); i++ {
    fmt.Printf("%x ", s[i])
}

// e6 97 a5 e6 9c ac e8 aa 9e
```

### Defer

Moves the execution of astatement to *after* the surrounding function has returned. Useful for cleaning / closing resources when done using them.

```go
func main() {
  defer fmt.Println("world")

  fmt.Println("hello")
}
// hello
// world

res, err := http.Get("abc.com/coffee")
if err != nil {
    return err
}
defer res.Body.Close()
// continue to use `res` and dont worry about forgetting to close the Body
```

### Panic

Note that even when panic occurs, the defer statement are executed before it.

```go
func entry(lang *string, aname *string) {
    defer fmt.Println("Defer statement in the entry function")
    if lang == nil {
        panic("Error: Language cannot be nil")
    }
    if aname == nil {
        panic("Error: Author name cannot be nil")
    }
    fmt.Printf("Author Language: %s \n Author Name: %s\n", *lang, *aname)
}

func main() {
    A_lang := "GO Language"
    defer fmt.Println("Defer statement in the Main function")
    entry(&A_lang, nil)
}

// Defer statement in the entry function
// Defer statement in the Main function
// panic: Error: Author name cannot be nil
```

### Recover

> from [here](https://golangbot.com/panic-and-recover/)

Recover is useful only when called inside deferred functions. Executing a call to recover inside a deferred function stops the panicking sequence by restoring normal execution and retrieves the error message passed to the panic function call.

Note that a function that recovers, returns to its surrounding function as if it ended correctly.

```go
func recoverFullName() {  
    if r := recover(); r!= nil {
        fmt.Println("recovered from ", r)
    }
}

func fullName(firstName *string, lastName *string) {  
    // defered recover //
    defer recoverFullName()
    if firstName == nil {
        panic("runtime error: first name cannot be nil")
    }
    if lastName == nil {
        panic("runtime error: last name cannot be nil")
    }
    fmt.Printf("%s %s\n", *firstName, *lastName)
    fmt.Println("returned normally from fullName")
}

func main() {  
    defer fmt.Println("deferred call in main")
    firstName := "Elon"
    fullName(&firstName, nil)
    fmt.Println("returned normally from main")
}

// recovered from  runtime error: last name cannot be nil  
// returned normally from main  
// deferred call in main  
```

## Pointers

Unlike c, Golang doesn't allow pointer arithmatics to prevent complexity. If you really need pointer arithmatics, look for the "unsafe" go package.

```go
a := 42
b := a
fmt.Println(a, b) // 42 42
a = 27
fmt.Println(a, b) // 27 42

var c int = 42
var d *int = &a
fmt.Println(&c, d) // 0xc00002c008 0xc00002c008
fmt.Println(c, *d) // 42 42
```

Pointer to struct

```go
type Vertex struct {
    X int
    Y int
}

func main() {
    v := Vertex{1, 2}
    p := &v
    p.X = 1e9 // (*p).X = 1e9
    fmt.Println(v)
}
```

Uninitialized pointer will hold the value `<nil>`

```go
type myStruct struct {
  foo int
}

func main() {
  var ms *myStruct
  fmt.Printlln(ms)
  ms = new(myStruct)
  fmt.Println(ms)
}

// <nil>
// &{0}
```

Rmember that `maps` and `slices` are passed around by reference. The variables that hold them are pointers to the these data structures.

## Functions

When passing multiple arguments with the same type, you can ommit the type from all but the last argument.

```go
func lessTypes(firstName, LastName string) {

}
```

### Variadic function

you can only have one, and it must be at the end.

```go
func main() {
  sum(1, 2, 3, 4, 5)
}

func sum(values ...int) {
  fmt.Println(values)
  result := 0
  for _, v := range values {
    result += v
  }
  fmt.Println("The sum is ", result)
}

// [1 2 3 4 5]
// The sum is 15
```

### Returning a pointer from a function

Unlike c where the functions variable allways freed after the function call ended, Go recognize that you want to return a pointer to a local variable so it moves it to the heap.

```go
func main() {
  s := sum(1, 2, 3, 4, 5)
  fmt.Println("The sum is ", *s)
}

func sum(values ...int) *int {
  fmt.Println(values)
  result := 0
  for _, v := range values {
    result += v
  }
  return &result
}

// [1 2 3 4 5]
// The sum is 15
```

### Named return value

```go
func main() {
  s := sum(1, 2, 3, 4, 5)
  fmt.Println("The sum is ", s)
}

func sum(values ...int) (result int) {
  fmt.Println(values)
  result := 0
  for _, v := range values {
    result += v
  }
  return // return 'result' as declared in function signature
}

// [1 2 3 4 5]
// The sum is 15
```

### Multiple Return Values

```go
func main() {
  d, err := divide(5.0, 0.0)
  if err != nil {
    fmt.Println(err)
    return
  }
  fmt.Println(d)
}

func divide(a, b float64) (float64, error) {
  if b == 0.0 {
    return 0.0, fmt.Errorf("Cannot divide by zero")
  }
  return a / b, nil
}

// Cannot divide by zero
```

### Anonymous Function

```go
func main() {
  func() {
    ...
  }() // anonymous function call

  f := func() {
    ...
  }

  f()

  var f func(a, b int) (int, error)
  f = func(a, b int) (int, error) {
    return a + b, nil
  }
  fmt.Println(f(3, 2))

}
```

### Methods


```go
func main() {
  g := greeter {
    greeting: "Hello",
    name: "Go",
  }
  g.greet()
}

type greeter struct {
  greeting string
  name     string
}

// func (g *greeter) greet() { // you could pass a pointer to mutate original caller
func (g greeter) greet() {
  fmt.Println(g.greeting, g.name)
}
```

Methods can be attached to any custom type

```go
type counter int

func (c *counter) inc() counter{
  *c++
  return *c
}

func main() {

  var cnt counter = 0
  fmt.Println(cnt.inc())
  fmt.Println(cnt.inc())

}
```

## Interfaces

```go
func main() {
  var w Writer = ConsoleWriter{}
  w.Write([]byte("Hello Go!"))
}

type Writer interface {
  Write([]byte) (int, error)
}

type ConsoleWriter struct{}

func (cw ConsoleWriter) Write(data []byte) (int, error) {
  n, err := fmt.Println(string(data))
  return n, err
}
```

### Composition of Interfaces

```go
type Writer interface {
  Write([]byte)(int, error)
}

type Closer interface {
  Close() error
}

type WriterCloser interface {
  Writer
  Closer
}

type BufferedWriterCloser struct {
  buffer *bytes.Buffer
}

func (bwc *BufferedWriterCloser) Write(data []byte) (int, error) {...}
func (bwc *BufferedWriterCloser) Close() error {...}
```

### The Empty Interface

An empty interface may hold values of any type. (Every type implements at least zero methods.)
Empty interfaces are used by code that handles values of unknown type. For example, `fmt.Print` takes any number of arguments of type `interface{}`.

```go
func main() {
  var i interface{}
  describe(i) // (<nil>, <nil>)
  i = 42
  describe(i) // (42, int)
  i = "hello"
  describe(i) // (hello, string)
}

func describe(i interface{}) {
  fmt.Printf("(%v, %T)\n", i, i)
}

```

```go
func do(i interface{}) {
  switch v := i.(type) {
  case int:
    fmt.Printf("Twice %v is %v\n", v, v*2)
  case string:
    fmt.Printf("%q is %v bytes long\n", v, len(v))
  default:
    fmt.Printf("I don't know about type %T!\n", v)
  }
}

func main() {
  do(21) // Twice 21 is 42
  do("hello") // "hello" is 5 bytes long
  do(true) // I don't know about type bool!
}
```

### Valiuse vs Pointers

- Method set of **value** is all methods with value receiver
- Method set of **pointer** is all methods, regardless of receiver type

### Best Practices

- Use many, small interfaces
  - Single method interfaces are some of the most powerful and flexible
    - `io.Writer`, `io.Reader`, `inerface{}`
- Don't export interfaces for types that will be consumed
- Do export interfcaes for types that will be used by package
- Design functions and methods to receive interfaces whenever possible

## Go Routines

Most programming language us OS threads to execut conncurrent code. OS thread a expensive, large in size and needs managment.
Goroutines can be thought of as light weight threads. The cost of creating a Goroutine is tiny when compared to a thread. Hence it's common for Go applications to have thousands of Goroutines running concurrently.

 ```go
func main() {
  go sayHello()
  time.Sleep(100 * time.Millisecond)
}

func sayHello() {
  fmt.Println("Hello")
}
 ```

### Wait Group

```go
var wg = sync.WaitGroup{}

func main() {
  msg := "Hello"
  wg.Add(1)

  go func(msg string) {
    fmt.Println(msg)
    wg.Done()
  }(msg)

  msg = "Goodbye"
  wg.Wait()
}
```

### Mutex

```go
package main

import (
  "fmt"
  "sync"
  "time"
)

// SafeCounter is safe to use concurrently.
type SafeCounter struct {
  mu sync.Mutex
  v  map[string]int
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
  c.mu.Lock()
  // Lock so only one goroutine at a time can access the map c.v.
  c.v[key]++
  c.mu.Unlock()
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
  c.mu.Lock()
  // Lock so only one goroutine at a time can access the map c.v.
  defer c.mu.Unlock()
  return c.v[key]
}

func main() {
  c := SafeCounter{v: make(map[string]int)}
  for i := 0; i < 1000; i++ {
    go c.Inc("somekey")
  }

  time.Sleep(time.Second)
  fmt.Println(c.Value("somekey")) // 1000
}

```


### Summary

- When creating a goroutine, know how it will end. Avoids subtle memory leaks
- Chcek for race conditions using the compiler flag `-race` that tells you if there is a data race in your program
- When using anonymous functions, pass data as local variables
- Synchronization
  - use `sync.WaitGroup` to wait for groups of goroutines to complete
  - use `sync.Mutex` and `sync.RWMutex` to protect data access
- Parallelism
  - By default, Go will use CPU threads equal to available cores
  - Change with `runtime.GOMAXPROCS
  - More threads can increase performance, but too many can slow it down.

## Channels

Unbuffered channel can work with a single messege at a time. Meaning that if a goroutin is trying to push a messege to a channel and its full, it will pause the execusion until something reads from that channel.

```go
var wg = sync.WaitGroup{}

func main() {
  ch := make(chan int)
  wg.Add(2)
  go func() {
    i := <-ch
    fmt.Println(i)
    wg.Done()
  }()
  go func() {
    ch <- 42
    wg.Done()
  }()
  wg.Wait()
}
```

Its a good practice to dedicate goroutins to only send OR receive from a channel, not both.

```go
var wg = sync.WaitGroup{}

func main() {
  ch := make(chan int)
  wg.Add(2)
  go func(ch <-chan int) { // receive only
    i := <- ch
    fmt.Println(i)
    wg.Done()
  }(ch)
  go func(ch chan<- int) { // send only
    ch <- 42
    wg.Done()
  }(ch)
  wg.Wait()
}
```

To create a buffered channel use `make(chan T, bufferSize)` to allocate `bufferSize` slots to store messeges in.

### For Range Over Channels

Range runs the loop for each element in the channel. In order for it to know that it reached the end of the channel, someone needs to `close(ch)` the channel.

```go
var wg = sync.WaitGroup{}

func main() {
  ch := make(chan int)
  wg.Add(2)

  go func(ch <-chan int) {
    for i := range ch {
      fmt.Println(i)
    }
    wg.Done()
  }(ch)

  go func(ch chan<- int) {
    ch <- 42
    ch <- 27
    close(ch)
    wg.Done()
  }(ch)

  wg.Wait()
}

```

The receiver side can also use the `if ok` to query the channel.

```go
go func(ch <-chan int) {
  for {
    if i, ok := <-ch; ok {
      fmt.Println(i)
    } else {
      break
    }
  }
  wg.Done()
}(ch)
```

### Select Statements

Select statement (without `default`) **blocks** execution until it can send or receive data from the specified channels.

from [Tour of go](https://tour.golang.org/concurrency/5)

```go
package main

import "fmt"

func fibonacci(c, quit chan int) {
  x, y := 0, 1
  for {
    select {
    case c <- x: // if I can send to c:
      x, y = y, x+y
    case <-quit: // If I can receive from quit:
      fmt.Println("quit")
      return
    }
  }
}

func main() {
  c := make(chan int)
  quit := make(chan int)
  go func() {
    for i := 0; i < 10; i++ {
      fmt.Println(<-c) // read in from c
    }
    quit <- 0 // send to quit to kill the main process.
  }()
  fibonacci(c, quit)
}

```
