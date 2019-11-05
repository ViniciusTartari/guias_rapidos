# Go Programming Language Guide

My basic guide to go programming language - Vinicius Tartari

## **Variable declaration**

- `var foo int`
- `var foo int = 42`
- `foo := 42`

- _Can't redeclare variables, but can shadow them_
- _All variables must be used_

### **Visibility**

- lower case first letter for package scope
- upper case first letter to export
- no private scope

### **Naming conventions**

- Pascal or camelCase
  - Capitalize acronyms(HTTP URL)
- As short as reasonable
  - longer names for longer lives

### **Type conversions**

- destinationType(variable)
- use strconv package for strings

### **Boolean type**

- Values are true or false
- Not an alias for other types (e.g. int)
- Zero value is false

### **Numeric types**

#### **Integers**

- Signed integers
  - int type has varying size, but min 32 bits
  - 8 bit (int8) through 64 bit (int64)
- Unsigned integers
  - 8 bit (byte and uint8) through 32 bit (uint32)
- Arithmetic operations
  - Addition, subtraction, multiplication, division, remainder
- Bitwise operations
  - And, or, xor and not
- Zero value is 0

- Can't mix types in same family! (uint16 + uint32 = error)

#### **Floating point numbers**

- Follow IEEE-754 standard
- Zero value is 0
- 32 and 64 bit versions
- Literal styles
  - Decimal (3.14)
  - Exponential (13e18 or 2E10)
  - Mixed (13.6e12)
- Arithmetic operations
  - Addition, subtraction, multiplication, division

#### **Complex numbers**

- Zero value is (0 + 0i)
- 64 and 128 bit versions
- Built-in functions
  - complex - make complex number from two floats
  - real - get real part as float
  - imag - get imaginary part as float
- Arithmetic operations
  - Addition, subtraction, multiplication, division

### **Text types**

#### **Strings**

- UTF-8
- Immutable
- Can be concatenated with plus (+) operator
- Can be converted to []byte

#### **Rune**

- UTF-32
- Alias for int32
- Special methods normally required to process
  - e.g. strings.Reader#ReadRune

### **Constants**

- Immutable, but can be shadowed
- Replaced by the compiler at compile time
  - Value must be calculable at compile time
- Named like variables
  - PascalCase for exported constants
  - camelCase for internal constants
- Typed constants work like immutable variabels
  - Can interoperate only with same type
- Untyped constants work like literals
  - Can interoperate with similar types

#### **Enumerated constants**

- Special symbol _iota_ allows related constants to be created easily
- _Iota_ starts at 0 in each const block and increments by one
- Watch out of constant values that match zero values for variables

#### **Enumerated expressions**

- Operations that can be determined at compile time are allowed
  - Arithmetic
  - Bitwise operations
  - Bit shifting

### **Arrays**

- Collection of items with same type
- Fixed size
- Declaration styles
  - `a := [3]int{1,2,3}`
  - `a := [...]int{1,2,3}`
  - `var a [3]int`
- Access via zero-based index
  - `a := [3]int {1,2,3} // a[1] ==3`
- _len_ function return size of array
- Copies refer to different underlying data

### **Slices**

- Backed by array
- Creation styles
  - Slice existing array or slice
  - Literal style
  - Via _make_ function
    - `a := make([]int, 10) // create slice with capacity and length == 10`
    - `a := make([]int, 10, 100) // slice with length == 10 and capacity == 100`
- _len_ function returns length of slice
- _cap_ function return length of underlying array
- _append_ function to add elements to slice
  - May cause expensive copy operation if underlying array is too small
- Copies refer to same underlying array

### **Maps**

- Collections of value types that are accessed via keys
- Created via literals or via _make_ function
- Members accessed via [*key*] syntax
  - `myMap["key"] = "value"`
- Check for presence with "value, ok" form of result
- Multiple assignments refer to same underlying data

### Structs

- Collections of disparate data types that describe a single concept
- Keyed by named fields
- Normally created as types, but anonymous structs are allowed
- Structs are value types
- No inheritance, but can use composition via embedding
- Tags can be added to struct fields to describe field

### Decision

#### **If statements**

- Initializer

#### **Switch statements**

- Switching on a tag
- Initializers
- Switches without tag
- Fallthrough

### Looping

#### **For statements**

- Simple loops
  - `for initializer; test; incrementer{}`
  - `for test{}`
  - `for{}`
- Exiting early
  - _break_
  - _continue_
  - _labels_
- Looping over collections
  - Arrays, slices, maps, strings, channels
  - `for k,v := range collection {}`

### Control flow

#### Defer

- Used to delay execution of a statement until function exists
- Useful to group "open" and "close" functions together
  - Be careful in loops
- Run in LIFO (last in, first out) order
- Arguments evaluated at time defer is executed, not at time of called function execution

#### Panic

- Occur when program cannot continue at all
  - Don't use when file can't be opened, unless it is critical
  - Use for unrecoverable events - cannot obtain TPC port for web server
- Function will stop executing
  - Deferred functions will still fire
- If nothing handles panic, program will exit

#### Recover

