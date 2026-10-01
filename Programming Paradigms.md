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

// Naming convention is PascalCase
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
5. Move Constructor

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

#### Destructor

Destructor is a method that is automatically called when the object goes out of scope or destroyed.

- In C++, the destructor name is also the same as the class name but with the (~) tilde symbol as the prefix.
- In Python, the destructor is named `__del__`.
- In java it’s automatically as it is garbage collected language.

> **NOTE**: You can overload constructor but you can’t overload destructor in C++. In python we don’t overload as it doesn’t support overload as it is dynamic language.

```cpp
class Student
{
private:
    string *name = nullptr;
    int roll_number = 0;

public:
    // Default or Non-parameterized constructor
    Student()
    {
        cout << "Default / Non-parameterized constructor called" << endl;
    }
    // both can't have default value otherwise give error -- more than one default constructor
    Student(int roll_number, string name = "Unknown")
    {
        this->name = new string(name);
        this->roll_number = roll_number;
        cout << "Parameterized constructor called for " << name << endl;
    }

    // copy constructor
    Student(Student &other)
    {
        this->roll_number = other.roll_number;
        this->name = new string(*other.name);
        cout << "Copy constructor is called for " << *name << endl;
    }
    // move constructor
    Student(Student &&other)
    {
        this->name = other.name;
        this->roll_number = other.roll_number;
        other.name = nullptr;
        cout << "Move constructor is called for " << *name << endl;
    }
    // destructor -- can't be parametrised & can't be overloaded
    ~Student()
    {
        cout << "Destructor is called for " << endl;
        delete name;
    }
};
Student createStudent()
{
    return Student(1, "Newbie");
}
int main(int argc, char **argv)
{
    Student newStudent;
    Student guy(12, "guy"); // calling parameterised constructor

    Student oldStudent = Student(12, "Old"); // copy constructor called
    Student newerStudent = oldStudent;
    Student newbie = createStudent();       // calls copy constructor due to C++ 17 compiler optimisation
    Student newGuy = std::move(oldStudent); // calls move constructor to move old to new
}
```

## 4 Pillars of OOP

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

They are called "**pillars**" because of an architectural metaphor: just like physical stone pillars hold up the roof of a heavy building, these four concepts hold up the entire weight and philosophy of Object-Oriented Programming.
Without them, OOP wouldn't exist—you would just be back to writing procedural code or passive data containers (like C structs).
Each pillar carries a specific structural load that transforms how code is built:

- **Encapsulation** bears the load of security and state protection (keeping data safe inside a boundary).
- **Abstraction** bears the load of simplicity and interface design (hiding overwhelming complexity behind clean buttons).
- **Inheritance** bears the load of reusability and organization (stopping you from rewriting code by creating parent-child relationships).
- **Polymorphism** bears the load of flexibility and decoupling (allowing different objects to respond to the exact same command in their own way).

### 1. Encapsulation

Encapsulation is the binding of data and methods that manipulate them into a single unit such that the sensitive data is hidden from the usersIt is implemented as the processes mentioned below:

1. **Data hiding**: A language feature to restrict access to members of an object. For example, private and protected members in C++.
2. **Bundling of data and methods together**: Data and methods that operate on that data are bundled together. For example, the data members and member methods that operate on them are wrapped into a single unit known as a class.

> In c++ we can do data hiding using **access modifiers** & Bundling using **class** keyword.

### 2. Data Abstraction

Abstraction is similar to data encapsulation and is very important in OOP. It means showing only the necessary information and hiding the other irrelevant information from the user. Abstraction is implemented using classes and interfaces.

#### Encapsulation vs Data Abstraction

Encapsulation restricts access to certain internal data like think of example on an ORM. If you build an ORM and decides to use struct of C then surely you can create multiple variables inside that stuct like db connection etc... But then maybe someone can close db in some function without your knowledge and then db starts failing. And also for inserting or deleting data in db you’ll have to write bunch of codes like connect then send this SQL COMMAND then do something else. In oops we use encapsulation to ensures that you don’t access internal db connections so that it doesn’t get corrupt. And what abstraction does is it helps to declutter things like instead of doing all those process yourself you give simple method .insert and then user can give data and you hide all underlying thing of connection, SQL or No-Sql command. user dont’ need to know SQL or No-SQL to insert in DB, it can do it with just this one method.

### 3. Inheritance

The idea of inheritance is simple, a class is derived from another class and uses data and implementation of that other class. The class which is derived is called child or derived or subclass and the class from which the child class is derived is called parent or base or superclass.
The main purpose of Inheritance is to increase code reusability. It is also used to achieve Runtime Polymorphism.

> In C++, we have different modes of inheritance & it's unique to C++.

#### Modes of Inheritance

**Modes of Inheritance** define how the public, protected, and private members of a base class are inherited and accessed by the derived class.

Three modes of Inheritance in C++:

| Base Class Access | Inherited as `Private` | Inherited as `Protected` | Inherited as `Public` |
| ----------------- | ---------------------- | ------------------------ | --------------------- |
| **Private**       | Not inherited          | Not inherited            | Not inherited         |
| **Protected**     | Private                | Protected                | Protected             |
| **Public**        | Private                | Protected                | Public                |

