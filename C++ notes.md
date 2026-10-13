# 📝 C++

C++ is a compiled language. Most popular compilers are GCC and Clang.
Compiler is sequential so it reads from top to bottom so all declarations should be before main function.

## Compiler options

Compile and generate executable:

```bash
g++ main.cpp -o main
```

Generate intermediate file:

```bash
g++ -E main.cpp -o main.i
```

`.i` file is intermediate file that compiler finally sees, it doesn't contain any comment.

## Basic C++ program

```cpp
#include <iostream>

using namespace std;

int main(){
    cout << "Hello, world!" << endl;
    return 0;
}
```

## Comments

```
// single line comment

/* multi-line
comment */
```

## Variables & Data Types

Naming rules for variables:

1. Can't use any reserved keyword as name
2. Can't start with number or any symbol execpt `_`
3. Can't use any symbol, except `_` in between
4. Can use number but can't start variable name with number

Convention:

- snake_case, for variables
- CAPITAL_LETTERS for constants

### Special operators & functions

```cpp
int val = 1;
cout << sizeof(val) <<endl; // 4 as its 4 byte
cout << sizeof(int) <<endl; // 4 as its 4 byte

// checking type

#include <typeinfo>
int myInt = 42;
double myDouble = 3.14;

// Print the compiler-internal name of the type
std::cout << typeid(myInt).name() << "\n";    // Outputs 'i' (on GCC/Clang) or 'int'
std::cout << typeid(myDouble).name() << "\n"; // Outputs 'd' or 'double'

// Directly compare types
if (typeid(myInt) == typeid(int)) {
    std::cout << "myInt is an int!\n";
}
```

### Types of data-types

**I. Primitive:**

1. Integer
2. Float or Double
3. Char
4. Bool
5. Void

**II. Derived:**

1. Array
2. Pointers
3. References
4. Strings

**III. Non-primitives:**

1. Class
2. Struct
3. Enum
4. Union

#### Integers

```cpp
int var2; // garbage value, size: 4 bytes
int var2 = 0;

// variants
short int var3; // size: 2 bytes, same as short var
short unsigned int var4; // size: 2 bytes, only +ve
long int var5; // size: 8 bytes
unsigned int var6; // size: 4, only +ve numbers
long long int var7 // size: 8-16 bytes


// const
int const var8 = 12; // same as const int var = 12;

var9 = 11; // ERROR

int const var10; // Error, const value must be initialised
```

##### How computer stores integers

For +ve numbers, just convert it into binary and put it in bytes.

For -ve numbers, take 2's complement and then put it in bytes. First bit or **Most Significant Bit (MSB)** turns out to be 1, which shows sign.

Benefits of 2's complement is that you can add and subtract easily just basic binary addition and substraction.

**How to find 2's complement:**

1. Convert absolute value of number to binary
2. Take it's complement, invert all bits
3. Add 1 to it.

#### Decimals

Float: Single precision \
Double: Double precision \
Long double: Extended precision

```cpp
float var1 = 1.0; // size: 4 byte
double var2 = 2.0 // size: 8 byte

long double var3 // size: 16 byte
signed double var4 // ERROR, signed and unsigned modifier is only for integers

```

##### How computer store decimal

Decided by **IEEE 754 standard**.

#### Characters (char)

```cpp
char c = 'a'; // size: 4 bytes
// convert 'a' into ASCII code then store that number
// no other variant
```

#### Boolean (bool)

```cpp
bool b = 0; // size: 1 bytes
// 0 means false
// no other variant
```

#### Voids

```cpp
// void means nothing
void c; // Error
// void datatypes is only used as return type, can't create it's variable

void* ptr; // allowed

// void* is generic pointer, must convert it to int* or char* to de-reference it.
```

#### Arrays

```cpp
int arr1[5]; // array with garbage value

// ways to initialise

int arr2[5] = {}; // all zero
int arr[] = {1,2,3,4,5}; // size automatically decided to be 5
int arr3[5] = {1,2} // 0:1, 1:2, rest 0

// const

int const arr5 = {} // same as const int arr5 = {}
arr5[0] = 2 // Error, it's constant

// array index
std::cout << arr3[2];
```

#### References

```cpp
int& c1; // error, declaration requires initialisation
int val = 2;
int& c = val; // same as int &c = val
c = 12; // Error, reference is read-only alias

val = 12; // c is also 12.

int val2 = 1;
c = val2; // allowed

// const
int val3 = 2;
const int &c3 = val3; // same as int& const c3 = val3;
c3 = val2; // not allowed
```

#### Pointers

