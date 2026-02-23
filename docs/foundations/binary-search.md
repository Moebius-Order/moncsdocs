---
title: "Binary Search"
category: "Algorithms"
pillar: "Foundational Theory"
tags: ["algorithms", "searching", "divide-and-conquer", "arrays"]
difficulty: "Beginner"
prerequisites: ["arrays", "algorithm-analysis", "recursion"]
estimated_time: "15 minutes"
last_updated: "2026-02-23"
author: "Moebius Order"
contributors: []
reviewers: []
version: "1.0"
status: "Published"
---

# Binary Search

## The Core Concept
> Binary search is a divide-and-conquer algorithm that finds the position of a target value within a **sorted array** by repeatedly dividing the search interval in half.

## The "Why" (The Problem)

Searching for an element in a collection is one of the most fundamental operations in computing. Without efficient search algorithms:

- **Linear search is inefficient**: Checking every element sequentially in a large dataset takes too long
- **Real-world applications suffer**: Think of searching through millions of records in a database, dictionary lookups, or finding a name in a phone book
- **Scalability becomes impossible**: As data grows, linear search time grows proportionally

Binary search solves this by exploiting a key property: **if the data is sorted, we can eliminate half of the remaining elements with each comparison**.

**Inefficiency addressed**: Reduces search time from linear \(O(n)\) to logarithmic \(O(\log n)\), making searches in large datasets practically instantaneous.

---

## Historical Context

### Origin
- **When**: First published in 1946
- **Who**: John Mauchly in "Theory and Techniques for Design of Electronic Digital Computers"
- **Why**: Needed efficient algorithms for searching sorted punch card systems

### Driving Need
Early computers had limited memory and processing power. Efficient search algorithms were critical for making practical use of sorted data stored on magnetic tapes and punch cards.

### Key Milestone
Though conceptually simple, the first correct implementation of binary search wasn't published until 1962 (by Donald Knuth), highlighting the subtlety of boundary conditions in the algorithm.

---

## Motivating Example

### The Scenario: Dictionary Lookup

Imagine searching for the word "computer" in a physical dictionary with 1,000 pages.

**Without Binary Search (Linear)**: 
- Start at page 1, check each page sequentially
- Worst case: Check all 1,000 pages
- Average case: Check 500 pages

**With Binary Search**:
1. Open to middle page (500)
2. "Computer" comes before the words on page 500 alphabetically
3. Eliminate pages 500-1000, now search pages 1-499
4. Open to middle of remaining pages (250)
5. "Computer" comes after page 250
6. Eliminate pages 1-250, search pages 251-499
7. Continue halving until found

**Result**: Found in ~10 comparisons instead of potentially 1,000!

---

## How it Works (The Logic)

Binary search maintains three pointers: **left**, **right**, and **middle**, defining the current search range.

### Logical Steps:

#### 1. Initial State:
- **Precondition**: Array must be sorted in ascending order
- **Setup**: 
  - `left = 0` (start of array)
  - `right = n - 1` (end of array)
  - `target` = value we're searching for

#### 2. The Transformation:

**Operation A**: Calculate middle index
- `middle = left + (right - left) / 2`
- Why this formula? Prevents integer overflow

**Operation B**: Compare target with middle element
- If `array[middle] == target`: Found! Return middle
- If `target < array[middle]`: Target must be in left half
  - Update: `right = middle - 1`
- If `target > array[middle]`: Target must be in right half
  - Update: `left = middle + 1`

**Operation C**: Repeat until found or search space exhausted
- Continue while `left ≤ right`
- If `left > right`: Target not in array

#### 3. The Result:
- **Success**: Returns index of target element
- **Failure**: Returns -1 (or sentinel value) indicating element not found
- **Property**: Search space halves with each iteration

---

## Visual Representation

### Search Process Visualization

```
Searching for target = 23 in sorted array:

Iteration 1:
Array: [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
Index:  0  1  2   3   4   5   6   7   8   9  10
        ↑                   ↑                   ↑
       left              middle              right
       
middle = (0 + 10) / 2 = 5
array[5] = 23 == target ✓ FOUND!
Return index 5
```

### Decision Tree

```
                    [Compare middle]
                          │
          ┌───────────┼───────────┐
          │              │              │
       target <       target ==       target >
        middle         middle         middle
          │              │              │
   [Search left]    [FOUND!]    [Search right]
       half                          half
```

---

## Mathematical & Logical Formalization

### Formal Definition