**NOTE:** By not inherited I mean you can't access these attributes or methods directly in child but as it is derived from base it does has all private properties of base. And if base has public or protected method to access and modify those private variables then you can modify from child class too.

**This table is to show how class in general behave like if base has something public and you inherit it publicly then object can use that attribute but when inherited using protected then object of child can't use that cuz it's now protected.**

```cpp

#include <iostream>
#include <string>
using namespace std;

class Vehicle
{
private:
    int engine_number = 0;

protected:
    string manufacturer = "me";
    int get_engine_no() { return engine_number; }

public:
    string model = "simple one";

    Vehicle()
    {
        cout << "Vehicle's Default constructor called" << endl;
    }

    Vehicle(int engine, string manufacturer, string model)
    {
        this->engine_number = engine;
        this->manufacturer = manufacturer;
        this->model = model;
        cout << "Vehicle's parameterised constructor called" << endl;
    }
    void print_all()
    {
        cout << "Engine number: " << engine_number;
        cout << " Manufacturer: " << manufacturer;
        cout << " Model: " << model << endl;
    }

    ~Vehicle()
    {
        cout << "Vehicle destructor called" << endl;
    }
};

// public inheritance
class Bike : public Vehicle
{
public:
    Bike()
    {
        cout << "Bike default constructor" << endl
             << endl; // parent's default constructor automatically called.
    }
    // Bike(int engine, string manufacturer, string model ){} -- parent's default constructor called so no value is set
    Bike(int engine, string manufacturer, string model) : Vehicle(engine, manufacturer, model)
    {
        // intensionally calls parent's parameterised constructor
        // intensionally calls parent's parameterised constructor
        cout << "Bike's parameterised constructor" << endl;
        cout << "Manufacturer: " << manufacturer << " Model: " << model;
        // cout << " Engine: " << engine_number;  Error as it's private
        cout << " Engine: " << get_engine_no() << endl
             << endl;
    }
    ~Bike()
    {
        cout << "Bike's destructor" << endl
             << endl;
    }
};

// protected inheritance
class Car : protected Vehicle
{
public:
    Car()
    {
        cout << "Car default constructor" << endl
             << endl; // parent's default constructor automatically called.
    }
    // Bike(int engine, string manufacturer, string model ){} -- parent's default constructor called so no value is set
    Car(int engine, string manufacturer, string model) : Vehicle(engine, manufacturer, model)
    {
        cout << "Car's parameterised constructor" << endl;
        cout << "Manufacturer: " << manufacturer << " Model: " << model;
        cout << " Engine: " << get_engine_no() << endl
             << endl;
    }
    ~Car()
    {
        cout << "Car's destructor" << endl
             << endl;
    }
};

// private inheritance
class Truck : private Vehicle
{
public:
    Truck()
    {
        cout << "Truck default constructor" << endl
             << endl; // parent's default constructor automatically called.
    }

    Truck(int engine, string manufacturer, string model)
    {
        // parent's default constructor is called automatically but not parametrised.
        // intensionally calls parent's parameterised constructor
        cout << "Truck's parameterised constructor" << endl;
        cout << "Manufacturer: " << manufacturer << " Model: " << model;
        cout << " Engine: " << get_engine_no() << endl
             << endl;
        ; // Error as it's private
    }

    void print()
    {
        cout << "\n\nPrinitng..\n";
        this->print_all();
        cout << "\n";
    }
    ~Truck()
    {
        cout << "Truck's destructor" << endl
             << endl;
    }
};

int main(int argc, char **argv)
{
    Bike tvs;
    Bike bajaj(12, "Bajaj", "Pulsar");
    Car suzuki;
    Car mahindra(12, "Bajaj", "Pulsar");
    Truck ashok_leyland;
    Truck tata(12, "Bajaj", "Pulsar");

    cout << "For bike:" << endl;
    // cout << "Engine number: " << bajaj.engine_number;                    Error as it's not accessible
    // cout << "Engine number: " << bajaj.get_engine_no();                  Error as it's not accessible
    // cout << " Manufacturer: " << bajaj.manufacturer;                     Error as it's not accessible
    cout << " Model: " << bajaj.model;

    cout << "\nFor Car:" << endl;
    // cout << "Engine number: " << mahindra.engine_number;                     Error as it's not accessible
    // cout << "Engine number: " << ˝mahindra.get_engine_no();                   Error as it's not accessible
    // cout << " Manufacturer: " << mahindra.manufacturer;                  Error as it's not accessible
    // cout << " Model: " << mahindra.model;                    Error as it's not accessible

    cout << "\nFor Truck:" << endl;
    // cout << "Engine number: " << tata.engine_number;                     Error as it's not accessible
    // cout << "Engine number: " << tata.get_engine_no();                   Error as it's not accessible
    // cout << " Manufacturer: " << tata.manufacturer;                  Error as it's not accessible
    // cout << " Model: " << tata.model;                    Error as it's not accessible

    // proof that even after inheriting privately child does contains all base class attributes
    tata.print();
}
```

> In C++, Private members of a base class are never directly accessible by a derived class, regardless of the inheritance mode (they require public/protected getter and setter methods).\
> When base doesn't has any parameterised constructor then it would be automatically called but when it has parameterised constructor and we want to call that then we'll have to call it explicity.

