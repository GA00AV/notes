# Introduction

**Data Structures and Algorithms** consists of two main concepts:

1. **Data Structure**
2. **Algorithm**

## Data Structures

**Data Structures** are formats for organising, processing and storing data.

In computer science, data structures are formally classified based on how data is organized in memory, the relationships between data elements, and how they can be manipulated.

They are:

1. Primitive Data Structures
2. Non-Primitive Data Structures

### 1. Primitive Data Structures

**Primitive data structures** are the foundational, basic data types supported directly by a programming language or machine architecture. They can hold a single value.

**Characteristics**: They are building blocks, language-dependent, and typically occupy a fixed amount of memory.

**Examples**:

1. **Integer**: Whole numbers (e.g., 42).
1. **Floating-Point / Double**: Numbers with decimal points (e.g., 3.14159).
1. **Character**: Single letters or symbols (e.g., 'A').
1. **Boolean**: True or false values.
1. **Pointer / Reference**: Variables that store memory addresses of other variables.

### 2. Non-Primitive Data Structures

Non-primitive data structures are more sophisticated, user-defined or derived structures built using primitive data structures. They can store multiple values and collections of data.

These are broadly divided into 3 categories:

1. Linear Data structures
2. Non-linear Data structures
3. Hash-Based Data structures

#### Linear Data Structures

In a linear data structure, data elements are arranged sequentially or linearly. Each element is connected to its previous and next element, meaning the data can be traversed in a single run.

- **Array**: A fixed-size, homogeneous collection of elements stored in contiguous memory locations. Elements are accessed directly via an index.
- **Vector**: A dynamically-sized, homogeneous collection of elements stored in contiguous memory locations. Elements are accessed directly via an index.
- **Linked List**: A dynamic collection of nodes where each node contains data and a reference (pointer) to the next node.
    - **Variants**:
        - Singly Linked List
        - Doubly Linked List
        - Circular Linked List.

- **Stack**: A LIFO (Last In, First Out) structure where elements are added and removed from only one end (the top).
- **Queue**: A FIFO (First In, First Out) structure where elements are inserted at the back (rear) and removed from the front.
    - **Variants**:
        - Linear Queue,
        - Circular Queue,
        - Deque (Double-Ended Queue),
        - Priority Queue.

#### Non-Linear Data Structures

In a non-linear data structure, elements are not arranged in a sequential order. Instead, elements form a hierarchical or interconnected network where a single data element can connect to multiple other elements.

- **Tree**: A hierarchical structure consisting of a root node with branching child nodes. There are no cycles.
    - **Variants**: Binary Tree, Binary Search Tree (BST), AVL Tree, Red-Black Tree, B-Tree, Trie (Prefix Tree).
- **Graph**: A network of nodes (Vertices) connected by links (Edges). Graphs can model complex relationships, maps, and networks.
    - **Variants**: Directed vs. Undirected, Weighted vs. Unweighted, Cyclic vs. Acyclic.

#### Hash-Based Data Structures

Hash-based structures leverage mathematical algorithms (hash functions) to organize and locate data instantly, bypassing sequential searches.

- **Hash Table / Hash Map**: Stores data in key-value pairs. A hash function computes an index (bucket) where the value is stored, enabling average O(1) lookups.
- **Hash Set**: Similar to a hash table, but it stores unique keys only (no associated values), used for fast membership testing.

## Algorithm

An **algorithm** is a step-by-step set of instructions or rules designed to solve a specific problem or perform a particular task.

For example if you have to add two numbers, the algorithm is like:

1. Take two numbers in input
2. Add them
3. Print to the screen

## Why Learn Data Structure and Algorithm

1. **It helps in cracking tech interviews**: Top tech companies and software jobs rely heavily on DSA questions to test your problem-solving skills during interviews.
2. **It teaches you problem solving skills**. It helps us to solve complex problem efficiently by using right data structure and most optimal algorithm

# Basics

## 1. Basics of Algorithm