**Given**: 
- Sorted array \( A[0..n-1] \)
- Target value \( x \)

**Find**: Index \( i \) such that \( A[i] = x \), or -1 if no such \( i \) exists

### Key Equations

**Middle Index Calculation**:
\[ \text{middle} = \left\lfloor \frac{\text{left} + \text{right}}{2} \right\rfloor \]

Or more safely (prevents overflow):
\[ \text{middle} = \text{left} + \left\lfloor \frac{\text{right} - \text{left}}{2} \right\rfloor \]

### Complexity Analysis

**Time Complexity**: 
\[ T(n) = T(n/2) + O(1) = O(\log n) \]

Proof: Each iteration halves the search space, leading to logarithmic depth.

**Space Complexity**: 
- Iterative: \( O(1) \) - constant extra space
- Recursive: \( O(\log n) \) - call stack depth

### Theoretical Properties

**Invariant**: At each step, if the target exists in the array, it must be within the range `[left, right]`

**Termination**: The algorithm terminates because:
1. The search space size decreases by at least half each iteration
2. When `left > right`, the search space is empty

---

## Worked Example

### Complete Walkthrough

**Problem**: Find `target = 31` in array `[3, 7, 12, 18, 24, 31, 42, 55, 63]`

**Initial State**:
- `array = [3, 7, 12, 18, 24, 31, 42, 55, 63]`
- `left = 0, right = 8, target = 31`

**Iteration 1**:
- `middle = 0 + (8 - 0) / 2 = 4`
- `array[4] = 24`
- `24 < 31` → search right half
- Update: `left = 5, right = 8`

**Iteration 2**:
- `middle = 5 + (8 - 5) / 2 = 6`
- `array[6] = 42`
- `42 > 31` → search left half
- Update: `left = 5, right = 5`

**Iteration 3**:
- `middle = 5 + (5 - 5) / 2 = 5`
- `array[5] = 31`
- `31 == 31` → **FOUND!**
- **Return**: index 5

**Total Comparisons**: 3 (vs. 6 for linear search)

---

## Practical Examples

### 1. Simple Implementation (Iterative)

```python
def binary_search(array, target):
    """
    Iterative binary search implementation.
    
    Args:
        array: Sorted list of comparable elements
        target: Element to search for
    
    Returns:
        Index of target if found, -1 otherwise
    """
    left, right = 0, len(array) - 1
    
    while left <= right:
        middle = left + (right - left) // 2
        
        if array[middle] == target:
            return middle
        elif array[middle] < target:
            left = middle + 1
        else:
            right = middle - 1
    
    return -1  # Target not found

# Usage
data = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
result = binary_search(data, 23)
print(f"Found at index: {result}")  # Output: Found at index: 5
```

### 2. Recursive Implementation

```python
def binary_search_recursive(array, target, left=0, right=None):
    """
    Recursive binary search implementation.
    """
    if right is None:
        right = len(array) - 1
    
    # Base case: search space exhausted
    if left > right:
        return -1
    
    middle = left + (right - left) // 2
    
    if array[middle] == target:
        return middle
    elif array[middle] < target:
        return binary_search_recursive(array, target, middle + 1, right)
    else:
        return binary_search_recursive(array, target, left, middle - 1)
```

### 3. Advanced: Finding Insertion Point

```python
def binary_search_insertion(array, target):
    """
    Returns the index where target should be inserted to maintain sorted order.
    If target exists, returns its index.
    """
    left, right = 0, len(array)
    
    while left < right:
        middle = left + (right - left) // 2
        
        if array[middle] < target:
            left = middle + 1
        else:
            right = middle
    
    return left

# Usage for finding boundaries
data = [1, 2, 2, 2, 5, 7, 9]
pos = binary_search_insertion(data, 2)
print(f"First occurrence at index: {pos}")  # Output: 1
```

---

## Variations & Extensions

### 1. Lower Bound / Upper Bound
- **Lower Bound**: First position where element ≥ target
- **Upper Bound**: First position where element > target
- **Use Case**: Finding range of duplicate elements

### 2. Binary Search on Answer Space
- **Concept**: Use binary search to find optimal value in continuous range
- **Example**: Finding square root, minimizing/maximizing a function
- **When to Use**: When checking if a value works is cheaper than computing optimal value directly

### 3. Rotated Array Search
- **Problem**: Array is sorted but rotated at unknown pivot
- **Solution**: Modified binary search that handles rotation
- **Use Case**: Circular buffers, rotated datasets

