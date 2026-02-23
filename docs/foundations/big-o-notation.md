---
title: "Big-O Notation: Time Complexity Basics"
category: "Algorithms and Complexity"
tags: ["complexity", "big-o", "algorithms", "analysis"]
difficulty: "Beginner"
last_updated: 2026-02-23
author: "ihelloeveryone"
---

# Big-O Notation: Time Complexity Basics

## Core concept
Big-O notation is a mathematical way to describe how the running time or space usage of an algorithm grows as the input size increases, focusing on long-term growth rather than exact step counts.
It provides an implementation- and hardware-independent upper bound on how fast resource usage can grow as the input size becomes large.

## The problem Big-O solves
Without a shared language like Big-O, it is difficult to compare algorithms across machines, programming languages, or implementations.
Raw timings (for example, "this runs in 10 ms") change with hardware, compiler optimizations, and constant factors, but the growth pattern with respect to input size usually does not.
Big-O gives a way to reason about scalability: how an algorithm behaves when input size grows from hundreds to millions.

## How Big-O works
Big-O describes the dominant term of a function that counts operations (or time/space) as a function of input size, usually written as \(n\).
Formally, an algorithm with running time \(T(n)\) is in \(O(f(n))\) if there are positive constants \(c\) and \(n_0\) such that for all \(n \ge n_0\), \(T(n) \le c \cdot f(n)\).
In practice, this means:
- Model the number of basic operations as a function of \(n\).
- Drop constant factors (for example, \(3n\) becomes \(n\)).
- Keep only the highest-order term (for example, \(2n^2 + 5n + 7\) becomes \(n^2\)).

### Logical steps for analyzing complexity
1. Identify the input and define what \(n\) represents (length of array, number of nodes, number of vertices, and so on).
2. Trace the algorithm and count how many times key operations execute in terms of \(n\).
3. Express this count as a function \(T(n)\), combining contributions from loops, branches, and function calls.
4. Simplify \(T(n)\) by removing constants and lower-order terms, then express the result using Big-O notation.

## Common complexity classes

| Notation | Name            | Typical example                                    |
|---------|-----------------|----------------------------------------------------|
| O(1)    | Constant time   | Accessing an element by index in an array         |
| O(log n)| Logarithmic time| Binary search on a sorted array                    |
| O(n)    | Linear time     | Scanning an array once (for example, linear search)|
| O(n log n)| Quasi-linear  | Efficient sorts like mergesort, heapsort           |
| O(n^2)  | Quadratic time  | Two nested loops over the same array               |
| O(2^n)  | Exponential time| Brute-force subset enumeration                     |

These classes describe growth rates: for large \(n\), an O(n log n) algorithm will eventually outperform an O(n^2) algorithm, even if the quadratic algorithm is faster for very small inputs.

## Visual intuition (growth curves)
A typical way to build intuition is to plot several functions on the same graph, such as \(n\), \(n \log n\), and \(n^2\), and see how they diverge as \(n\) increases.
In the MonCSDocs media repository, this topic can be illustrated with a diagram that shows multiple complexity curves on the same axes.

Example placeholder (to be provided by moncsdocs-media):

![Growth curves for common complexity classes](https://media.moncsdocs.moebiusorder.com/data/foundations/complexity/big-o-growth-curves.svg)

> Figure: Relative growth of O(1), O(log n), O(n), O(n log n), and O(n^2) as input size increases.

## Mathematical examples
Consider an algorithm whose operation count can be written as:

\[ T(n) = 3n^2 + 5n + 20. \]

For sufficiently large \(n\), the \(3n^2\) term dominates the \(5n\) and constant 20.
Therefore, the algorithm has time complexity \(O(n^2)\).

As another example, suppose \(T(n) = 7n + 100\).
For large \(n\), the constant 100 becomes negligible relative to \(7n\), so the running time is \(O(n)\).

## Worked example: simple loop

Consider the following pseudocode that sums an array of \(n\) elements:

```text
sum = 0
for i from 0 to n - 1:
    sum = sum + a[i]
return sum
```

- The body of the loop runs once for each element, so the number of additions is proportional to \(n\).
- Ignoring constant-time statements before and after the loop, the total time is proportional to \(n\).

This algorithm runs in linear time, so its time complexity is \(O(n)\).

## Worked example: nested loops

Consider a simple double loop that compares all pairs of elements in an array:

```text
for i from 0 to n - 1:
    for j from 0 to n - 1:
        compare(a[i], a[j])
```

- The inner loop runs \(n\) times for each of the \(n\) iterations of the outer loop.
- The comparison executes \(n \times n = n^2\) times.

This algorithm runs in quadratic time, so its time complexity is \(O(n^2)\).

## How to read Big-O in practice
When you see a complexity like O(n log n), interpret it as "if the input size doubles, the running time grows a bit more than linearly, but far less than quadratically."
Big-O focuses on worst-case or upper-bound behavior unless otherwise specified, which is helpful when designing systems that must remain responsive even in heavy-load scenarios.

## Common misconceptions and pitfalls
- Big-O is not about exact speed; a well-optimized O(n^2) algorithm can be faster than a poorly implemented O(n log n) algorithm on small inputs.
- Big-O usually ignores constant factors and lower-order terms, but in engineering practice those constants can matter for realistic input sizes.
- Big-O by itself does not distinguish between best, average, and worst case; those need to be specified separately if they differ.

## Real-world applications
Big-O notation is used to compare data structures and algorithms when designing libraries, backend services, operating systems, and more.
It informs trade-offs: for example, choosing between a hash table (average-case O(1) lookup) and a balanced tree (O(log n) lookup) depending on performance guarantees and memory constraints.

## Practice exercises
- Analyze the complexity of an algorithm that has one loop from 0 to n, and inside that loop calls a function that runs in O(log n) time.
- Given pseudocode with three nested loops, each running from 0 to n - 1, determine the Big-O time complexity.
- For a divide-and-conquer algorithm that splits the input into two halves and recursively processes both halves with a linear-time combine step, derive the Big-O complexity.

## Related topics
- Asymptotic notations beyond Big-O: Omega (lower bound) and Theta (tight bound).
- Amortized analysis for operations whose cost varies between calls.
- Space complexity, which measures how memory usage grows with \(n\).

---
[Back to Foundational Theory index](./README.md)