#### Types of inheritance:

1. **Single Inheritance**: Child class derived directly from the base class

```cpp
#include <iostream>

class Animal {
public:
    void eat() {
        std::cout << "Eating..." << std::endl;
    }
};

// Dog inherits from Animal
class Dog : public Animal {
public:
    void bark() {
        std::cout << "Barking..." << std::endl;
    }
};

int main() {
    Dog dog;
    dog.eat();  // Inherited from Animal
    dog.bark(); // Defined in Dog
    return 0;
}
```

2. **Multilevel Inheritance**: Child class derived from the class which is also derived from another base class.

```cpp
#include <iostream>

class Vehicle {
public:
    void start() {
        std::cout << "Vehicle started." << std::endl;
    }
};

// Car inherits from Vehicle
class Car : public Vehicle {
public:
    void drive() {
        std::cout << "Driving car..." << std::endl;
    }
};

// SportsCar inherits from Car
class SportsCar : public Car {
public:
    void turboBoost() {
        std::cout << "Turbo boost activated!" << std::endl;
    }
};

int main() {
    SportsCar myCar;
    myCar.start();      // From Vehicle
    myCar.drive();      // From Car
    myCar.turboBoost(); // From SportsCar
    return 0;
}
```

> In multilevel inheritance, in `C++` constructor calling is from top-to-bottom like parent then child but in `python` you must use `super().__init__()` before using self. For **Destructor** order is LIFO i.e. Child class destructor is called first then base class.

3. **Multiple Inheritance**: Child class derived from multiple base classes.

```cpp
#include <iostream>

class Printer {
public:
    void print() {
        std::cout << "Printing document..." << std::endl;
    }
};

class Scanner {
public:
    void scan() {
        std::cout << "Scanning document..." << std::endl;
    }
};

// AllInOnePrinter inherits from both Printer and Scanner
class AllInOnePrinter : public Printer, public Scanner {
public:
    void fax() {
        std::cout << "Sending fax..." << std::endl;
    }
};

int main() {
    AllInOnePrinter machine;
    machine.print(); // From Printer
    machine.scan();  // From Scanner
    machine.fax();   // From AllInOnePrinter
    return 0;
}
```

4. **Hierarchical Inheritance**: Multiple child classes derived from a single base class.

```cpp
#include <iostream>

class Shape {
public:
    void draw() {
        std::cout << "Drawing shape..." << std::endl;
    }
};

// Circle inherits from Shape
class Circle : public Shape {
public:
    void calculateRadius() {
        std::cout << "Calculating circle radius..." << std::endl;
    }
};

// Rectangle inherits from Shape
class Rectangle : public Shape {
public:
    void calculateArea() {
        std::cout << "Calculating rectangle area..." << std::endl;
    }
};

int main() {
    Circle c;
    Rectangle r;

    c.draw();             // From Shape
    c.calculateRadius();  // From Circle

    r.draw();             // From Shape
    r.calculateArea();    // From Rectangle

    return 0;
}
```

5. **Hybrid Inheritance**: Inheritance consisting of multiple inheritance types of the above specified. A classic scenario is the Diamond Problem (combining Hierarchical + Multiple Inheritance), which requires `virtual` inheritance to avoid duplicate base copies.

```cpp
#include <iostream>

class Person {
public:
    void showRole() {
        std::cout << "I am a person." << std::endl;
    }
};

// Virtual inheritance solves the diamond problem
class Student : virtual public Person {
public:
    void study() {
        std::cout << "Studying..." << std::endl;
    }
};

class Faculty : virtual public Person {
public:
    void teach() {
        std::cout << "Teaching..." << std::endl;
    }
};

// Teaching Assistant inherits from both Student and Faculty
class TA : public Student, public Faculty {
public:
    void assist() {
        std::cout << "Assisting in lab..." << std::endl;
    }
};

int main() {
    TA ta;
    ta.showRole(); // Works unambiguously because of 'virtual public Person'
    // if not use virtual inheritance then gives error
    ta.study();    // From Student
    ta.teach();    // From Faculty
    ta.assist();   // From TA
    return 0;
}
```

**How virtual inheritance works?**\
When you use `virtual` keyword in inheritance, it checks for duplication i.e. if two or more class has same base class then it keeps only one copy and then provides other class virtual pointer to base class(vbptr). `vbptr` is compiler internal we can't use it.

When we inherit without virtual keyword then compiler doesn't look for duplication. And if we have classes with different base class then virtual keyword would work just as without keyword as there is no duplication.

##### How other languages solve "DIAMOND PROBLEM"?

**Java/C#** prevent it by leaving multiple inheritance altogether. They use interfaces. \
**Python** uses MRO (Method resolution order) that says whichever parent class is first that's base calss would be called.

##### Interface vs Abstract class

**Abstract class:**\
In general terms, an **abstract** class is a class that is intended to be used for inheritance. It cannot be instantiated. An abstract class can consist of both abstract and non-abstract methods.

- In C++, an abstract class is a class that contains at least one pure virtual function.
- In Java and C#, an abstract class is declared with an abstract keyword.

**Interface:**\
A unique class type that contains methods but not their definitions. Inside an interface, only method declaration is permitted. You cannot make objects using an interface.

