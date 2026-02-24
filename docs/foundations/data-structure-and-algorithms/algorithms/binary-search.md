---
title: "Binary Search"
category: "Algorithms"
pillar: "Foundational Theory"
tags: ["algorithms", "searching", "divide-and-conquer", "arrays"]
difficulty: "Beginner"
prerequisites: ["arrays", "algorithm-analysis", "recursion"]
estimated_time: "20 minutes"
last_updated: "2026-02-23"
author: "Moebius Order"
contributors: []
reviewers: []
version: "1.1"
status: "Published"
---

# Binary Search

## The Core Concept

Binary search is an elegant algorithm that finds a target value in a **sorted array** by repeatedly eliminating half of the remaining possibilities. Imagine searching for a word in a dictionary—you don't start at page 1 and flip through sequentially. You open somewhere in the middle, check if you're too far ahead or behind, then repeat the process with the correct half.

This "divide-and-conquer" strategy is what makes binary search so powerful: every comparison reduces the search space by 50%, leading to logarithmic time complexity.

**The essential requirement:** The array must be sorted. Without order, we can't make logical deductions about which half contains our target.

---

## The Problem

Searching is everywhere in computing. Every time you:
- Look up a contact in your phone
- Find a file on your computer
- Query a database
- Use autocomplete

...you're using a search algorithm.

### Why Linear Search Falls Short

**Linear search** (checking each element one by one) works, but it doesn't scale:

```
Array size     Average comparisons (linear)
10             5
100            50
1,000          500
1,000,000      500,000
1,000,000,000  500,000,000
```

For a billion elements, linear search might take **seconds**. In a world where users expect millisecond response times, this is unacceptable.

### The Key Insight

If data is sorted, we can be **strategic**. When we check the middle element:
- If target < middle: target must be in the left half (if it exists)
- If target > middle: target must be in the right half (if it exists)
- If target == middle: found it!

We've just eliminated half the array with a single comparison. Do this repeatedly, and we can search a billion elements in about 30 comparisons.

**The trade-off:** Sorting costs \(O(n \log n)\), but if we search many times, the cost amortizes. One sort, many searches—that's the sweet spot for binary search.

---

## Historical Context

### The Surprisingly Tricky History

Binary search seems simple, but correct implementation eluded programmers for years:

**1946:** John Mauchly first described the algorithm in "Theory and Techniques for Design of Electronic Digital Computers"
- Context: Searching sorted punch card systems
- Problem: Computers had tiny memories; efficiency was critical

**1962:** Donald Knuth published the first **provably correct** implementation
- That's a **16-year gap**!
- Why? Off-by-one errors in boundary conditions are notoriously subtle

**1960s-1980s:** Studies found that most published binary search implementations had bugs

**2006:** A bug was found in Java's `Arrays.binarySearch()` that had existed since 1994
- The issue: `mid = (low + high) / 2` causes integer overflow for large arrays
- The fix: `mid = low + (high - low) / 2`

This history reminds us: **simple concepts can have complex implementations**.

---

## How Binary Search Works: The Mechanics

### The Setup

We maintain three pointers into the array:

```
Array: [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
Index:  0  1  2   3   4   5   6   7   8   9  10
        ↑                   ↑                   ↑
       left              middle              right
```

**Initial state:**
- `left = 0` (first index)
- `right = n - 1` (last index)
- `middle = left + (right - left) / 2` (midpoint)

### The Algorithm: Step by Step

**Step 1: Calculate middle**

We use this formula:

\[
\text{middle} = \text{left} + \left\lfloor \frac{\text{right} - \text{left}}{2} \right\rfloor
\]

**Why not just `(left + right) / 2`?**

Consider `left = 2,000,000,000` and `right = 2,000,000,100`:
- `left + right = 4,000,000,100`
- In 32-bit systems, max int = 2,147,483,647
- **Overflow!** Result wraps to negative number
- Bug: returns wrong index or crashes

Using `left + (right - left) / 2`:
- `right - left = 100`
- `100 / 2 = 50`
- `left + 50 = 2,000,000,050`
- No overflow, correct answer

This is the infamous Java bug mentioned earlier.

**Step 2: Compare**

```python
if array[middle] == target:
    return middle  # Found it!
```

If we're lucky, we found it immediately. Best case: \(O(1)\).

**Step 3: Eliminate half**