### Comparison Table

| Variant | Time Complexity | Use Case |
|:--------|:----------------|:---------|
| Standard | \(O(\log n)\) | Find exact match |
| Lower Bound | \(O(\log n)\) | Find first occurrence |
| Upper Bound | \(O(\log n)\) | Find last occurrence |
| Rotated Array | \(O(\log n)\) | Search in rotated sorted array |
| Answer Space | \(O(\log n \cdot f(n))\) | Optimize over range |

---

## Common Misconceptions

### Misconception 1: "Binary search works on unsorted arrays"

**Wrong**: Binary search on unsorted data gives incorrect results.

**Correct**: The array **must be sorted** for binary search to work. The algorithm relies on the ordering property to eliminate half the search space.

**Why it matters**: Using binary search on unsorted data leads to silent failures—no error, just wrong results.

### Misconception 2: "middle = (left + right) / 2 is fine"

**Problematic**: Can cause integer overflow when `left + right` exceeds maximum integer value.

**Better**: `middle = left + (right - left) / 2`

**Why it matters**: In languages like C/C++/Java with fixed integer sizes, overflow leads to bugs that only appear with large arrays.

### Misconception 3: "Binary search is always faster"

**Not always**: For very small arrays (n < 10), linear search can be faster due to lower overhead.

**Correct understanding**: Binary search shines with large datasets. Overhead of calculating middle index and maintaining pointers can outweigh benefits for tiny arrays.

---

## Advantages & Limitations

### Advantages

1. **Efficient for large datasets**: \(O(\log n)\) means searching 1 million elements takes ~20 comparisons
2. **Simple to implement**: Core logic is straightforward once understood
3. **Predictable performance**: Worst case is logarithmic, no surprises
4. **Minimal space**: Iterative version uses \(O(1)\) extra space

### Limitations

1. **Requires sorted data**: Sorting costs \(O(n \log n)\), may not be worth it for single search
   - **Workaround**: If searching multiple times, sort once and reuse
2. **Random access required**: Doesn't work efficiently on linked lists
   - **Workaround**: Use different data structures (e.g., balanced BST)
3. **Not optimal for small arrays**: Linear search simpler for n < 10
   - **Workaround**: Use linear search for small subarrays (hybrid approach)
4. **Difficult to implement correctly**: Off-by-one errors are common
   - **Workaround**: Use well-tested libraries or thoroughly test boundary cases

### When to Use vs When to Avoid

**Use When**:
- Searching in large sorted datasets
- Multiple searches on same data
- Need guaranteed \(O(\log n)\) performance

**Avoid When**:
- Data is unsorted and sorting cost isn't justified
- Working with linked lists or sequential access structures
- Array is very small (< 10 elements)
- Data changes frequently (sorting overhead)

---

## Comparison with Similar Concepts

### Binary Search vs Linear Search vs Hash Table

| Aspect | Binary Search | Linear Search | Hash Table |
|:-------|:--------------|:--------------|:-----------|
| **Time Complexity (Search)** | \(O(\log n)\) | \(O(n)\) | \(O(1)\) average |
| **Requires Sorted Data** | Yes | No | No |
| **Space Complexity** | \(O(1)\) | \(O(1)\) | \(O(n)\) |
| **Best Use Case** | Sorted arrays | Small or unsorted data | Frequent lookups |
| **Insertion Cost** | \(O(n)\) | \(O(1)\) | \(O(1)\) average |

---

## Practice & Exercises

### Conceptual Questions

<details>
<summary><strong>Q1: Why must the array be sorted for binary search?</strong></summary>

**Answer**: Binary search relies on the ordering property to make decisions. When comparing the target with the middle element, we can definitively eliminate half the array because we know all elements on one side are either smaller or larger. Without sorting, we can't make this guarantee.
</details>

<details>
<summary><strong>Q2: What is the maximum number of comparisons for an array of 1000 elements?</strong></summary>

**Answer**: \(\lceil \log_2 1000 \rceil = 10\) comparisons. Each comparison halves the search space, and \(2^{10} = 1024\), which is just larger than 1000.
</details>

<details>
<summary><strong>Q3: Can binary search be applied to linked lists efficiently?</strong></summary>

**Answer**: No. Binary search requires random access (\(O(1)\) access to any element). Linked lists have \(O(n)\) access time to reach the middle element, defeating the purpose of binary search. Use a balanced BST instead for \(O(\log n)\) search in linked structures.
</details>

### Problem-Solving Exercises