**Abstract class vs Interface**
| Feature | Abstract Class | Interface |
|---|---|---|
|Primary Intent |"**Is-A**" Relationship: Provides a common base with partial implementation for closely related classes. | "**Can-Do**" Relationship: Defines a strict behavioral contract for potentially unrelated classes. |
|State / Variables |Can have state (member variables like `int x`, `std::string` name). | Stateless: Should not contain instance variables (only constant definitions, if any).|
|Method Implementations | Can have a mix of pure virtual functions and concrete methods with code. | All methods are pure virtual functions (`= 0`) with no bodies. |
|Constructors / Destructors | Has constructors and a virtual destructor. | No constructors needed; has a pure/empty virtual destructor.|
|Multiple Inheritance | Classes typically inherit implementation from only one primary abstract base class. | A class can implement multiple interfaces without diamond-problem issues. |

**Why create constructor in abstract class if it can't be instantiated?**\
It's because it can still be called automatically when child's constructor is called.

> NOTE: Both `abstract class` and `interface` can be used a base data type for variable storing any of its children.

```cpp
#include <iostream>
#include <string>
#include <vector>

// ==========================================
// 1. INTERFACE (Pure Abstract Class)
// - Stateless (no member variables)
// - ALL functions are pure virtual (= 0)
// - Has a virtual destructor
// ==========================================
class IPrintable {
public:
    virtual ~IPrintable() = default;
    virtual void printDetails() const = 0; // Pure virtual function
};


// ==========================================
// 2. ABSTRACT CLASS
// - Can have state (member variables)
// - Can have constructors
// - Has at least ONE pure virtual function
// - Can contain both concrete and pure virtual methods
// ==========================================
class Employee {
protected:
    std::string name;
    int id;

public:
    // Constructor to initialize base state
    Employee(const std::string& empName, int empId)
        : name(empName), id(empId) {}

    // Virtual destructor for safe polymorphic cleanup
    virtual ~Employee() = default;

    // Concrete method shared by all employees
    void showHeader() const {
        std::cout << "--- Employee ID: " << id << " ---" << std::endl;
    }

    // Pure virtual function makes this class Abstract
    virtual double calculateSalary() const = 0;
};


// ==========================================
// 3. CONCRETE CLASS
// - Inherits from the Abstract Class (Employee)
// - Implements the Interface (IPrintable)
// - MUST implement all pure virtual functions to be instantiated
// ==========================================
class FullTimeEmployee : public Employee, public IPrintable {
private:
    double monthlySalary;

public:
    FullTimeEmployee(const std::string& empName, int empId, double salary)
        : Employee(empName, empId), monthlySalary(salary) {}

    // Overriding pure virtual function from Employee
    double calculateSalary() const override {
        return monthlySalary;
    }

    // Overriding pure virtual function from IPrintable
    void printDetails() const override {
        showHeader();
        std::cout << "Name: " << name << std::endl;
        std::cout << "Type: Full-Time" << std::endl;
        std::cout << "Salary: $" << calculateSalary() << std::endl;
    }
};

class ContractEmployee : public Employee, public IPrintable {
private:
    double hourlyRate;
    int hoursWorked;

public:
    ContractEmployee(const std::string& empName, int empId, double rate, int hours)
        : Employee(empName, empId), hourlyRate(rate), hoursWorked(hours) {}

    // Overriding pure virtual function from Employee
    double calculateSalary() const override {
        return hourlyRate * hoursWorked;
    }

    // Overriding pure virtual function from IPrintable
    void printDetails() const override {
        showHeader();
        std::cout << "Name: " << name << std::endl;
        std::cout << "Type: Contract" << std::endl;
        std::cout << "Salary: $" << calculateSalary() << std::endl;
    }
};


// ==========================================
// 4. MAIN FUNCTION (Polymorphism in action)
// ==========================================
int main() {
    // ❌ Cannot instantiate abstract class or interface directly:
    // Employee emp("John", 101);     // Error!
    // IPrintable printable;          // Error!

    // ✅ Storing concrete instances inside Abstract Class and Interface pointers
    Employee* emp1 = new FullTimeEmployee("Alice", 101, 5000.0);
    Employee* emp2 = new ContractEmployee("Bob", 102, 40.0, 120);

    std::cout << "=== Salary Calculations ===" << std::endl;
    std::cout << "Alice Salary: $" << emp1->calculateSalary() << std::endl;
    std::cout << "Bob Salary: $" << emp2->calculateSalary() << std::endl;
    std::cout << std::endl;

    // ✅ Using the Interface pointer in a polymorphic collection
    std::vector<IPrintable*> printableItems;
    printableItems.push_back(dynamic_cast<IPrintable*>(emp1));
    printableItems.push_back(dynamic_cast<IPrintable*>(emp2));

    std::cout << "=== Printable Items ===" << std::endl;
    for (const auto* item : printableItems) {
        item->printDetails();
        std::cout << std::endl;
    }

    // Cleanup
    delete emp1;
    delete emp2;

    return 0;
}
```

> NOTE: A class that implements `interface` must implement all of its features in order to be instantiable.

##### How to stop further inheritance?

**Stopping Inheritance:**
When you append final after the class name, no other class can inherit from it. Attempting to do so results in a compile-time error.