```python
if target < array[middle]:
    right = middle - 1  # Search left half
else:
    left = middle + 1   # Search right half
```

**Critical detail:** We set `right = middle - 1`, not `middle`.

Why? We already checked `middle`, so we can exclude it. If we set `right = middle`, we might loop forever.

**Step 4: Repeat**

Continue while `left <= right`. When `left > right`, the search space is empty—target doesn't exist.

### Complete Visual Walkthrough

Let's search for **target = 45** in `[2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]`

**Initial state:**
```
Array: [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
Index:  0  1  2   3   4   5   6   7   8   9  10
        ↑                   ↑                   ↑
       left              middle              right
       (0)                (5)                (10)

middle = 0 + (10 - 0) / 2 = 5
array[5] = 23
Compare: 45 > 23
Action: Search right half
Update: left = 5 + 1 = 6
```

**After iteration 1:**
```
Array: [2, 5, 8, 12, 16, 23, | 38, 45, 56, 67, 78]
Index:  0  1  2   3   4   5     6   7   8   9  10
                                 ↑   ↑           ↑
                                left mid        right
                                (6)  (8)        (10)

middle = 6 + (10 - 6) / 2 = 8
array[8] = 56
Compare: 45 < 56
Action: Search left half
Update: right = 8 - 1 = 7
```

**After iteration 2:**
```
Array: [2, 5, 8, 12, 16, 23, | 38, 45, | 56, 67, 78]
Index:  0  1  2   3   4   5     6   7     8   9  10
                                 ↑  ↑
                                left/mid/right
                                 (6) (7)

middle = 6 + (7 - 6) / 2 = 6
array[6] = 38
Compare: 45 > 38
Action: Search right half
Update: left = 6 + 1 = 7
```

**After iteration 3:**
```
Array: [2, 5, 8, 12, 16, 23, 38, | 45 | 56, 67, 78]
Index:  0  1  2   3   4   5   6     7    8   9  10
                                      ↑
                                  left/mid/right
                                      (7)

middle = 7 + (7 - 7) / 2 = 7
array[7] = 45
Compare: 45 == 45
FOUND! Return 7
```

**Total comparisons:** 3 (compared to 8 for linear search if we started from index 0)

---

## Mathematical Formalization

### Formal Algorithm Definition

**Given:**
- A sorted array \(A = [a_0, a_1, a_2, \ldots, a_{n-1}]\) where \(a_i \le a_{i+1}\) for all \(i\)
- A target value \(x\)

**Find:**
- An index \(i\) such that \(A[i] = x\), or
- Return \(-1\) (or `null`) if no such \(i\) exists

**Algorithm:**

```
BinarySearch(A, x):
    left ← 0
    right ← length(A) - 1
    
    while left ≤ right do:
        middle ← left + ⌊(right - left) / 2⌋
        
        if A[middle] = x then:
            return middle
        else if A[middle] < x then:
            left ← middle + 1
        else:
            right ← middle - 1
    
    return -1  // Not found
```

### Correctness Proof

We prove binary search is correct using a **loop invariant**:

**Invariant:** If \(x\) exists in \(A\), then \(x\) is in the subarray \(A[\text{left} \ldots \text{right}]\)

**Proof by induction:**

**Base case (initialization):**
- Initially, `left = 0` and `right = n - 1`
- Subarray \(A[0 \ldots n-1]\) is the entire array
- If \(x\) exists anywhere, it's in this range
- Invariant holds

**Inductive step (maintenance):**

Assume invariant holds before an iteration. Three cases:

**Case 1:** \(A[\text{middle}] = x\)
- We return `middle` immediately
- Correct!

**Case 2:** \(A[\text{middle}] < x\)
- Since array is sorted, all elements left of `middle` are ≤ \(A[\text{middle}] < x\)
- So \(x\) cannot be in \(A[\text{left} \ldots \text{middle}]\)
- If \(x\) exists, it must be in \(A[\text{middle}+1 \ldots \text{right}]\)
- We set `left = middle + 1`
- Invariant maintained

**Case 3:** \(A[\text{middle}] > x\)
- Since array is sorted, all elements right of `middle` are ≥ \(A[\text{middle}] > x\)
- So \(x\) cannot be in \(A[\text{middle} \ldots \text{right}]\)
- If \(x\) exists, it must be in \(A[\text{left} \ldots \text{middle}-1]\)
- We set `right = middle - 1`
- Invariant maintained