#### Easy
1. **First Bad Version**: You have n versions [1, 2, ..., n] and an API `isBadVersion(version)`. Find the first bad version. Minimize API calls.
   - **Hint**: Binary search on version numbers

#### Medium
2. **Search in Rotated Sorted Array**: Array is sorted then rotated at unknown pivot. Example: `[4,5,6,7,0,1,2]`. Find target in \(O(\log n)\).
   - **Hint**: Modified binary search considering rotation

3. **Find Peak Element**: Array where `arr[i] != arr[i+1]`. Find any peak (element greater than neighbors).
   - **Hint**: Binary search on array considering ascending/descending slopes

#### Hard
4. **Median of Two Sorted Arrays**: Given two sorted arrays, find median in \(O(\log(m+n))\).
   - **Hint**: Binary search on partition points

### Online Practice
- **LeetCode**: #704 Binary Search, #35 Search Insert Position, #33 Search in Rotated Sorted Array
- **HackerRank**: Binary Search challenges in Algorithm section
- **Codeforces**: Search problems tagged "binary search"

---

## Real-World Application

### Where Binary Search is Used

1. **Database Systems**: 
   - B-tree indexes use binary search principles
   - Query optimization for range searches

2. **Operating Systems**:
   - Finding free memory blocks in sorted free lists
   - System call tables (finding handler by ID)

3. **Libraries & APIs**:
   - `std::binary_search()` in C++ STL
   - `Arrays.binarySearch()` in Java
   - `bisect` module in Python

4. **Version Control**:
   - `git bisect` finds which commit introduced a bug using binary search

5. **Machine Learning**:
   - Hyperparameter tuning using binary search on parameter space
   - Finding optimal thresholds in classification

### Industry Example: Git Bisect

**Problem**: A bug appeared somewhere in the last 1000 commits. Which commit introduced it?

**Solution**: `git bisect` uses binary search:
1. Mark current commit as "bad" (has bug)
2. Mark old commit as "good" (no bug)
3. Git checks out middle commit
4. Developer tests and marks as good/bad
5. Repeat until bug-introducing commit found

**Result**: Find problematic commit in ~10 tests instead of 1000!

---

## Related Theory

### Prerequisites
- [Arrays](./arrays.md) - Understanding array indexing and access
- [Algorithm Analysis](./algorithm-analysis.md) - Big-O notation
- [Recursion](./recursion.md) - For recursive implementation

### Related Topics
- [Divide and Conquer](./divide-and-conquer.md) - General paradigm
- [Binary Search Trees](./binary-search-tree.md) - Binary search in tree form
- [Sorting Algorithms](./sorting-algorithms.md) - Creating sorted data
- [Lower/Upper Bound](./bounds.md) - Binary search variants

### Advanced Extensions
- [Exponential Search](./exponential-search.md) - For unbounded searches
- [Interpolation Search](./interpolation-search.md) - Better for uniformly distributed data
- [Ternary Search](./ternary-search.md) - Finding extrema in unimodal functions

---

## Further Reading

### Academic Resources

**Textbooks**:
1. *Introduction to Algorithms* (CLRS), Chapter 2 - Binary search analysis
2. *The Algorithm Design Manual* by Skiena - Practical binary search applications
3. *Programming Pearls* by Bentley - Chapter on binary search edge cases

**Papers**:
- Bentley, J. (1986). "Programming Pearls: Algorithm Design Techniques" *Communications of the ACM*

### Online Resources

**Tutorials**:
- [VisuAlgo - Binary Search Visualization](https://visualgo.net/en/bst)
- [TopCoder Binary Search Tutorial](https://www.topcoder.com/community/competitive-programming/tutorials/binary-search)

**Interactive**:
- [Binary Search Game](https://www.cs.usfca.edu/~galles/visualization/Search.html)

---

## References

1. Knuth, D. (1998). *The Art of Computer Programming, Vol. 3: Sorting and Searching*. Addison-Wesley.
2. Cormen, T., Leiserson, C., Rivest, R., Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). MIT Press.
3. Bentley, J. (1999). *Programming Pearls* (2nd ed.). Addison-Wesley.

---

<div align="center">

**[Back to Foundational Theory](./README.md)** | **[View All Topics](../README.md)** | **[Report Issue](../../issues/new?template=bug_report.md)**

---

Part of [MON CS DOCS](../../README.md) | Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

If you found this helpful, star the [repository](https://github.com/Moebius-Order/moncsdocs)!

</div>