```cpp
int* ptr1; // size: 4 bytes(32bit), 8 bytes (64bit)
int* ptr2 = new int(); // integer ptr, pointing to 0 value on heap
int val = 2;
int* ptr3 = &val; // ptr pointing to val reference

*ptr3 = 4; // val = 4 now

// arrays
int* ptr = new int[5] {1}; // same as int pointer as it points to just first elements
std::cout << *ptr <<endl; // 1 as it points to 1st element
std::cout << *(ptr + 1) <<endl; // 0 as 2nd element is zero
// if adress of 1st element is 1001, then ptr + 1 = 1005 (as int has size 4 byte) now that points to 2nd element
std::cout << *ptr[0] <<endl; // ERROR, as *ptr is int not array

delete[] ptr;
delete ptr2;

// Const
const int* ptr4 = &val; // pointer to a const int
ptr4 = new int(12); // allowed as pointer is not const
*ptr4 = 12; // ERROR as val is considered const

int* const ptr5 = &val; // const ptr
ptr5 = new int(12); // ERROR as pointer is constant
*ptr5 = 1; // Allowed as val isn't const

int val4 = 1;
int* const ptr6 = &val4; // const ptr
*ptr5 = 1; // ERROR as val is a const
```

#### Strings

```cpp
    char str[20] = "hello"; // stores chars array with one extra char '\0' as null character that tells end of text.
    char str2[] = "hello";
    cout << str2 <<endl;

// strings from STL

#include <string>

std::string str3 = "hello";
int val = std::stoi("1234");
cout << val << "-------"<< str3 <<endl;
```

#### Struct

A struct is a user-defined data type that groups related variables of different types together under a single name.

```cpp
struct Point {
    int x;
    int y;
}


Point p;
p.x = 12;
p.y = 13;
```

#### ENUM

An `enum` creates a user-defined type with a fixed set of named integer constants, replacing magic numbers with meaningful identifiers.

1. Two Types of Enumerations:

    A. **Classic `enum` (Unscoped)**
    _ Names leak into the surrounding scope.
    _ Implicitly converts to int.

    B. **Modern `enum` class (Scoped — Recommended)**
    _ Names are hidden inside `EnumName::Value`.
    _ Strongly typed; requires static_cast<int>() to convert to int.

**Two Value Allocation Styles**

1. Default Values (Auto-Incrementing)
    - First item defaults to 0.
    - Each subsequent item automatically increases by 1.
2. Custom Values
    - Explicitly assign explicit integer values (= N).
    - Any unassigned item following a custom value increments by 1 from the previous assigned value.

```cpp
#include <iostream>
// 1. Classic Unscoped enum (Default Values: 0, 1, 2)
enum Direction {
    NORTH, // 0
    EAST,  // 1
    SOUTH  // 2
};


// 2. Classic Unscoped enum (Custom Values)
enum Priority {
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30
};


// 3. Modern Scoped enum class (Default Values: 0, 1, 2)
enum class Color {
    Red,   // 0
    Green, // 1
    Blue   // 2
};


// 4. Modern Scoped enum class (Custom Values)
enum class HttpStatus {
    OK = 200,
    NotFound = 404,
    ServerError = 500
};

int main() {
    // Unscoped usage & implicit int conversion
    Direction dir = EAST;
    int dirVal = dir; // Automatically converts to 1

    // Scoped usage (requires Scope::Value & explicit cast for int)
    HttpStatus status = HttpStatus::NotFound;
    int code = static_cast<int>(status); // 404

    std::cout << "Direction: " << dirVal << "\n";
    std::cout << "HTTP Status Code: " << code << "\n";

    return 0;
}
```

#### Type alias

```cpp
typedef int integer;
integer i = 12; // int only but named one
```

### Taking input in variables

```cpp

// integer or float or double or char or char[], let's say variable name is 'var'
cin >> var; // automatically converts
std::string str;
cin >> str; // allowed as it automatically converts
cout << str <<endl;
/*
cin: stops as soon as it hits space or enter
getline: reads even space, till newline but can modify to have custom delimiter.
*/

// default
std::getline(std::istream &stream, std::string &val); // its definition
std::getline(std::istream &stream, std::string &val, char delim); // custom delimiter

// for stdin
std::string str6;
std::getline(std::cin, str6);
cout << str6 <<endl;

// even with other types
int var5;
std::getline(std::cin, var5); // Error as it can only take string
// for int, take string then perform val = std::stoi(str)

```

### Memory Management

Memory leaks happens when pointers allocate memory on heap then pointer goes out of scope. **_Memory allocated on heap must be manually deleted otherwise it would exist till program terminates_**.

**Solution:** smart pointers

```cpp
#include <memory>

void safeMemory() {

    std::unique_ptr<int[]> ptr = std::make_unique<int[]>(1000);
    // Automatically deleted when 'ptr' goes out of scope!
    // other types are shared_ptr, weak_ptr
}

```