**Termination:**
- Each iteration, either:
  - We find \(x\) and return, or
  - Search space reduces by at least half
- Since search space size decreases, eventually `left > right`
- When `left > right`, search space is empty
- By invariant, if we haven't found \(x\), it doesn't exist
- Returning -1 is correct

Thus, binary search is **correct**.

### Time Complexity Analysis

Let \(T(n)\) be the worst-case number of comparisons for an array of size \(n\).

**Recurrence relation:**

After one comparison, we search a subarray of size \(\lfloor n/2 \rfloor\):

\[
T(n) = T\left(\left\lfloor \frac{n}{2} \right\rfloor\right) + 1
\]

where the "+1" is for the comparison at this level.

**Base case:** \(T(1) = 1\) (one element, one comparison)

**Expanding the recurrence:**

\[
\begin{align}
T(n) &= T(n/2) + 1 \\
&= (T(n/4) + 1) + 1 \\
&= T(n/4) + 2 \\
&= (T(n/8) + 1) + 2 \\
&= T(n/8) + 3 \\
&\vdots \\
&= T(n/2^k) + k
\end{align}
\]

We stop when \(n/2^k = 1\), which means \(2^k = n\), so \(k = \log_2 n\).

Therefore:

\[
T(n) = T(1) + \log_2 n = 1 + \log_2 n
\]

**Result:** \(T(n) = O(\log n)\)

### Space Complexity

**Iterative implementation:**

\[
\text{Space} = O(1)
\]

We only use a constant number of variables (`left`, `right`, `middle`, regardless of \(n\)).

**Recursive implementation:**

\[
\text{Space} = O(\log n)
\]

Each recursive call adds a frame to the call stack. Maximum recursion depth is \(\log n\) (the height of the binary search tree).

**Example:** For \(n = 1024\):
- Iterative: 3-4 integer variables ≈ 12-16 bytes
- Recursive: 10 stack frames × ~20 bytes/frame ≈ 200 bytes

For large \(n\), iterative is more memory-efficient.

### Why Logarithmic is Powerful

Let's see how \(\log_2 n\) grows:

```
n              log₂(n)    Comparisons needed
10                3.3      4
100               6.6      7
1,000            10        10
10,000           13        13
100,000          17        17
1,000,000        20        20
1,000,000,000    30        30
```

Notice: **Every time we add a zero to \(n\) (multiply by 10), we add only ~3 comparisons**.

Compare to linear search:

```
n              Linear    Binary    Speedup
1,000          1,000     10        100×
1,000,000      1,000,000 20        50,000×
1,000,000,000  1 billion 30        33 million×
```

This is why binary search is called "logarithmic" and why it's so effective for large datasets.

---

## Worked Example: Complete Trace

### Problem

Find **target = 31** in array `[3, 7, 12, 18, 24, 31, 42, 55, 63]`

**Array size:** \(n = 9\)

**Expected comparisons:** \(\lceil \log_2 9 \rceil = \lceil 3.17 \rceil = 4\) (worst case)

### Detailed Execution

**Initial State:**
```
Array:  [3,  7,  12, 18, 24, 31, 42, 55, 63]
Index:   0   1   2   3   4   5   6   7   8
         ↑                   ↑               ↑
        left             middle          right
```

Variables:
- `left = 0`
- `right = 8`
- `target = 31`

---

**Iteration 1:**

Calculate middle:

\[
\text{middle} = 0 + \left\lfloor \frac{8 - 0}{2} \right\rfloor = 0 + 4 = 4
\]

Compare:

\[
\text{array}[4] = 24 \stackrel{?}{=} 31
\]

\(24 < 31\), so target is in the **right half**.

Update:
- `left = middle + 1 = 5`
- `right = 8` (unchanged)

Search space reduced:
```
Array:  [3,  7,  12, 18, 24, | 31, 42, 55, 63]
Index:   0   1   2   3   4     5   6   7   8
                                ↑           ↑
                               left       right
```

New size: 4 elements (was 9)

---

**Iteration 2:**

Calculate middle:

\[
\text{middle} = 5 + \left\lfloor \frac{8 - 5}{2} \right\rfloor = 5 + 1 = 6
\]

Compare:

\[
\text{array}[6] = 42 \stackrel{?}{=} 31
\]