```cpp
#include <iostream>

class Base {
public:
    void display() { std::cout << "Base class\n"; }
};

// Marking 'FinalClass' as final prevents any further inheritance
class FinalClass final : public Base {
public:
    void show() { std::cout << "Final class\n"; }
};

// ❌ COMPILE ERROR: Cannot inherit from 'final' class 'FinalClass'
/*
class Derived : public FinalClass {
};
*/

int main() {
    FinalClass fc;
    fc.show();
    return 0;
}
```

**Stopping overriding:**

```cpp
#include <iostream>

class Base {
public:
    virtual void render() { std::cout << "Rendering Base\n"; }

    // Mark the virtual method as 'final' right in the base class
    virtual void criticalOperation() final {
        std::cout << "Executing fixed base logic that CANNOT be changed.\n";
    }
};

class Intermediate : public Base {
public:
    // Overrides Base::render() and prevents child classes from overriding it further
    void render() override final {
        std::cout << "Rendering Intermediate\n";
    }
};

class Child : public Intermediate {
public:
    // ❌ COMPILE ERROR: Cannot override 'final' function 'Intermediate::render()'
    /*
    void render() override {
        std::cout << "Rendering Child\n";
    }
    */
};
```

##### Pros and Cons of inheritance

**Pros of inheritance:**

- **Enforces Code Reuse (DRY):** If multiple classes share the same logic (like Dog, Cat, and Bird all needing name, age, and sleep()), you write it once in a parent Animal class instead of duplicating it.
- **Logical Hierarchies:** It naturally mirrors real-world taxonomies, making codebases easier for human teams to conceptualize at a glance.
- **Enables Polymorphism:** Inheritance is the gateway to polymorphism. Because a child class inherits from a parent, you can write generic code that handles any "Animal" without needing to know if it's specifically a dog or a cat.

**Limitations / Cons of inheritance:**

1. **Tight Coupling** (The Fragile Base Class Problem)
   Inheritance creates a deep, unbreakable bond between a parent class and its children.
   _ **The Limit:** If you modify, refactor, or delete a method in the parent class, you risk silently breaking dozens of child classes scattered across your entire codebase.
   _ **Why it hurts:** It makes code fragile. You can no longer change a parent class with confidence because the side effects ripple downward.
2. **The Diamond Problem** (Multiple Inheritance Ambiguity)
   Some languages (like C++) allow a class to inherit from multiple parents. This introduces a notorious architectural trap called the Diamond Problem.
   _ **The Limit:** If Class A has two children (Class B and Class C), and a fourth class (Class D) inherits from both B and C, which parent's method does D execute if they both share the same name?
   _ **Why it hurts:** It creates massive ambiguity and forces languages to implement complex rules (like virtual inheritance or method resolution orders) just to prevent code collisions.
3. **Violating the Liskov Substitution Principle (LSP)**
   Inheritance is usually taught using the "is-a" relationship (e.g., a Dog is an Animal). But forcing this rule can lead to bad design.
   _ **The Limit:** Developers often use inheritance just to share code, even when the "is-a" relationship doesn't fit logically.
   _ **Why it hurts:** Classic example: Making a Square inherit from a Rectangle. Mathematically, a square is a rectangle. But in code, a rectangle has independent set_width() and set_height() methods. If you pass a Square where a Rectangle is expected, calling set_width() while leaving height alone will break the square's geometry, causing mysterious bugs.
4. **Code Bloat and Unnecessary Inheritance**
    - **The Limit:** To inherit one useful utility method from a parent class, a child class is forced to inherit everything else the parent carries—including properties and methods it doesn't need or want.
    - **Why it hurts:** Objects end up carrying around a massive amount of "baggage" they never use, bloating memory and cluttering the developer's autocomplete menus.

### 4. Polymorphism

It is the property of some code to behave differently for different contexts. For example, in C++ language, we can define multiple functions having the same name but different working depending on the context.

Polymorphism means "many forms". In C++, it allows objects of different derived classes to be treated through a single uniform base class pointer or reference.

Polymorphism can be classified into two types based on the time when the call to the object or function is resolved. They are as follows:

- Compile Time Polymorphism
- Runtime Polymorphism

#### 1. Compile-Time Polymorphism (Static Binding)

Determined at compile time based on function signatures or types. It is fast because there is zero runtime overhead.

- Function Overloading: Multiple functions with the same name but different parameter types.
- Operator Overloading: Custom behavior for standard C++ operators (+, <<, ==).
- Template programming is also example of this.

> NOTE: When overloading function or method or even operator with different declaration and definiton then only function signature should be same, name of parameter can be different in definition and declaration.