1. [Reverse a Number](https://leetcode.com/problems/reverse-integer)
1. [Check Palindrome](https://leetcode.com/problems/palindrome-number)
1. [Armstrong Numbers](https://www.geeksforgeeks.org/problems/armstrong-numbers2727/1)

## 2. Basics of recursion

1. [Power of Four](https://leetcode.com/problems/power-of-four/description/?envType=problem-list-v2&envId=recursion)
1. [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/description/?envType=problem-list-v2&envId=recursion)

## 3. Analysing Performance of an Algorithm

Okay so now that we know about algorithm suppose there is a problem: `check palindrome` and we know that we can have multiple algorithm to solve a problem. And i come up with two solutions: `Algorithm 1`, and `Algorithm 2`.

```cpp

// Algorithm 1
bool isPalindrome(int x) {
        std::string o = std::to_string(x);
        std::string str = std::to_string(x);
        std::reverse(str.begin(), str.end());
        return str == o;
    }

// Algorithm 2
bool isPalindrome(int x) {
        if(x < 0 || (x % 10 == 0 && x != 0)) return false;
        int rev = 0;
        while(x > rev) {
            rev = rev * 10 + x % 10;
            x /= 10;
        }
        return x == rev || x == rev / 10;
}
```

So out of these two algorithms which algorithm should we choose?

**Answer** is obvious chose the one which perform better.

**So what are the ways to analyse which algorithm is better and when do we say that one algorithm is better than other?** Well, when analysing algorithm we mostly care about just two things:

1. How much time an algorithm takes to run
2. How much memory(space) it takes

A very simple way to do this is by any command-line tools like `time` command in linux or for a platform independent way, we can write a very simple python script that would do that for us.

```python
import subprocess
import time
import psutil

# Command to run your compiled C++ program
command = ["./my_program"]

# Start the process and the timer
start_time = time.time()
process = subprocess.Popen(command)

peak_memory = 0

# Poll the process while it's running to capture peak memory (RSS)
while process.poll() is None:
    try:
        p = psutil.Process(process.pid)
        mem_info = p.memory_info().rss  # Resident Set Size in bytes
        if mem_info > peak_memory:
            peak_memory = mem_info
    except (psutil.NoSuchProcess, psutil.AccessDenied):
        break
    time.sleep(0.001)  # Poll every 1ms

end_time = time.time()
elapsed_time = end_time - start_time

print(f"Execution Time: {elapsed_time:.4f} seconds")
print(f"Peak Memory (RSS): {peak_memory / (1024 * 1024):.2f} MB")
```

Using this script, we can figure out how much time an algorithm takes to run and how much memory it takes. But there is a big flaw. Suppose you are working in team and you come up with an algorithm that takes 1ms to run and then your co-worker comes up with an algorithm that takes 2ms then does that mean your algorithm is better. Answer isn't always yes. It's because how much time an algorithm takes to run doesn't just depend on how efficient an algorithm is but also on many other factors.

It is fundamentally flawed for comparing algorithms universally due to four key reasons:

1. **Hardware Bias**: The same code runs significantly faster on a high-end machine with a modern processor than on an older laptop or mobile device.
1. **Environment & Background Noise**: Operating system scheduling, background processes, compiler/interpreter optimizations, and memory management (like garbage collection) introduce unpredictable variations in time.
1. **Language Dependency**: Code written in C or C++ will almost always execute faster than the exact same algorithm written in Python or JavaScript.
1. **Input Limitations**: Testing requires running the code with specific datasets. An algorithm might perform exceptionally well on small inputs (e.g., $N=100$) but completely collapse on massive datasets (e.g., $N=10,000,000$), which might crash your system during a test run.

So now we know that just measuring time and memory taken by an algorithm isn't a good way of measuring its performance and we need a better way that shouldn't get affected by all those extra noise. And that's why we use **Complexity Analysis**.

Complexity analysis .

So, **Complexity analysis** is a technique used to evaluate an algorithm's efficiency independently of any machine or environment.

There are mainly two types of complexity analysis:

1. **Time Complexity Analysis**: Measures how the amount of operations/running time increases as the input size (n) grows. We count the number of basic operations (like comparisons or assignments), not actual seconds.
2. **Space Complexity Analysis**: Measures how much extra memory (auxiliary space) the algorithm requires in RAM relative to the input size n.

Okay now we know we use complexity analysis instead of measuring time and memory but **how do we actually do it mathematically?** So for this, we'll introduce a new concept called "Asymptotic Analysis".

To understand **Asymptotic Analysis**, consider this equation:
$$ y = x^{3} + x + 2 $$

if we consider the values of $y$, at \
$x=0, y=2$,\
$x=2, y=12$,\
$x=10, y=1012$,\
$x=100, y=1000102$\
$x=10000, y=10000000010002$\
as you can see as as value of input ($x$) increases the the $x^3$ part of the function becomes dominating. So as $x \to \infty$, we can assume that $y \approx x^{3}$. This is the core idea of **Asymptotic Analysis**.

**Asymptotic analysis** is the mathematical way of evaluating an algorithm's performance as the input size (n) approaches infinity ($n \to \infty$).

We do **complexity analysis** of an algorithm by using **Asymptotic anlysis**. So, **complexity analysis** is more like a technique or idea and **asymptotic analysis** is the mathematics used to do it.