\(42 > 31\), so target is in the **left half** (of our current range).

Update:
- `left = 5` (unchanged)
- `right = middle - 1 = 5`

Search space reduced:
```
Array:  [3,  7,  12, 18, 24, | 31 | 42, 55, 63]
Index:   0   1   2   3   4     5    6   7   8
                                ↑
                            left/right
```

New size: 1 element (was 4)

---

**Iteration 3:**

Calculate middle:

\[
\text{middle} = 5 + \left\lfloor \frac{5 - 5}{2} \right\rfloor = 5 + 0 = 5
\]

Compare:

\[
\text{array}[5] = 31 \stackrel{?}{=} 31
\]

**Match!** Return `middle = 5`.

---

**Summary:**
- **Total comparisons:** 3
- **Predicted max:** 4
- **Linear search would need:** 6 comparisons (if starting from left)

Binary search is twice as fast in this example, and the advantage grows exponentially with array size.

---

## Practical Implementation Examples

### Iterative Implementation (Recommended)

```python
def binary_search(array, target):
    """
    Iterative binary search - most efficient.
    
    Args:
        array: Sorted list of comparable elements
        target: Element to search for
    
    Returns:
        Index of target if found, -1 otherwise
    
    Time: O(log n)
    Space: O(1)
    """
    left = 0
    right = len(array) - 1
    
    while left <= right:
        # Prevent overflow: don't use (left + right) // 2
        middle = left + (right - left) // 2
        
        if array[middle] == target:
            return middle  # Found
        elif array[middle] < target:
            left = middle + 1  # Search right half
        else:
            right = middle - 1  # Search left half
    
    return -1  # Not found


# Test
data = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
print(binary_search(data, 23))  # Output: 5
print(binary_search(data, 50))  # Output: -1 (not found)
```

### Recursive Implementation

```python
def binary_search_recursive(array, target, left=0, right=None):
    """
    Recursive binary search - elegant but uses call stack.
    
    Time: O(log n)
    Space: O(log n) due to recursion stack
    """
    if right is None:
        right = len(array) - 1
    
    # Base case: search space empty
    if left > right:
        return -1
    
    middle = left + (right - left) // 2
    
    if array[middle] == target:
        return middle
    elif array[middle] < target:
        # Recurse on right half
        return binary_search_recursive(array, target, middle + 1, right)
    else:
        # Recurse on left half
        return binary_search_recursive(array, target, left, middle - 1)
```

**Recursion tree visualization for `n = 8`:**

```
                    [0...7] n=8
                   /            \
            [0...3] n=4        [4...7] n=4
           /        \          /        \
      [0...1]    [2...3]  [4...5]    [6...7]  n=2
      /    \     /    \    /    \     /    \
    [0]   [1] [2]   [3] [4]   [5]  [6]   [7]  n=1

Depth = log₂(8) = 3 levels
```

Each level halves the problem size—classic divide-and-conquer.

### Advanced: Finding Insertion Point (Lower Bound)

```python
def binary_search_insert_position(array, target):
    """
    Find the leftmost position where target should be inserted
    to maintain sorted order.
    
    Returns:
        Index where target should be inserted.
        If target exists, returns index of first occurrence.
    
    Example:
        array = [1, 2, 2, 2, 5, 7]
        binary_search_insert_position(array, 2) -> 1 (first 2)
        binary_search_insert_position(array, 4) -> 4 (between 2 and 5)
    """
    left = 0
    right = len(array)
    
    while left < right:  # Note: < not <=
        middle = left + (right - left) // 2
        
        if array[middle] < target:
            left = middle + 1
        else:
            # Even if equal, keep searching left for first occurrence
            right = middle
    
    return left


# Test with duplicates
data = [1, 2, 2, 2, 5, 7, 9]
print(binary_search_insert_position(data, 2))   # 1 (first 2)
print(binary_search_insert_position(data, 4))   # 4 (before 5)
print(binary_search_insert_position(data, 10))  # 7 (end of array)
```

This variant is useful for:
- Maintaining sorted lists with insertions
- Finding ranges of duplicate elements
- Database indexing operations

---

## Variations & Extensions

### Lower Bound and Upper Bound

**Lower bound:** First position where `element >= target`

**Upper bound:** First position where `element > target`

These let you find the **range** of duplicates in \(O(\log n)\) time.

