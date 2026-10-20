# Maths for DSA

## 1. GCD or HCF

1. Basic approach -- find the largest common divisor that divides both the number
2. Euclidean algorithm: It is based on a fundamental principle: The greatest common divisor of two numbers also divides their difference. Same old shcool math way of finding GCD -- O(min(a,b))

| Problems                                                                                        | Handwritten solution | Video Solution |
| ----------------------------------------------------------------------------------------------- | -------------------- | -------------- |
| [GCD of Two](https://www.geeksforgeeks.org/problems/gcd-of-two-numbers3459/1)                   | link                 | link           |
| [GCD of Odd and Even Sums](https://leetcode.com/problems/gcd-of-odd-and-even-sums/description/) | link                 | link           |

## 2. divisors

1. Naive -- O(n) -- start from 1 till number and find divisors
2. O(sqrt(n)) -- divisors forms pair and split around sqrt(N)

[All Divisors of Number](https://www.geeksforgeeks.org/problems/all-divisors-of-a-number/1)
[Number of common factors](https://leetcode.com/problems/number-of-common-factors/description/)

[Perfect number](https://leetcode.com/problems/perfect-number/description/)

[Three Divisors](https://leetcode.com/problems/three-divisors/description/)

[Count the digits that divide the number](https://leetcode.com/problems/count-the-digits-that-divide-a-number/description/)

[Closest Divisors](https://leetcode.com/problems/closest-divisors/description/)

## 3. Prime number

**Checking prime number**: check prime by check if it's divisible by any number between 2 and sqrt(N)

Finding prime number till N

1. start from two to N and check if it's prime and keep adding -- O(Nsqrt(N))
2. Using sieve of eratosthenes -- create a bool array till n and mark each as prime then start from 2 and mark each multiple of 2 as non-prime till n, starting from i=2\*2, incrementing i+=i

[Sieve of Eratosthenes](https://www.geeksforgeeks.org/problems/sieve-of-eratosthenes5242/1)

[Count Primes](https://leetcode.com/problems/count-primes/description/)

[Prime pairs with target sum](https://leetcode.com/problems/prime-pairs-with-target-sum/description/)

[Closest prime numbers in range](https://leetcode.com/problems/closest-prime-numbers-in-range/description/)

## 4. Square root

1. Naive -- O(sqrt(n)) time -- start from one and keep checking if its square is closer

2. using binary search -- O(log(N)) time & O(1) space

3. Builtin function std::sqrt -- O(1) time & space O(1)

4. using formula -- $\sqrt{n} = e^{\frac{1}{2}x\log{n}}$ -- O(1)

[Sqrt(x)](https://leetcode.com/problems/sqrtx/description/)

## 5. Power of a number

- NOTE: $e^k$ isn't calculated and it's O(1) as compiler uses CPU to find it out

1. Naive approaches -- iterative -- O(N)
2. recursion -- O(N) for both
3. spliting even as power(b, e/2)* power(b, e/2) or odd as b*power(b, e/2)\* power(b, e/2) -- O(logN) for both
4. builtin pow function -- log(N) & O(1)

[Pow(x, n)](https://leetcode.com/problems/powx-n/description/)

[Check if a number is sum of powers of three](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three/description/)

[]()

## 6. Fibonacci numbers

1. Naive -- recursion -- O($2^N$) & space(N)
2. recursion but memoised -- O(N) for both space and time
3. Iterative approach -- O(N) & O(1)
4. Matrix exponentiation -- O(log(n)) time and O(log(n)) space

$$
\left(
\begin{array}{cc}
1 & 1 \\
1 & 0
\end{array}
\right)^{n-1} =

\left(
\begin{array}{cc}
F(n) & F(n-1) \\
F(n-1) & F(n-2)
\end{array}
\right)
$$

[Fibonacci number](https://leetcode.com/problems/fibonacci-number/description/)

[Three fibonacci sum](https://leetcode.com/problems/three-fibonacci-sum/description/)

## 7. Factorial of a number

1. iterative -- O(N) & O(1) space
2. Recursive -- O(N) & O(N) space

[Factorial of a number](https://www.geeksforgeeks.org/problems/factorial5739/1)

[Clumsy factorial](https://leetcode.com/problems/clumsy-factorial/description/)

[Factorial Trailing zeroes](https://leetcode.com/problems/factorial-trailing-zeroes/description/)

## 8. Modular Arithmetic

Modular arithmetic is a system of arithmetic for numbers where numbers "wrap around" after reaching a certain value, called the modulus.
Like in a 12-hour clock after 12 it should be 13 but it shows 1, this is the exactly what modular arithmetic does. And that's why it is often referred to as "clock arithmetic."

So in simple terms, in modular arithmetic we are going to see how modular operator works in case of:

1. addition: (a+b)%c
2. Multiplication
3. Division
4. Exponentiation

But before that let's discuss the differnce between modulus and remainder.

what is modulus & difference from Quotient Remainder Theorem

Quotient Remainder Theorem states that for any pair of integers a and b (b is positive), there exist two unique integers q and r such that: a = b x q + r , where 0 <= r < b

Let's now proceed with modular arithmetic.

**Modular Addition**:
(a+b)%c = ((a%c)+(b%c))%c

example -- 17 + 19 % 7

**Modular multiplication**:
(a\*b)%c = ((a%c)\*(b%c))%c

- same example

**Modular division**:
The Modular Division is totally different from modular addition, subtraction and multiplication. It also does not exist always.

(a / b) mod m is not equal to ((a mod m) / (b mod m)) mod m.
This is calculated using the following formula:

(a / b) mod m = (a x (inverse of b)) mod m

and inverse of b doesn't always exists.

Inverse

The modular inverse of a mod m exists only if a and m are relatively prime i.e. gcd(a, m) = 1. Hence, for finding the inverse of a under modulo m, if (a x b) mod m = 1 then b is the Modular Inverse of a.
The modular inverse x must be in the range [1, ... , m−1] (it cannot be 0 since n × 0 mod m is never 1).

Example:

a = 5, m = 7 (5 x 3) % 7 = 1 hence, 3 is modulo inverse of 5 under 7.

Input: n = 3, m = 11
Output: 4
Explanation: (3 × 4) mod 11 = 1, so 4 is the modular inverse.
Note: 15 also works since (3 × 15) mod 11 = 1, but it is not in the range 1 to 10, so it is invalid.

**Modular Exponentiation**:
here we often have to calculate x^n first then we can calculate modulus.

[Modular inverse](https://www.geeksforgeeks.org/problems/modular-multiplicative-inverse-1587115620/1)
[Super Pow](https://leetcode.com/problems/super-pow/)

# Bit Manipulation

[Bitwise Operators for Maths](https://utkarsh1504.github.io/DSA-Java/bitwise-operator)

# Arrays

## 1. Theory

1. How arrays works under the hood?
2. Time and space complexities of Array operations
3. Array implementation in C++
4. Pre-implemented array & its opeartions in C++ (STL)

## 2. Practice Problems

In DSA Sheet + Video solutions on Own Platform

# Matrix

# Strings

# Sorting & Searching

# Linked List

# Stack & Queues

# Tree & Binary Tree

# Binary Search Tree

# Greedy

# Backtracking

# Dyanmic programming

# Hashing

# Heap

# Graph

# Segment Tree

# Trie

# Fenwick Tree (used in prefix sum)