**Buffer Overflow & Underflow**\
_Overflow_: When you put value in variable that is beyond in range like adding 1Bn to short int \
_Underflow_: When you put value in variable that is less than least value in range like adding -ve 1Bn to short int.

**Variable Scope**\
variables automatically gets out of scope as {} square braces ends.
Once it ends, we can re-instantiate variable of same name.

## Namespaces

Namespace must be before main function and can't be defined inside any function or class.

```cpp
namespace myNameSpace {
    int val = 12;
}
int main(){
    std::cout << myNameSpace::val << endl;
}
```

## Type casting or Type conversion

Two types:

1. Implicit (Type coersion)
2. Explicit (type conversion)

```cpp
// old C-style
float j = 12.0;
int i = int(j); // same as (int) j, don't share memory

// new ways
i = static_cast<int>(j); // compile-time, don't share memory
i = dynamic_cast<int>(j); // run-time check if possible, so good for pointers, don't share memory
i = const_cast<int>(j); // used to add or remove const qualifier to variable, espeically pointer, also shares memory
i = reinterpret_cast<int>(j); // low-level, shares memory and just assumes that old memory as new data so changing i would change j

// C-style is chaotic combination of all these

// remove const with const_cast
int v = 1;
const int* ptr = &v;
*ptr = 2; // Error
int* ptr2 = const_cast<int*>(ptr);
*ptr2 = 3; // fine & even ptr points to 3 & val is 3 too.
```

## Operators & Control flow

Types of operators:

1. Arithmetic Operators: `+`, `-`, `*`, `/`, `%`
2. Comparison Operators: `<`, `>`, `==`, `<=`, `>=`
3. Logical Operators: `&&` (AND), `||` (OR), `!` (NOT)
4. Bitwise Operators: `&`, `|`, `^` (XOR), `~` (NOT)
5. Initialisation operator: `=`, `+=`, `-=`, and so on
6. Increment & Decrement: `++`, `--`, like ++X (pre-increment) and X++(Post increment -- return then add)
7. Special: `sizeof`, ternary (`?` - condition ? true: false)

**Control Flow**

```cpp
if (true){}
else{}
int var = 12;
switch (var){
 case 1: cout <<"1"; break; // else default would run anyways
 case 12: cout <<"12 yahh"; break;
 default: cout <<"oh no";
}

// loops

for(int i = 0; i < 12; ++i){
    cout<<i;
    if (i == 1){
        break;
    }else{
        continue;
    }
}
i = 0
while (true){
    i += 1;
    if (i == 1){break;}
}


do{
    cout<<'1';
}while(i < 12);


// auto loop for arrays or STL
int arr[12] = {};
for (auto a: arr){cout<<a;}

auto i = 12; // i is automatically set to int
auto j = "hello"; // j is automatically set to char[]
```

## Functions

**Argument:** variables that you pass to function\
**Parameter:**variables that you declare in function definition

> Functions must be declared before main function is they are to be used in main function. But they can be defined even below main function.

**Naming Convention**: snake_case

```cpp
// declaration & definition
int func(int value){
    return value + 1;
}

// Declartion
int func2(int v);
// Definition
int func2(int v){
    return v*2;
}

// Function Overloading - can define function with same name but different parameter
// can have same number of parameter but different type
// But can't have different return types

// overloads func2
int func2(int &v, int v2 = 0){ // uses pass by value & default value
    return v+v2;
}
```

> NOTE: When overloading function or method or even operator with different declaration and definiton then only function signature should be same, name of parameter can be different in definition and declaration.

**Can Operator be overloaded as function?**\
Yes, operators can be overloaded just like functions. The key limitation is that AT LEAST ONE operand must be a user-defined type (`class`, `struct`, or `enum`).

```cpp
struct Point
{
    int x;
    int y;
};

// return void so can't be stored in variable
void operator*(Point &p, int value)
{
    p.x = value * p.x;
    p.y = value * p.y;
}

// returns reference so can be stored
Point &operator/(Point &p, int value)
{
    p.x = p.x / value;
    p.y = p.y / value;
    return p;
}

int main(int argc, char **argv)
{
    Point p;
    p.x = 10;
    p.y = 12;

    // Multiply by 2 (returns void)
    p * 2;
    cout << "After p * 2: " << p << endl;

    // Divide by 2 (returns Point&)
    p / 2;
    cout << "After p / 2: " << p << endl;
    cout << "What they return" << endl;
    cout << "P/2: " << p / 2 << endl;
    cout << "After p / 2: " << p << endl;

    // cout << "P*2: " << p * 2 << endl; Error as p*2 returns void and void can't be display
    cout << "After p * 2: " << p << endl;
}
```

**Using multiple files:** You can have separate `.h` or `.hpp` file where you declare or define function and then you can include it into your main file.