**Example:**
```
Array: [1, 2, 2, 2, 2, 5, 7]
Target: 2

Lower bound: 1 (first 2)
Upper bound: 5 (first element > 2, which is 5)
Range of 2's: [1, 5) -> indices 1, 2, 3, 4
```

Useful for database queries like "find all records between dates A and B."

### Binary Search on Answer Space

**Concept:** Binary search doesn't only work on arrays—it works on any **monotonic function**.

**Problem:** Find the square root of \(x\) to 6 decimal places.

**Solution:** Binary search on the range \([0, x]\):

```python
def sqrt_binary_search(x, precision=1e-6):
    left, right = 0, x
    
    while right - left > precision:
        mid = (left + right) / 2
        if mid * mid < x:
            left = mid
        else:
            right = mid
    
    return (left + right) / 2
```

We're searching for the **value** where \(\text{value}^2 = x\), not an array index.

**Applications:**
- Finding roots of equations
- Minimizing/maximizing functions
- Optimization problems ("minimize cost such that constraint is satisfied")

### Binary Search on Rotated Arrays

**Problem:** Array is sorted, then rotated at an unknown pivot.

**Example:** `[4, 5, 6, 7, 0, 1, 2]` (rotated at index 4)

**Challenge:** Normal binary search fails because ordering is broken.

**Solution:** Modified binary search that determines which half is sorted:

```python
def search_rotated(array, target):
    left, right = 0, len(array) - 1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if array[mid] == target:
            return mid
        
        # Determine which half is sorted
        if array[left] <= array[mid]:  # Left half is sorted
            if array[left] <= target < array[mid]:
                right = mid - 1  # Target in sorted left half
            else:
                left = mid + 1   # Target in rotated right half
        else:  # Right half is sorted
            if array[mid] < target <= array[right]:
                left = mid + 1   # Target in sorted right half
            else:
                right = mid - 1  # Target in rotated left half
    
    return -1
```

Still \(O(\log n)\), but requires careful logic to handle the rotation.

---

## Common Misconceptions

### Misconception 1: "Binary search works on unsorted data"

**False.** Binary search's correctness relies on the sorted property.

**Counterexample:**
```
Array: [5, 2, 8, 1, 9]
Target: 1

Binary search:
- middle = 2, array[2] = 8
- 1 < 8, so search left half: [5, 2]
- middle = 0, array[0] = 5
- 1 < 5, so search left... but left = 0, right = -1
- Not found!

But 1 IS in the array at index 3.
```

Binary search fails silently on unsorted data—no error, just wrong results.

### Misconception 2: "(left + right) / 2 is fine"

**Risky.** This causes **integer overflow** in languages with fixed-size integers.

**Example in Java (32-bit ints):**
```java
int left = 2_000_000_000;
int right = 2_000_000_100;
int mid = (left + right) / 2;  // Overflow!

// left + right = 4,000,000,100
// Max int = 2,147,483,647
// Result wraps to: -294,967,196
// mid = -147,483,598 (wrong!)
```

**Correct:**
```java
int mid = left + (right - left) / 2;

// right - left = 100
// 100 / 2 = 50
// mid = 2,000,000,050 (correct)
```

This bug existed in Java's standard library for 12 years (1994-2006)!

### Misconception 3: "Binary search is always faster than linear"

**Not for small arrays.** Binary search has higher **overhead**:

```
Operations per comparison:
- Linear search: 1 comparison, 1 increment
- Binary search: 1 comparison, 2 subtractions, 1 division, 2 assignments
```

**Crossover point:** Typically around \(n = 10\).

Many optimized sorting algorithms (like Timsort, used in Python) switch to insertion sort for small subarrays.

**Rule of thumb:**
- \(n < 10\): Linear search often faster
- \(n = 10\text{-}100\): About equal
- \(n > 100\): Binary search dominates

---

## Advantages & Limitations

### Advantages

1. **Extremely efficient for large datasets**
   - Searching 1 million elements: ~20 comparisons
   - Searching 1 billion elements: ~30 comparisons

2. **Predictable performance**
   - Worst case = average case = \(O(\log n)\)
   - No performance surprises

3. **Minimal memory**
   - Iterative version: \(O(1)\) extra space
   - Just a few integer variables

4. **Provably optimal**
   - For comparison-based search in sorted arrays, you can't beat \(O(\log n)\)

