# Programming Paradigm

Programming paradigm is a fundamental style, model, or way of organizing and structuring computer code to solve problems.
Modern languages are multi-paradigm but main classifications are:

1. **Imperative Paradigm:** focus on how to get the result by writing explicit, step-by-step instructions that mutate state
    1. **Procedural:** breaks down a program into smaller subroutines, procedures, or functions that execute sequentially.
        - Examples: C, Pascal
    2. **Object-Oriented Programming (OOP):** Organizes code into classes and objects that bundle data and behavior together. Example C++, Java
        - Examples: Java, Python, C++
    3. **Parallel Processing:** Divides program tasks across multiple processors to run simultaneously.

2. **Declarative Paradigm:** focus on what result you want, letting the underlying language or system handle the execution details.
    1. **Functional:** uses concept of pure function. Treats function as first class citizen so it can be instantiated, copy i.e. function is like any other data type. For example: Erlang. Pure functional programming can’t give useful things as pure function dones’ have side effect I.e. it can’t change external state (so how something would be displayed). In functional programming we don’t use loop rather we use filter map, etc.. i.e. chain functions to get desired outcome.
        - Examples: Haskell, Clojure
    2. **Logic Programming:** Uses a base of facts and rules where a logical engine infers answers.
        - Examples: Prolog.
    3. **Database / Data-Driven:** Focuses on data streams and structural queries rather than imperative routines.
        - Examples: SQL

# Object Oriented Programming (OOP)

Object-Oriented Programming (OOP) is a computer coding style or programming paradigm that organizes software design around data, or objects, rather than functions and logic.

OOP is fantastic for large, complex applications where multiple developers need to collaborate on structured, organized systems.

**Class:** Class is a user-defined data type which defines its properties and its functions. Class is the only logical representation of the data.its like a blueprint or template. It defines what properties and behaviors an item will have. For example, a `Car` class defines that every car has a color and a speed. Classes do not use memory. They merely serve as a template from which items are made. Now, objects actually initialize the class members and methods when they are created, using memory in the process.

**Object:** Object is a run-time entity. It is an instance of the class. A real-world instance of a class. It takes up memory. For example, your `red sports car` is an object created from the `Car` class.

**Defining Class in C++**

```cpp
class Student{
    int roll_number;
    string name;
public:
    void print(){
        std::cout << name << " " << roll_number <<endl; // accessing class variables directly
    }
    void print_nicely(){
        (*this).print(); // same as this-> print // same as print() as we can use class methods directly but use this for clearance
        this->name = "dummy";
        print();
    }
};
```

#### Attributes & Methods

**Attributes:** Variables inside a class is called attribute.
**Methods:** Functions defined inside a class is called method.

> NOTE: it's not always necessary to instantiate a class to use it's attribute or method. We can use it directly if it's static method or attribute

#### Static Keyword

In C++, the static keyword changes the lifetime, scope, or linkage of a variable or function, depending on where it is used. At its core, static means "**persist across the entire program lifetime**" or "**shared across all instances instead of duplicated.**"

1. **Static Variables (In function)**: When you declare a variable as `static` inside a function, it is initialized only once, and its value persists between function calls. Its lifetime is the entire program, but its scope remains restricted to that function.

```cpp
void counterFunction() {
    static int count = 0; // Initialized only once!
    count++;
    cout << "Count: " << count << endl;
}

int main() {
    counterFunction(); // Output: Count: 1
    counterFunction(); // Output: Count: 2 (retains previous value)
    counterFunction(); // Output: Count: 3
    return 0;
}
```

2. Static Data Members (Inside a Class):
   When a variable is declared as `static` inside a class, it belongs to the class as a whole, rather than to any individual object.
    - Only one copy of that variable exists, shared by all objects of that class.
    - It must be defined and initialized outside the class (usually in a `.cpp` file).

```cpp
class Employee {
public:
    static int totalEmployees; // Declaration inside class

    Employee() {
        totalEmployees++; // Shared counter increments for every new object
    }
};

// Definition and initialization outside the class
int Employee::totalEmployees = 0;

int main() {
    Employee e1;
    Employee e2;
    Employee e3;

    cout << "Total Employees: " << Employee::totalEmployees << endl; // Output: 3
    return 0;
}
```

3. Static Member Functions (Inside a Class):\
   A static member function belongs to the class rather than any object.
    - **No `this` pointer:** Because it doesn't belong to a specific object, it has no this pointer.
    - **Access restriction:** It can only access other static variables or static methods. It cannot touch non-static members.
    - **How to call:** It can be called using the class name directly without creating any object (`ClassName::methodName()`).

```cpp
class MathUtils {
public:
    static int square(int x) {
        return x * x; // Can be called without creating an object of MathUtils
    }
};

int main() {
    // Calling static function directly using the class name
    int result = MathUtils::square(5);
    cout << "Square: " << result << endl; // Output: 25
    return 0;
}
```

4. Static at Global/Namespace Scope (Internal Linkage):\
   When you declare a global variable or a function as static outside of any class or function, its visibility is restricted to the current translation unit (file). It cannot be accessed from other files using the extern keyword.

```cpp
// file1.cpp
static void helperFunction() {     // Only callable inside file1.cpp
    // Do something
}
static int internalVariable = 42; // Only visible inside file1.cpp

int main(){


static SomeClass val; // exists till end of program, it's destructor would be called after main function ends.

}
```

> Note: In modern C++, anonymous namespaces are preferred for this, but static is still widely used in legacy code.

#### Access modifier

Access modifiers are keywords used to set the visibility and accessibility of classes, interfaces, constructors, methods, and variables.

Types:

- **Private:** data & methods are visible inside class only, not even derived
- **Private:** data & methods are visible to all, even user, and derived class
- **Protected:** data & methods are visible inside class and to derived class only

#### Constructor

Constructor is a special method which is invoked automatically at the time of object creation. It is used to initialize the data members of new objects generally. Constructors are only called once, at object creation.

The most common classification of constructors includes:

1. Default Constructor
2. Non-Parameterized Constructor
3. Parameterized Constructor
4. Copy Constructor

##### Default Constructor

The default constructor is a constructor that doesn't take any arguments. It is a non-parameterized constructor that is automatically defined by the compiler when no explicit constructor definition is provided. It initializes the data members to their default values.

##### Non-Parameterized Constructor

It is a user-defined constructor having no arguments or parameters.

##### Parameterized Constructor

The constructors that take some arguments are known as parameterized constructors.

##### Copy Constructor

A copy constructor is a member function that initializes an object using another object of the same class.

> In Python, we do not have built-in copy constructors like Java and C++ but we can make a workaround using different methods (`__copy__(self)`)

- A shallow copy copies object references, so both objects share the same nested data. Changes to shared data affect both objects.
- A deep copy creates a completely independent copy of the object and all its nested objects. Changes to one object do not affect the other.

> In multilevel inheritance, in `C++` constructor calling is from top-to-bottom like parent then child but in `python` you must use `super().__init__()` before using self

#### Destructor

Destructor is a method that is automatically called when the object goes out of scope or destroyed.

- In C++, the destructor name is also the same as the class name but with the (~) tilde symbol as the prefix.
- In Python, the destructor is named `__del__`.
- In java it’s automatically as it is garbage collected language.

> **NOTE**: You can overload constructor but you can’t overload destructor in C++. In python we don’t overload as it doesn’t support overload as it is dynamic language.

```cpp

```