- Used to recover from panics
- Only useful in deferred functions
- Current function will not attempt to continue, but higher functions in call stack will

### Pointers

#### **Creating pointers**

- Pointer types use an asterisk (\*) as a prefix to type pointed to
  - \*int - a pointer to an integer
- Use the addressof operator (&) to get address of variable

#### **Dereferencing pointers**

- Dereference a pointer by preceding with an asterisk (\*)
- Complex types (e.g. structs) are automatically dereferenced

#### **Create pointer to objects**

- Can use the addressof operator (&) if value type already exists

  ```go
  ms := myStruct{ foo: 42 }
  p := &ms
  ```

- Use adressof operator before initializer

  - `&myStruct{ foo: 42 }`

- Use the _new_ keyword

  - Can't initialize fields at the same time

#### **Types with internal pointers**

- All assignment operations in Go are copy operations
- Slices and maps contain internal pointers, so copies point to same underlying data

### Functions

#### **Basic syntax**

- `func foo() {}`

#### **Parameters**

- Comma delimited list of variables and types
  - `func foo(bar string, baz int)`
- Parameters of same type list once
  - `func foo(bar, baz int)`
- When pointers are passed in, the function can change the value in the caller
  - This is always true for data of slices and maps
- Use variadic parameters to send list of same types in
  - Must be last parameter
  - Received as a slice
  - `func foo(bar string, baz ...int)`

#### **Return values**

- Single return values just list type
  - `func foo() int {}`
- Multiple return value list types sorounded by parentheses
  - `func foo() (int, error) {}`
  - The (result type, error) paradigm is very common idiom
- Can use named return values
  - Initializes returned variables
  - Return using _return_ keyword on its own
- Can return address of local variables
  - Automatically promoted from local memory (stack) to shared memory (heap)

#### **Anonymous functions**

- Functions don't have name if they are:

  - Immediately invoked

    ```go
    func () {
        ...
    } ()
    ```

- Assigned to a variable or passed as an argument to a function

  ```go
  a := func() {
      ...
  }
  a()
  ```

#### **Functions as types**

- Can assign functions to variables or use as arguments and return values in functions
- Type signature is like functions signature, with no parameter names
  - `var f func(string, string, int) (int, error)`

#### **Methods**

- Function that executes in context of a type

- Format

  ```go
  func (g greeter) greet() {
      ...
  }
  ```

- Receiver can be value or pointer

  - Value receiver gets copy of type
  - Pointer receiver gets pointer to type

### Interfaces

#### Basics

```go
type Writer interface {
    Write([]byte)(int, error)
}
type ConsoleWriter struct {}
func (cw ConsoleWriter) Write(data []byte)(int, error){
    n,err := fmt.Println(string(data))
    return n,err
}
```

#### Composing interfaces

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
```

#### Type conversion

```go
var wc WriterCloser = NewBufferedWriterCloser()
bwc := wc.(*BufferedWriterCloser)
```

#### The empty Interface and type switches

```go
var i interface{} = 0
switch i.(type){
  case int:
    fmt.Println("i is an integer")
  case string:
    fmt.Println("i is a string")
  default:
    fmt.Println("I don't know what i is")
}
```

#### Implementing with values vs pointers

- Method set of **value** is all methods with value receivers
- Method set of **pointer** is all methods, regardless of receiver type

#### Best Practices

- Use many, small interfaces

  - Single method interfaces are some of the most powerful and flexible

    ```go
    io.Writer, io.Reader, interface {}
    ```

- Don't export interfaces for types that will be consumed

- Do export interfaces for types that will be used by package

- Design functions and methods to receive interfaces whenever possible

### Goroutines

#### Creating goroutines

- Use go keyword in front of function call
- When using anonymous functions, pass data as local variables

#### Synchronization

- Use `sync.WaitGroup` to wait for groups of goroutines to complete
- Use `sync.Mutex` and `sync.RWMutex` to protect data access

#### Parallelism

- By Default, Go will use CPU threads equal to available cores
- Change with `runtime.GOMAXPROCS`
- More threads can increase performance, but too many can slow it down

#### Best Practices

- Don't create goroutines in libraries
  - Let consumer control concurrency
- When creating a goroutine, know how it will end
  - Avoids subtle memory leaks
- Check for race conditions at compile time

### Channels

#### Basics

- Create a channel with `make` command
  - `make(chan int)`
- Send message into channel
  - `ch <- val`
- Receive message from channel
  - `val := <-ch`
- Can have multiple senders and receivers

#### Restricting data flow

- Channel can be cast into send-only or receive only versions
  - Send-only: `chan <- int`
  - Receive-only: `<- chan int`

#### Buffered channels

- Channels block sender side till receiver is available
- Block receiver side till message is available
- Can decouple sender and receiver with buffered channels
  - `make(chan int, 50)`
- Use buffered channels when sender and receiver have asymmetric loading

#### For...range loops

- Use to monitor channel and process messages as they arrive
- Loop exists when channel is closed

#### Select statements

- Allows goroutines to monitor several channels at once
  - Blocks if all channels block
  - If multiple channels receive value simultaneously, behavior is undefined