### Limitations

1. **Requires sorted data**
   - Sorting costs \(O(n \log n)\)
   - Only worth it if searching multiple times
   - **Breakeven:** If you'll search \(\geq n\) times, sorting pays off

2. **Requires random access**
   - Doesn't work on linked lists (accessing middle takes \(O(n)\))
   - Requires array or similar structure

3. **Not optimal for small arrays**
   - Overhead outweighs benefits for \(n < 10\)

4. **Implementation subtlety**
   - Easy to get wrong (off-by-one errors, overflow)
   - Use well-tested library implementations when possible

### When to Use

**Use binary search when:**
- Data is **already sorted** or will be searched many times
- Working with **large datasets** (\(n > 100\))
- Need **guaranteed** \(O(\log n)\) performance
- Using **arrays** or random-access structures

**Avoid binary search when:**
- Data is **unsorted** and sorting cost isn't justified
- Working with **linked lists** or sequential structures
- Array is **very small** (\(n < 10\))
- Data **changes frequently** (insertions/deletions break sorting)

**Alternative:** Use hash tables for \(O(1)\) average-case search (but with \(O(n)\) space).

---

## Comparison with Alternatives

| Aspect | Binary Search | Linear Search | Hash Table | Binary Search Tree |
|:-------|:--------------|:--------------|:-----------|:-------------------|
| **Search Time** | \(O(\log n)\) | \(O(n)\) | \(O(1)\) average, \(O(n)\) worst | \(O(\log n)\) balanced |
| **Requires Sorted** | Yes | No | No | Maintains order |
| **Space** | \(O(1)\) | \(O(1)\) | \(O(n)\) | \(O(n)\) |
| **Insert Cost** | \(O(n)\) | \(O(1)\) end | \(O(1)\) average | \(O(\log n)\) balanced |
| **Delete Cost** | \(O(n)\) | \(O(n)\) | \(O(1)\) average | \(O(\log n)\) balanced |
| **Best Use Case** | Read-heavy sorted data | Small/unsorted data | Frequent lookups | Dynamic sorted data |

**Key insight:** Choose data structure based on operation frequency:
- Mostly searching, rarely modifying → Binary search on sorted array
- Frequent insertions/deletions → Balanced BST
- Pure lookups, no order needed → Hash table
- Small data → Linear search (simplicity wins)

---

## Practice Exercises

### Conceptual Questions

**Q1: Why must the array be sorted?**

<details>
<summary>Click to reveal answer</summary>

Binary search's correctness depends on making logical deductions from comparisons. When we find `array[middle] < target`, we conclude "target must be in the right half." This is only valid if the array is sorted.

In an unsorted array:
```
[5, 2, 8, 1, 9], target = 1
middle = 2, array[2] = 8
1 < 8, search left: [5, 2]
```

But `1` is actually at index 3 (right side). The algorithm fails because we can't trust the "left < right" property.
</details>

**Q2: What's the maximum number of comparisons for \(n = 1000\)?**

<details>
<summary>Click to reveal answer</summary>

\(\lceil \log_2 1000 \rceil = \lceil 9.97 \rceil = 10\) comparisons.

Why? After \(k\) comparisons, we've narrowed the search to \(n / 2^k\) elements. We stop when this reaches 1:

\[
\frac{1000}{2^k} = 1 \implies 2^k = 1000 \implies k = \log_2 1000 \approx 9.97
\]

Round up to 10 since we need an integer number of comparisons.
</details>

**Q3: Can binary search work on linked lists efficiently?**

<details>
<summary>Click to reveal answer</summary>

No. Binary search requires \(O(1)\) access to the middle element. In a linked list:

```
Array: middle = array[n/2]  -> O(1)
Linked list: middle = traverse n/2 nodes -> O(n)
```

Each iteration of binary search would take \(O(n)\) to find the middle, giving total time \(O(n \log n)\)—worse than linear search!

**Solution for linked lists:** Use a balanced binary search tree instead (\(O(\log n)\) search with \(O(\log n)\) insert/delete).
</details>

### Coding Problems

**Easy:**
1. **First Bad Version:** Given `n` versions and a function `isBadVersion(v)`, find the first bad version minimizing API calls.
   - Hint: Binary search on version numbers