```cpp
// Function Overloading
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }

class NumberContainer {
private:
    std::vector<int> values;

public:
    NumberContainer(std::initializer_list<int> list) : values(list) {}

    // ==========================================
    // 1. SUBSCRIPT OPERATOR ([])
    // Allows accessing elements like an array: container[i]
    // ==========================================
    int& operator[](size_t index) {
        return values[index];
    }
    const int& operator[](size_t index) const {
        return values[index];
    } // const in between promise the compiler that it won't modify constants. If not given then it woudl throw error when read-only object is passed.

    // ==========================================
    // 2. FUNCTION CALL OPERATOR (())
    // Allows the object to be called like a function: container(2)
    // ==========================================
    void operator()(int multiplier) {
        for (auto& val : values) {
            val *= multiplier;
        }
    }

    // ==========================================
    // 3. UNARY OPERATORS (-, ++, --)
    // ==========================================
    // Unary Minus: -container
    NumberContainer operator-() const {
        NumberContainer temp = *this;
        for (auto& val : temp.values) {
            val = -val;
        }
        return temp;
    }

    // Pre-increment: ++container
    NumberContainer& operator++() {
        for (auto& val : values) {
            ++val;
        }
        return *this;
    }

    // Post-increment: container++ (takes a dummy 'int' parameter)
    NumberContainer operator++(int) {
        NumberContainer temp = *this;
        ++(*this); // Call pre-increment
        return temp;
    }

    // ==========================================
    // 4. BINARY ARITHMETIC OPERATORS (+, -, *, etc.)
    // ==========================================
    NumberContainer operator+(const NumberContainer& other) const {
        NumberContainer result = *this;
        for (size_t i = 0; i < values.size() && i < other.values.size(); ++i) {
            result.values[i] += other.values[i];
        }
        return result;
    }

    // ==========================================
    // 5. COMPOUND ASSIGNMENT OPERATORS (+=, -=, etc.)
    // ==========================================
    NumberContainer& operator+=(const NumberContainer& other) {
        for (size_t i = 0; i < values.size() && i < other.values.size(); ++i) {
            values[i] += other.values[i];
        }
        return *this;
    }

    // ==========================================
    // 6. RELATIONAL OPERATORS (==, !=, <, >, etc.)
    // ==========================================
    bool operator==(const NumberContainer& other) const {
        return values == other.values;
    }

    bool operator!=(const NumberContainer& other) const {
        return !(*this == other);
    }

    // ==========================================
    // 7. STREAM INSERTION & EXTRACTION (<<, >>)
    // Must be friend functions because the left operand is std::ostream/std::istream
    // ==========================================
    friend std::ostream& operator<<(std::ostream& os, const NumberContainer& c) {
        os << "[ ";
        for (int val : c.values) {
            os << val << " ";
        }
        os << "]";
        return os;
    }
};


// Templates with class
template <typename T>
class Pair {
private:
    T first;
    T second;

public:
    Pair(T a, T b) : first(a), second(b) {}

    T getMax() const {
        return (first > second) ? first : second;
    }

    void print() const {
        std::cout << "(" << first << ", " << second << ")\n";
    }
};

int main() {
    // Instantiating for int
    Pair<int> intPair(10, 20);
    intPair.print();
    std::cout << "Max: " << intPair.getMax() << "\n\n";

    // Instantiating for std::string
    Pair<std::string> strPair("Apple", "Banana");
    strPair.print();
    std::cout << "Max: " << strPair.getMax() << "\n";

    return 0;
}


// Another example
template <typename T, std::size_t Size>
class StaticArray {
private:
    T data[Size]; // Allocates fixed array of type T and size Size at compile time

public:
    // Method to set values
    void set(std::size_t index, T value) {
        if (index < Size) {
            data[index] = value;
        }
    }

    // Method to get values
    T get(std::size_t index) const {
        if (index < Size) {
            return data[index];
        }
        return T(); // Default-constructed T if out of bounds
    }

    // Return the compile-time capacity
    std::size_t getSize() const {
        return Size;
    }
};

int main() {
    // Creating an object storing 5 integers
    StaticArray<int, 5> intArray;
}

```

#### 2. Run-Time Polymorphism (Dynamic Binding)

Also known as dynamic polymorphism or late binding, runtime polymorphism is the type of polymorphism where the actual implementation of the function is determined during the runtime or execution.

Determined at runtime using virtual functions, pointers, and references. This lets a base pointer trigger different behaviors depending on the concrete object it points to.

- Virtual Functions & Function overriding are examples of this.

#### Virtual keyword in C++

`Virtual` keyword has 4 main uses in C++:

1. **Virtual Method:** Declaring a member function as virtual instructs the C++ compiler to resolve function calls at runtime (late binding) based on the actual object type, rather than at compile time based on the pointer or reference type.

```cpp
#include <iostream>

class Base {
public:
    virtual void show() {
        std::cout << "Base show()" << std::endl;
    }
};

class Derived : public Base {
public:
    void show() override {
        std::cout << "Derived show()" << std::endl;
    }
};

int main() {
    Base* ptr = new Derived();
    ptr->show(); // Outputs "Derived show()" because show() is virtual otherwise it would out put "Base show()"

    delete ptr;
    return 0;
}
```

2. **Pure Virtual Functions (Interfaces & Abstract Classes)**

```cpp
#include <iostream>

// Abstract Class / Interface
class IShape {
public:
    virtual ~IShape() = default;
    virtual void draw() = 0; // Pure virtual function
};

class Circle : public IShape {
public:
    void draw() override {
        std::cout << "Drawing Circle" << std::endl;
    }
};

int main() {
    // IShape s; // ❌ Compile Error: Cannot instantiate abstract class

    IShape* shape = new Circle();
    shape->draw(); // Outputs "Drawing Circle"

    delete shape;
    return 0;
}
```