> NOTE: when we create a separate header file we use `#pragma once` in file that we are adding like in `.h` file, so that it is only copied once.

**Magic of main function**

```cpp
int main(int argc, char** argv){
    // argc is number of strings passed
    for (int i = 0; i < argc; ++i){
        cout <<*(argv+i) <<endl;
        }
}
```

### Template programming & Generic functions

> NOTE: there shouldn't be any `;` after template and functions or class using template should be defined there only otherwise define template again

Functions or classes using template must be declared and defined together otherwise causes error.

```cpp
template<typename T> // not even necessary to put T, can be t too
T getMax(T a, T b){
    if (a>b){return a;}
    else {return b;}
}
```

**Accepting unlimited variables of different data type in function:**

```cpp
template<typename T, typename... Args> // not even necessary to put T, can be t too
T getMax(T a, Args ...args){
    cout << a;
    getMax(args...)
}
```

**Accepting unlimited variables of same data type in function:**

```cpp
#include <initializer_list>

int sum(std::initializer_list<int> args){
    int sum = 0;
    for (auto x: args){
        sum += x;
    }
    return sum;
}
```

## Error Handling

Types of Error:

1. Compile-time
2. Run-time

```cpp
try {
    throw "zero error";
}catch(char* errMsg){
    cout << errMsg <<endl;
}

// STL Errors
#include <stdexcept>

// std::exception is the parent of all STL exceptions

try{}
catch(std::out_of_range &e){
    cout << e.what()<< endl;
}
catch(std::exception &e){
    cout << e.what()<< endl;
}
```

## Object Oriented Programming

Discussed in ["Programming Paradigms Notes"](./Programming%20Paradigms.md)

## Standard Template Library (STL) in C++

The **Standard Template Library (STL)** is a collection of pre-written C++ class and function templates. Instead of implementing data structures like dynamic arrays, linked lists, or sorting algorithms by hand, STL gives you production-ready, highly optimized components.

STL rests on four fundamental pillars:

1. **Containers**
2. **Iterators**
3. **Algorithms**
4. **Functors / Lambdas**

### STL Containers

STL (Standard Template Library) containers in C++ are template classes that provide pre-implemented, highly optimized data structures to store and manage collections of elements efficiently.

C++ STL containers are broadly divided into four main categories based on how they organize and store data:

1. Sequence Containers
2. Associative Containers
3. Unordered Associative Containers
4. Container Adapters

#### 1. Sequence Containers

Sequence containers implement data structures where elements are arranged linearly and preserve their insertion order.

- `std::array`: A safe wrapper around raw static arrays. Its size is fixed at compile-time and cannot grow or shrink.

- `std::vector`: A dynamic array that can resize automatically at runtime. It is the default go-to container because it stores elements in contiguous memory, making it highly cache-friendly.

- `std::forward_list`: A singly-linked list. It only allows forward traversal but consumes less memory per element than `std::list`.

- `std::list`: A doubly-linked list. Non-contiguous memory allocation allows fast insertions or removals anywhere.

- `std::deque`: A double-ended queue. It allows fast insertion and deletion at both the beginning and the end.

```cpp

```

#### 2. Associative Containers

Associative containers store elements in a strictly sorted order (typically implemented using self-balancing binary search trees like Red-Black Trees). They look up values by a key rather than an index position.

- `std::set`: Collection of unique keys sorted by value.
- `std::map`: Collection of unique key-value pairs sorted by keys.
- `std::multiset`: Similar to a set, but allows duplicate keys.
- `std::multimap`: Similar to a map, but allows duplicate keys.

Time Complexity: $O(\log N)$ for search, insertion, and deletion.

```cpp

```

#### 3. Unordered Associative Containers

Introduced to provide faster operations, these containers organize data using hash tables instead of trees. As the name suggests, the elements are completely unsorted.

- `std::unordered_set`: Unsorted unique keys.
- `std::unordered_map`: Unsorted unique key-value pairs.
- `std::unordered_multiset`: Unsorted keys with allowed duplicates.
- `std::unordered_multimap`: Unsorted key-value pairs with allowed duplicate keys.

Time Complexity:
$O(1)$ average time complexity for search, insertion, and deletion $O(N)$ worst-case if many hash collisions occur.

```cpp

```

#### 4. Container Adapters

Container adapters are not independent data structures. Instead, they are interfaces that wrap around existing sequence containers (like vector, deque, or list) to restrict and adapt their behavior for specific logic.

- `std::stack`: Implements Last-In, First-Out (LIFO) logic. Default underlying container is std::deque.
- `std::queue`: Implements First-In, First-Out (FIFO) logic. Default underlying container is std::deque.
- `std::priority_queue`: Implements a heap structure where the top element always holds the highest priority. Default underlying container is std::vector

```cpp

```