**Medium:**
2. **Search in Rotated Sorted Array:** Array is sorted then rotated (e.g., `[4,5,6,7,0,1,2]`). Find target in \(O(\log n)\).
   - Hint: Determine which half is sorted

3. **Find Peak Element:** In array where `arr[i] != arr[i+1]`, find any index `i` where `arr[i] > arr[i-1]` and `arr[i] > arr[i+1]`.
   - Hint: Binary search on slope direction

**Hard:**
4. **Median of Two Sorted Arrays:** Given two sorted arrays, find the median in \(O(\log(m+n))\).
   - Hint: Binary search on partition points

---

## Real-World Applications

### Database Indexes (B-Trees)

Databases use B-trees, which are generalized binary search trees optimized for disk I/O:

```
Without index (linear scan):
- 1 million rows
- Check each row: 1,000,000 disk reads
- At 10ms/read: 2.8 hours

With B-tree index:
- Height = log(n) ≈ 20
- 20 disk reads
- At 10ms/read: 0.2 seconds
```

**Impact:** 50,000× speedup. This is why "add an index" often magically fixes slow queries.

### Git Bisect

Find which commit introduced a bug:

```bash
$ git bisect start
$ git bisect bad            # Current commit has bug
$ git bisect good v1.0      # v1.0 was fine

# Git checks out middle commit
$ run_tests.sh
# If tests fail:
$ git bisect bad
# If tests pass:
$ git bisect good

# Repeat ~log(n) times
# Git identifies exact commit
```

For 1000 commits, finds the bug in ~10 tests instead of testing all 1000.

### Operating Systems

OS maintains sorted free-block lists:

```
Free memory blocks: [0x1000-0x2000, 0x3000-0x5000, ...]

Allocation request: 4KB
- Binary search for suitable block: O(log n)
- Without: O(n) linear scan
```

Critical for OS performance as memory operations happen millions of times per second.

### Standard Libraries

Binary search is ubiquitous:

- **C++ STL:** `std::binary_search()`, `std::lower_bound()`, `std::upper_bound()`
- **Java:** `Arrays.binarySearch()`, `Collections.binarySearch()`
- **Python:** `bisect.bisect_left()`, `bisect.bisect_right()`
- **Go:** `sort.Search()`

These are highly optimized, battle-tested implementations. Use them instead of rolling your own.

---

## Related Topics

### Prerequisites
- [Arrays](./arrays.md) - Random access data structure
- [Algorithm Analysis](./algorithm-analysis.md) - Big-O notation
- [Recursion](./recursion.md) - For recursive implementation

### Related Algorithms
- [Divide and Conquer](./divide-and-conquer.md) - General paradigm
- [Binary Search Trees](./binary-search-tree.md) - Binary search in tree form
- [Sorting Algorithms](./sorting-algorithms.md) - Prerequisite for binary search

### Advanced Topics
- [Interpolation Search](./interpolation-search.md) - \(O(\log \log n)\) for uniformly distributed data
- [Exponential Search](./exponential-search.md) - For unbounded arrays
- [Ternary Search](./ternary-search.md) - For finding extrema in unimodal functions

---

## Further Reading

### Textbooks
1. **Introduction to Algorithms (CLRS)**, Chapter 2
   - Rigorous mathematical treatment
2. **The Algorithm Design Manual by Skiena**
   - Practical applications and war stories
3. **Programming Pearls by Bentley**
   - Chapter on binary search edge cases and bugs

### Papers
- Bentley, J. (1986). "Programming Pearls: Algorithm Design Techniques" *Communications of the ACM*
- Discusses the difficulty of getting binary search right

### Online Resources
- [VisuAlgo - Binary Search Visualization](https://visualgo.net/en/bst)
- [TopCoder Binary Search Tutorial](https://www.topcoder.com/community/competitive-programming/tutorials/binary-search)

---

## References

1. Knuth, D. (1998). *The Art of Computer Programming, Vol. 3: Sorting and Searching*. Addison-Wesley.
2. Cormen, T., Leiserson, C., Rivest, R., Stein, C. (2009). *Introduction to Algorithms* (3rd ed.). MIT Press.
3. Bentley, J. (1999). *Programming Pearls* (2nd ed.). Addison-Wesley.
4. Bloch, J. (2006). "Extra, Extra - Read All About It: Nearly All Binary Searches and Mergesorts are Broken." Google Research Blog.

---