3. **Virtual Destructors (Safe Polymorphic Cleanup):**When deleting a derived object via a base class pointer, the base class destructor must be `virtual`. Without it, only the base destructor executes, skipping the derived destructor and causing memory/resource leaks.

```cpp
#include <iostream>

class Base {
public:
    virtual ~Base() { // Virtual destructor
        std::cout << "Base Destructor" << std::endl;
    }
};

class Derived : public Base {
private:
    int* data;
public:
    Derived() { data = new int[100]; }
    ~Derived() override {
        delete[] data; // Cleans up heap memory
        std::cout << "Derived Destructor" << std::endl;
    }
};

int main() {
    Base* ptr = new Derived();
    delete ptr;
    // Output order:
    // 1. Derived Destructor
    // 2. Base Destructor
    return 0;
}
```

4. **Virtual Inheritance (Solving the Diamond Problem)**

## Concept of Friendship in C++

Encapsulation dictates that an object’s `private` and `protected` data should remain hidden from the outside world to protect its internal state. However, real-world software architecture sometimes requires tight, trusted partnerships between classes or external utilities.\
Friendship is C++’s controlled, surgical mechanism to break encapsulation selectively.

C++ supports 2 types of friendship:

1. Friend Functions
2. Friend Class

### 1. Friend Functions

A friend function is not a member of the class, yet it has full access to its `private` and `protected` members. There are two types of friend functions:

- **Global/External functions** (that happen to access private data).
- **Specific member functions of another class** (making only one method of another class a friend).

```cpp
// External Function

class Box {
private:
    double width;

public:
    Box(double w) : width(w) {}

    // Declare an external global function as a friend
    friend void printBoxWidth(const Box& b);
};

// Definition of the global function
void printBoxWidth(const Box& b) {
    // Directly accessing the private member 'width'
    std::cout << "Global Function -> Box width: " << b.width << std::endl;
}


/*
Member function of another class
*/

// Forward declaration
class SecretData;

class Inspector {
public:
    // This method will be a friend of SecretData
    void inspect(const SecretData& s);
};

class SecretData {
private:
    int pinCode = 9999;

public:
    // Granting friendship to ONLY the 'inspect' method of the Inspector class
    friend void Inspector::inspect(const SecretData& s);
};

// Definition of Inspector::inspect (must come after SecretData is fully defined)
void Inspector::inspect(const SecretData& s) {
    std::cout << "Inspector Class -> Accessed PIN: " << s.pinCode << std::endl;
}
```

### 2. Friend Class

When a class declares another class as a **friend** class, every single member function of the friend class gains unrestricted access to the private and protected members of the target class.

```cpp
class BankAccount {
private:
    std::string accountNumber = "ACC-12345";
    double balance = 5000.0;

    // Grant friendship to the entire Auditor class
    friend class Auditor;
};

class Auditor {
public:
    void auditAccount(const BankAccount& acc) {
        // Auditor can access ALL private members of BankAccount
        std::cout << "Auditing Account: " << acc.accountNumber << std::endl;
        std::cout << "Verified Balance: $" << acc.balance << std::endl;
    }
};
```

### Friendship & Overloading `<<` or `>>` operator

**Left & Right Operand:** `5 + 3`, 5 is left operand and 3 is right operand.

When we overload any operator then it expects its left operand to be the object of the class. But the problem with `<<` is that it expects `std::cout` as its left operand. That's why we use external friend function to overload operator to achieve this.

```cpp
class myString
{
    char data[12] = "hello";
    // why return ostream --- operator chaining
public:
    std::ostream &operator<<(std::ostream &output)
    {
        output << data << endl;
        return output;
    }
};
int main(int argc, char **argv)
{
    myString obj;
    // cout << obj; // Error as obj is right operand, that's why we make it friend function
    obj << cout << " This is it\n";
    cout << "alternate\n";
    obj.operator<<(cout) << " it also works";
}

// What if we don't return ostream
class myString
{
    char data[12] = "hello";
public:
    void operator<<(std::ostream &output)
    {
        output << data << endl;
    }
};
int main(int argc, char **argv)
{
    myString obj;
    // cout << obj; // Error as obj is right operand, that's why we make it friend function
    obj << cout << " This is it\n"; // this is: void << "This is it\n"; so compilation ERR
    cout << "alternate\n";
    obj.operator<<(cout) << " it also works"; // same as above
}


// Proper overlaoding of << & >>
class myString
{
    char data[12] = "hello";

public:
    friend std::ostream &operator<<(std::ostream &output, myString &var);
    friend std::istream &operator>>(std::istream &put, myString &var);
};

std::ostream &operator<<(std::ostream &output, myString &var)
{
    output << var.data << endl;
    return output;
}
std::istream &operator>>(std::istream &input, myString &var)
{
    input >> var.data;
    return input;
}

int main(int argc, char **argv)
{
    myString obj;
    // cout << obj; // Error as obj is right operand, that's why we make it friend function
    cout << obj << " This is it\n"; // this is: void << "This is it\n"; so compilation ERR
    cin >> obj;
    cout << "\n" << obj << endl;
}

```

**Does it mean we can overload operators like functions?**\
Yes, operators can be overloaded just like functions. The key limitation is that AT LEAST ONE operand must be a user-defined type (`class`, `struct`, or `enum`).

```cpp
struct Point
{
    int x;
    int y;
};

std::ostream &operator<<(std::ostream &output, Point &point)
{
    output << "X: " << point.x << "Y: " << point.y << endl;
    return output;
}
std::istream &operator>>(std::istream &input, Point &point)
{
    input >> point.x >> point.y;
    return input;
}

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
    cout << "Enter X and Y coordinates (e.g. 10 20): ";
    cin >> p; // Uses operator>>

    cout << "Initial Point: " << p << endl; // Uses operator<<

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

**If we use friend function to use cout as left operand then why ++Obj works, here Obj is right operand?**

```cpp
++obj;  // Translated by compiler to:
obj.operator++();


obj++;  // Translated by compiler to:
obj.operator++(int(0)); // The compiler automatically passes a 0 behind the scenes

```

### Rules for friendship

1. **Friendship is NOT Symmetric:**
   If class A declares class B as a friend, B can access A's private data. However, A cannot access B's private data unless B explicitly declares A as a friend. (A friend of your friend is not automatically your friend).
2. **Friendship is NOT Transitive:**
   If class A is a friend of B, and class B is a friend of C, class A is not automatically a friend of C.
3. **Friendship is NOT Inherited:**
   If a base class Base grants friendship to a function or class, derived classes (Derived : public Base) do not pass that friendship down to their children. The friend only has access to the Base portion, not the derived extensions.

### When to use friendship?

- **Use it for:** Operator overloading (operator<<, operator>>), tightly coupled data structures (like a Node and a LinkedList, or an Iterator and a Container), or performance-critical mathematical wrappers.
- **Avoid it for:** General code organization. If you find yourself scattering friend declarations across unrelated classes, it usually indicates a flaw in your object-oriented design and encapsulation strategy.

## How objects related to one another in OOP?

Three concepts describe how objects relate to one another in object-oriented design. They exist on a spectrum of coupling strength (how tightly bound the objects are to each other's lifecycle).

- **Association**: A general relationship where two objects are connected but can exist independently.

```cpp
class Patient {
public:
    std::string name;
    Patient(std::string n) : name(n) {}
};

class Doctor {
public:
    std::string name;
    Doctor(std::string n) : name(n) {}

    // Association: Doctor uses Patient, but doesn't store/own Patient
    void prescribe(const Patient& patient) {
        std::cout << "Dr. " << name << " prescribes medicine to " << patient.name << "\n";
    }
};

int main() {
    Doctor doc("Smith");
    Patient pat("Alice");

    doc.prescribe(pat); // Association in action

    // Both objects exist and die independently
    return 0;
}
```

- **Aggregation**: A weak "has-a" relationship where the child object can exist independently of the parent.

```cpp
#include <iostream>
#include <string>

class Teacher {
public:
    std::string name;
    Teacher(std::string n) : name(n) {}
};

class Department {
private:
    // Aggregation: Stores a pointer/reference to an EXTERNALLY created Teacher
    const Teacher* teacher;

public:
    Department(const Teacher* t) : teacher(t) {}

    void printTeacher() const {
        if (teacher) {
            std::cout << "Department has teacher: " << teacher->name << "\n";
        }
    }
};

int main() {
    // Teacher is created outside Department
    Teacher* t1 = new Teacher("Prof. Alan");

    {
        Department csDept(t1);
        csDept.printTeacher();
    } // csDept goes out of scope and is DESTROYED here...

    // ...but t1 is STILL alive!
    std::cout << "Teacher still exists: " << t1->name << "\n";

    delete t1; // Manual cleanup since Department didn't own it
    return 0;
}
```

- **Composition**: A strong "has-a" relationship where the child object's lifetime depends on the parent object. Composition is the strongest relationship. The child object is an integral part of the parent. The parent object owns the child and manages its creation and destruction. If the parent dies, the child dies with it.
  In modern C++, composition is typically achieved via direct member variables or `std::unique_ptr`.

```cpp
#include <iostream>
#include <memory>

class Engine {
public:
    Engine() { std::cout << "Engine created.\n"; }
    ~Engine() { std::cout << "Engine destroyed.\n"; }
    void start() { std::cout << "Vroom vroom!\n"; }
};

class Car {
private:
    // Composition option 1: Direct object member (automatically destroyed with Car)
    // Engine engine;

    // Composition option 2: Unique ownership pointer (smart pointer manages lifecycle)
    std::unique_ptr<Engine> engine;

public:
    Car() : engine(std::make_unique<Engine>()) {
        std::cout << "Car created.\n";
    }

    ~Car() {
        std::cout << "Car destroyed.\n";
    } // engine is automatically destroyed here

    void drive() {
        engine->start();
    }
};

int main() {
    {
        Car myCar;
        myCar.drive();
    } // Entire Car and its internal Engine are destroyed here automatically!

    return 0;
}
```

### How to decide which one to use?

**Can the child exist without the parent?**

- **No** - Use Composition (Direct member or std::unique_ptr).
- **Yes**
    - **Ask**: Does the parent hold a reference to it long-term?
        - **Yes** - Use Aggregation (Raw pointer T\*, std::shared_ptr, or reference T&).
        - **No** - Use Association (Pass as a function argument).
