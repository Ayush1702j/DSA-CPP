# 📚 Arrays in C++ — Theory and Problem Solving

Welcome to my **Arrays in C++** repository! 🚀

This repository is part of my **Data Structures and Algorithms (DSA) learning journey**. It contains theoretical explanations, C++ programs, examples, and practice problems to help beginners understand arrays and develop strong problem-solving skills.

The main goal is to learn arrays from the basics and gradually move toward advanced coding interview problems.

---

## 📌 Table of Contents

1. [Introduction to Arrays](#-1-introduction-to-arrays)
2. [Array Declaration and Initialization](#-2-array-declaration-and-initialization)
3. [Memory Representation](#-3-memory-representation-of-arrays)
4. [Array Traversal](#-4-array-traversal)
5. [Insertion and Deletion](#-5-insertion-and-deletion)
6. [Finding Minimum and Maximum](#-6-finding-minimum-and-maximum)
7. [Reversing an Array](#-7-reversing-an-array)
8. [Searching Algorithms](#-8-searching-algorithms)
9. [Sorting Algorithms](#-9-sorting-algorithms)
10. [Two Pointers Technique](#-10-two-pointers-technique)
11. [Prefix Sum](#-11-prefix-sum)
12. [Sliding Window](#-12-sliding-window)
13. [Subarrays](#-13-subarrays)
14. [Kadane's Algorithm](#-14-kadanes-algorithm)
15. [Binary Search on Answer](#-15-binary-search-on-answer)
16. [Monotonic Techniques](#-16-monotonic-techniques)
17. [Time and Space Complexity](#-17-time-and-space-complexity)
18. [Common Array Patterns](#-18-common-array-patterns)
19. [Beginner-to-Advanced Practice Problems](#-19-beginner-to-advanced-practice-problems)
20. [How to Run C++ Programs](#-20-how-to-run-c-programs)
21. [Learning Roadmap](#-21-learning-roadmap)

---

# 📖 1. Introduction to Arrays

## What is an Array?

An **array** is a linear data structure that stores multiple elements of the same data type in consecutive memory locations.

Instead of creating separate variables for every value, we can store multiple values under one variable name.

### Example Without an Array

```cpp
int marks1 = 75;
int marks2 = 80;
int marks3 = 90;
int marks4 = 85;
```

This approach becomes difficult when we need to store hundreds of values.

### Example Using an Array

```cpp
int marks[4] = {75, 80, 90, 85};
```

Now, all four marks are stored inside one array named `marks`.

### Important Characteristics

- **Same data type:** A normal C++ array stores elements of the same declared type.
- **Contiguous memory:** Its elements occupy consecutive memory locations.
- **Index-based access:** We access elements using their positions, called indices.
- **Fixed size:** A built-in array has a fixed size after it is created.
- **Fast access:** Accessing an element by index takes constant time, O(1).

## Understanding Array Indexing

In C++, array indexing starts from **0**, not 1.

Consider this array:

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

| Index | Element |
|---:|---:|
| 0 | 10 |
| 1 | 20 |
| 2 | 30 |
| 3 | 40 |
| 4 | 50 |

To access an element:

```cpp
cout << arr[0];  // Output: 10
cout << arr[3];  // Output: 40
```

**Important:** For an array of size `n`, valid indices are from `0` to `n - 1`. Accessing an invalid index causes undefined behavior.

---

# 🧱 2. Array Declaration and Initialization

## 2.1 Declaration

Declaration specifies the data type, name, and size of an array.

```cpp
int arr[5];
```

This creates space for five integers. If it is a local built-in array, its elements are not automatically initialized.

## 2.2 Initialization

Initialization means assigning initial values to an array.

```cpp
int arr[5] = {10, 20, 30, 40, 50};
```

You can also let the compiler determine the size:

```cpp
int arr[] = {10, 20, 30};
```

The size is automatically determined as 3.

## 2.3 Partial Initialization

```cpp
int arr[5] = {10, 20};
```

The array contains:

```text
10 20 0 0 0
```

When a built-in array is initialized with a braced list, the remaining elements are zero-initialized.

## 2.4 Accessing and Updating Elements

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[3] = {10, 20, 30};

    cout << arr[1] << endl;

    arr[1] = 100;

    cout << arr[1] << endl;

    return 0;
}
```

Output:

```text
20
100
```

## 2.5 Using `std::vector`

In modern C++, `vector` is often more convenient than a built-in array because it can grow or shrink dynamically.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    vector<int> arr = {10, 20, 30};

    arr.push_back(40);

    cout << arr.size() << endl;

    return 0;
}
```

Output:

```text
4
```

Use built-in arrays when learning fixed-size arrays, and use `vector` when you need a resizable sequence.

---

# 🧠 3. Memory Representation of Arrays

Array elements are stored in contiguous memory locations.

Suppose:

```cpp
int arr[4] = {10, 20, 30, 40};
```

Assume the first element starts at address `1000` and each integer occupies 4 bytes.

| Index | Value | Example address |
|---:|---:|---:|
| 0 | 10 | 1000 |
| 1 | 20 | 1004 |
| 2 | 30 | 1008 |
| 3 | 40 | 1012 |

These addresses are illustrative. Actual addresses depend on the program and system.

### Address Calculation

For an array whose first element is at address `B`, the address of element `arr[i]` is:

`Address = B + (i × size of each element)`

For example, the address of `arr[2]` is:

`1000 + (2 × 4) = 1008`

This explains why accessing an array element by index takes **O(1)** time.

---

# 🔄 4. Array Traversal

Traversal means visiting each element of an array, usually to print or process its values.

### Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = 5;

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

### How It Works

1. Start with index `0`.
2. Access `arr[i]`.
3. Perform an operation, such as printing the element.
4. Increase `i` by 1.
5. Continue until `i` reaches `n`.

### Complexity

- Time: O(n), because each element is visited once.
- Extra space: O(1), because no additional array is created.

---

# ✏️ 5. Insertion and Deletion

Insertion means adding an element at a particular position. Deletion means removing an element.

For a built-in array, the allocated size does not change automatically. These operations require shifting elements within the existing capacity or using a different structure such as `vector`.

## 5.1 Insertion at a Position

Suppose:

```text
Array: 10 20 30 40
Insert 25 at index 2
```

The result is:

```text
10 20 25 30 40
```

Elements from the insertion position onward must be shifted to the right.

### C++ Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[10] = {10, 20, 30, 40};
    int n = 4;
    int position = 2;
    int value = 25;

    for (int i = n; i > position; i--) {
        arr[i] = arr[i - 1];
    }

    arr[position] = value;
    n++;

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 25 30 40
```

This example assumes the array has enough unused capacity and that the position is valid.

## 5.2 Deletion from a Position

Suppose:

```text
Array: 10 20 30 40 50
Delete the element at index 2
```

The result is:

```text
10 20 40 50
```

### C++ Example

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = 5;
    int position = 2;

    for (int i = position; i < n - 1; i++) {
        arr[i] = arr[i + 1];
    }

    n--;

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 40 50
```

### Complexity

| Operation | Typical time complexity |
|---|---|
| Insert at the end when capacity is available | O(1) |
| Insert at the beginning | O(n) |
| Insert in the middle | O(n) |
| Delete from the end | O(1) |
| Delete from the beginning | O(n) |
| Delete from the middle | O(n) |

For `vector`, appending with `push_back()` is O(1) amortized. Inserting or erasing at the beginning or middle is generally O(n) because elements must shift.

---

# 🔍 6. Finding Minimum and Maximum

Finding the minimum means identifying the smallest element. Finding the maximum means identifying the largest element.

Example:

```text
Array: 12 5 28 7 19
Minimum: 5
Maximum: 28
```

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {12, 5, 28, 7, 19};
    int n = 5;

    int minimum = arr[0];
    int maximum = arr[0];

    for (int i = 1; i < n; i++) {
        if (arr[i] < minimum) {
            minimum = arr[i];
        }

        if (arr[i] > maximum) {
            maximum = arr[i];
        }
    }

    cout << "Minimum: " << minimum << endl;
    cout << "Maximum: " << maximum << endl;

    return 0;
}
```

Output:

```text
Minimum: 5
Maximum: 28
```

### Why Start with `arr[0]`?

We use the first element as the initial minimum and maximum. Every remaining element is compared against these values.

This also works when all the elements are negative.

### Complexity

- Time: O(n)
- Extra space: O(1)

---

# 🔁 7. Reversing an Array

Reversing an array means arranging its elements in the opposite order.

Example:

```text
Original:  10 20 30 40 50
Reversed:  50 40 30 20 10
```

## Two-Pointer Approach

One pointer starts at the beginning, and another starts at the end. Swap their elements, then move both pointers toward the center.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int n = 5;

    int left = 0;
    int right = n - 1;

    while (left < right) {
        swap(arr[left], arr[right]);

        left++;
        right--;
    }

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
50 40 30 20 10
```

### Complexity

- Time: O(n)
- Extra space: O(1)

Only half the array needs to be swapped because the other half is handled simultaneously.

---

# 🔎 8. Searching Algorithms

Searching is the process of finding whether a particular value exists in an array and, if it does, locating its index.

## 8.1 Linear Search

Linear search checks elements one by one until the target is found or the array ends.

Example:

```text
Array: 10 25 30 45 50
Target: 30
Index: 2
```

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 25, 30, 45, 50};
    int n = 5;
    int target = 30;
    int index = -1;

    for (int i = 0; i < n; i++) {
        if (arr[i] == target) {
            index = i;
            break;
        }
    }

    cout << "Index: " << index << endl;

    return 0;
}
```

Output:

```text
Index: 2
```

If the target is not found, `index` remains `-1`.

**Complexity:**
- Best case: O(1)
- Worst case: O(n)
- Extra space: O(1)

Linear search works on both sorted and unsorted arrays.

## 8.2 Binary Search

Binary search repeatedly divides the search range in half.

**Important:** The array must be sorted for standard binary search to work correctly.

Example:

```text
Array: 10 20 30 40 50 60 70
Target: 50
```

Instead of checking every element, binary search examines the middle element and discards the half that cannot contain the target.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50, 60, 70};
    int n = 7;
    int target = 50;

    int left = 0;
    int right = n - 1;
    int index = -1;

    while (left <= right) {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target) {
            index = mid;
            break;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }

    cout << "Index: " << index << endl;

    return 0;
}
```

Output:

```text
Index: 4
```

### Complexity

- Best case: O(1)
- Worst case: O(log n)
- Extra space: O(1) for iterative binary search.

Binary search is much faster than linear search for large, sorted arrays.

---

# 🔃 9. Sorting Algorithms

Sorting means arranging elements in ascending or descending order.

Example:

```text
Before: 40 10 30 20 50
After:  10 20 30 40 50
```

## 9.1 Bubble Sort

Bubble sort compares adjacent elements and swaps them when they are in the wrong order.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {40, 10, 30, 20, 50};
    int n = 5;

    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

Output:

```text
10 20 30 40 50
```

Complexity:
- Average and worst case: O(n²)
- Best case: O(n) with an early-stop optimization.
- Extra space: O(1)

Bubble sort is useful for learning but is inefficient for large arrays.

## 9.2 Selection Sort

Selection sort repeatedly finds the smallest element in the unsorted portion and places it at the beginning of that portion.

Complexity:
- Best, average, and worst time: O(n²)
- Extra space: O(1)

## 9.3 Insertion Sort

Insertion sort takes one element at a time and inserts it into the correct position within the already-sorted portion.

Complexity:
- Best case: O(n) for an already-sorted array.
- Average and worst case: O(n²)
- Extra space: O(1)

## 9.4 Merge Sort

Merge sort divides the array into smaller parts, sorts those parts, and merges them into a sorted array.

Complexity:
- Best, average, and worst time: O(n log n)
- Extra space: Typically O(n) for an array implementation.

## 9.5 Quick Sort

Quick sort selects a pivot, partitions the elements around the pivot, and recursively sorts the resulting parts.

Complexity:
- Average time: O(n log n)
- Worst time: O(n²)
- Stack space depends on recursion depth.

### Which Sorting Algorithm Should You Learn First?

1. Bubble sort for understanding comparisons and swapping.
2. Selection sort for understanding minimum selection.
3. Insertion sort for understanding sorted and unsorted portions.
4. Merge sort and quick sort for efficient sorting algorithms.
5. `std::sort()` for practical C++ programming.

For normal C++ programs, you can use:

```cpp
#include <algorithm>
#include <iostream>
using namespace std;

int main() {
    int arr[] = {40, 10, 30, 20, 50};

    sort(arr, arr + 5);

    for (int x : arr) {
        cout << x << " ";
    }
}
```

Output:

```text
10 20 30 40 50
```

---

# 👉 10. Two Pointers Technique

The two-pointers technique uses two indices to solve a problem efficiently.

The pointers can move toward each other, move in the same direction, or track positions in different arrays.

## Example: Find a Pair with a Given Sum

Given a sorted array:

```text
Array: 1 2 4 6 8 9
Target sum: 10
```

Find two elements whose sum is 10.

The pair is `2 + 8 = 10`.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {1, 2, 4, 6, 8, 9};
    int n = 6;
    int target = 10;

    int left = 0;
    int right = n - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target) {
            cout << arr[left] << " + "
                 << arr[right] << " = " << target;
            return 0;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }

    cout << "Pair not found";

    return 0;
}
```

Output:

```text
2 + 8 = 10
```

### How Does It Work?

- If the sum is too small, move the left pointer right to increase the sum.
- If the sum is too large, move the right pointer left to decrease the sum.
- If the sum matches the target, the pair is found.

This logic depends on the array being sorted.

### Complexity

- Time: O(n)
- Extra space: O(1)

### Common Applications

- Reversing an array.
- Finding pairs with a target sum.
- Removing duplicates from sorted arrays.
- Checking palindromes.
- Merging sorted arrays.

---

# ➕ 11. Prefix Sum

A prefix sum stores cumulative sums of array elements.

It is useful when we need to calculate the sum of many ranges efficiently.

Consider:

```text
Array:       2 4 6 8 10
Prefix Sum:  2 6 12 20 30
```

Each prefix sum represents the sum of all elements from index `0` to that index.

## Formula

Using a zero-based prefix array:

`prefix[i] = prefix[i - 1] + arr[i]`

with the first element handled separately.

For range sum from index `L` to index `R`:

`sum(L, R) = prefix[R] - prefix[L - 1]`

when `L > 0`. If `L == 0`, the range sum is simply `prefix[R]`.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {2, 4, 6, 8, 10};
    int n = 5;

    int prefix[5];
    prefix[0] = arr[0];

    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] + arr[i];
    }

    int L = 1;
    int R = 3;

    int sum = prefix[R];

    if (L > 0) {
        sum -= prefix[L - 1];
    }

    cout << "Range sum: " << sum << endl;

    return 0;
}
```

Output:

```text
Range sum: 18
```

The selected range is `4 + 6 + 8 = 18`.

### Complexity

- Building prefix sums: O(n)
- Each range-sum query: O(1)
- Extra space: O(n)

**When should you use prefix sums?**

Use them when an array remains unchanged and you need to answer many range-sum queries.

---

# 🪟 12. Sliding Window

Sliding window is a technique for processing a continuous section of an array without repeatedly recalculating everything.

A window is a range of consecutive elements.

There are two common forms:

1. Fixed-size window.
2. Variable-size window.

## 12.1 Fixed-Size Sliding Window

### Problem

Find the maximum sum of any three consecutive elements.

```text
Array: 2 1 5 1 3 2
Window size: 3
```

Possible window sums:

```text
2 + 1 + 5 = 8
1 + 5 + 1 = 7
5 + 1 + 3 = 9
1 + 3 + 2 = 6
```

The maximum sum is 9.

### C++ Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {2, 1, 5, 1, 3, 2};
    int n = 6;
    int k = 3;

    int windowSum = 0;

    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }

    int maxSum = windowSum;

    for (int i = k; i < n; i++) {
        windowSum += arr[i];
        windowSum -= arr[i - k];

        if (windowSum > maxSum) {
            maxSum = windowSum;
        }
    }

    cout << "Maximum sum: " << maxSum;

    return 0;
}
```

Output:

```text
Maximum sum: 9
```

Instead of calculating each window from scratch, the algorithm adds the incoming element and removes the outgoing element.

### Complexity

- Time: O(n)
- Extra space: O(1)

## 12.2 Variable-Size Sliding Window

The window expands or shrinks based on a condition.

For example, with an array of positive numbers, find the shortest subarray whose sum is at least a target.

The algorithm generally:

1. Expands the window by moving the right pointer.
2. Adds the new element to the running sum.
3. Shrinks the window from the left while the condition is satisfied.
4. Records the best valid window.

**Important:** This simple approach relies on positive numbers. With negative numbers, the sum may not change predictably as the window expands or shrinks, so a different algorithm may be needed.

---

# 📦 13. Subarrays

A subarray is a **contiguous part of an array**.

Consider:

```text
Array: [1, 2, 3]
```

Its non-empty subarrays are:

```text
[1]
[2]
[3]
[1, 2]
[2, 3]
[1, 2, 3]
```

The elements must be adjacent in the original array.

For example, `[1, 3]` is not a subarray because the two elements are not adjacent.

A subsequence, in contrast, does not need to be contiguous.

## Number of Non-Empty Subarrays

For an array of size `n`, the total number of non-empty subarrays is:

`n × (n + 1) / 2`

For `n = 3`:

`3 × 4 / 2 = 6`

### Print All Subarrays

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {1, 2, 3};
    int n = 3;

    for (int start = 0; start < n; start++) {
        for (int end = start; end < n; end++) {
            for (int i = start; i <= end; i++) {
                cout << arr[i] << " ";
            }

            cout << endl;
        }
    }

    return 0;
}
```

This program prints each subarray on a separate line.

### Complexity

Printing all subarrays with every element displayed takes O(n³) time in the worst case, because there are O(n²) subarrays and each may contain O(n) elements.

Many optimized subarray algorithms reduce the time complexity by maintaining a running sum or using prefix sums.

---

# ⚡ 14. Kadane's Algorithm

Kadane's algorithm finds the maximum sum of a non-empty contiguous subarray.

It is one of the most important array algorithms for coding interviews.

### Example

```text
Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

The maximum-sum subarray is:

```text
[4, -1, 2, 1]
```

Its sum is:

`4 + (-1) + 2 + 1 = 6`

## Main Idea

At every position, decide whether to:

- Extend the previous subarray.
- Start a new subarray at the current element.

The recurrence is:

`current = max(arr[i], current + arr[i])`

Then update:

`best = max(best, current)`

### C++ Program

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int arr[] = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
    int n = 9;

    int current = arr[0];
    int best = arr[0];

    for (int i = 1; i < n; i++) {
        current = max(arr[i], current + arr[i]);
        best = max(best, current);
    }

    cout << "Maximum subarray sum: " << best;

    return 0;
}
```

Output:

```text
Maximum subarray sum: 6
```

### Why Initialize with the First Element?

This ensures that an array containing only negative values still returns its largest element rather than incorrectly returning zero.

### Complexity

- Time: O(n)
- Extra space: O(1)

**Common applications:** Maximum subarray sum, stock-profit variants, and related optimization problems.

---

# 🔎 15. Binary Search on Answer

Binary search on answer is an advanced technique used when the answer lies in a range and we can efficiently check whether a candidate answer is feasible.

Instead of searching for an element in an array, we search for the smallest or largest answer that satisfies a condition.

### Example: Minimum Capacity

Suppose we have packages with weights:

```text
Weights: [1, 2, 3, 4, 5]
```

We need to ship all packages in order within three days.

We want to find the minimum ship capacity that makes this possible.

A capacity that is too small requires too many days. Increasing the capacity cannot increase the number of days needed.

This gives us a monotonic condition.

## Main Idea

1. Choose the smallest possible capacity as the lower bound.
2. Choose a safe upper bound.
3. Calculate the middle capacity.
4. Check whether the packages can be shipped within three days.
5. If feasible, try a smaller capacity.
6. If infeasible, increase the capacity.
7. Continue until the minimum feasible capacity is found.

### C++ Example

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool canShip(const vector<int>& weights, int days, int capacity) {
    int usedDays = 1;
    int currentLoad = 0;

    for (int weight : weights) {
        if (currentLoad + weight > capacity) {
            usedDays++;
            currentLoad = 0;
        }

        currentLoad += weight;
    }

    return usedDays <= days;
}

int main() {
    vector<int> weights = {1, 2, 3, 4, 5};
    int days = 3;

    int left = *max_element(weights.begin(), weights.end());
    int right = 0;

    for (int weight : weights) {
        right += weight;
    }

    while (left < right) {
        int mid = left + (right - left) / 2;

        if (canShip(weights, days, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    cout << "Minimum capacity: " << left;

    return 0;
}
```

Output:

```text
Minimum capacity: 6
```

### Complexity

Let `n` be the number of packages and `S` be the sum of their weights.

- Feasibility check: O(n)
- Binary search iterations: O(log S)
- Total time: O(n log S)

### Common Applications

- Minimum ship capacity.
- Minimum maximum workload.
- Allocate books among students.
- Find the minimum possible maximum distance.
- Find the smallest feasible processing rate.

**Key requirement:** The answer space must have a monotonic feasibility condition, and the bounds must be valid.

---

# 📈 16. Monotonic Techniques

Monotonic techniques maintain elements in increasing or decreasing order to solve certain array problems efficiently.

A common example is a monotonic stack.

## 16.1 Next Greater Element

For each element, find the first element to its right that is greater than it.

Example:

```text
Array:       [4, 5, 2, 10]
Next greater: [5, 10, 10, -1]
```

The last element has no greater element to its right, so we use `-1`.

### C++ Program Using a Monotonic Stack

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

int main() {
    vector<int> arr = {4, 5, 2, 10};
    int n = arr.size();

    vector<int> answer(n, -1);
    stack<int> st;

    for (int i = n - 1; i >= 0; i--) {
        while (!st.empty() && st.top() <= arr[i]) {
            st.pop();
        }

        if (!st.empty()) {
            answer[i] = st.top();
        }

        st.push(arr[i]);
    }

    for (int x : answer) {
        cout << x << " ";
    }

    return 0;
}
```

Output:

```text
5 10 10 -1
```

### How Does It Work?

- Traverse the array from right to left.
- Remove stack elements that are less than or equal to the current element.
- If the stack is not empty, its top is the next greater element.
- Push the current element onto the stack.

Each element is pushed and popped at most once.

### Complexity

- Time: O(n)
- Extra space: O(n)

### Other Monotonic Problems

- Next smaller element.
- Previous greater element.
- Stock span.
- Daily temperatures.
- Largest rectangle in a histogram.
- Sliding window maximum using a monotonic deque.

---

# ⏱️ 17. Time and Space Complexity

Complexity analysis helps us understand how an algorithm performs as the input size increases.

## 17.1 Big O Notation

Big O describes an upper bound on how an algorithm's resource usage grows with input size.

Common complexities:

| Complexity | Name | Example |
|---|---|---|
| O(1) | Constant | Access an array element |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Traverse an array |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Basic bubble sort |
| O(n³) | Cubic | Naive subarray printing |

## 17.2 Time Complexity

Time complexity measures how the number of operations grows with input size.

Example:

```cpp
for (int i = 0; i < n; i++) {
    cout << i << " ";
}
```

The loop executes `n` times, so its time complexity is O(n).

## 17.3 Space Complexity

Space complexity measures the memory required by an algorithm. Auxiliary space refers specifically to the extra memory used beyond the input.

Example:

```cpp
int sum = 0;

for (int i = 0; i < n; i++) {
    sum += arr[i];
}
```

The algorithm uses only a constant amount of additional memory, so its auxiliary space is O(1).

If we create another array of size `n`, the additional space is O(n).

## 17.4 Complexity of Common Array Operations

| Operation | Typical complexity |
|---|---|
| Access by index | O(1) |
| Update by index | O(1) |
| Linear search | O(n) |
| Traverse | O(n) |
| Binary search on sorted data | O(log n) |
| Insert at beginning | O(n) |
| Delete at beginning | O(n) |
| Append to `vector` | O(1) amortized |
| Sort using `std::sort` | O(n log n) worst-case comparisons |

Complexity depends on the exact operation and data structure. For example, binary search requires sorted data, and a built-in array does not resize automatically.

---

# 🧩 18. Common Array Patterns

Many coding problems can be solved by recognizing a familiar pattern.

| Pattern | When to use it | Example problem |
|---|---|---|
| Traversal | Process every element | Find array sum |
| Two pointers | Work with two positions efficiently | Pair sum in sorted array |
| Prefix sum | Answer repeated range-sum queries | Sum from L to R |
| Sliding window | Process continuous ranges | Maximum sum of K elements |
| Binary search | Search sorted data | Find target index |
| Binary search on answer | Find minimum or maximum feasible value | Minimum shipping capacity |
| Kadane's algorithm | Maximum sum of a contiguous subarray | Maximum subarray |
| Sorting | Arrange data for easier processing | Sort numbers |
| Hashing | Count or quickly locate values | Two Sum |
| Monotonic stack | Find nearest greater or smaller values | Next Greater Element |
| Frequency counting | Count occurrences | Most frequent element |
| In-place modification | Reduce additional memory | Remove duplicates from a sorted array |

## How to Recognize a Pattern

- If the problem asks for a range sum many times, consider prefix sums.
- If it asks for a fixed-length continuous range, consider sliding window.
- If it asks for a pair in a sorted array, consider two pointers.
- If it asks for a maximum subarray sum, consider Kadane's algorithm.
- If the data is sorted and you need to find a value, consider binary search.
- If you need the minimum feasible capacity or maximum feasible rate, consider binary search on answer.
- If you need the next greater or smaller element, consider a monotonic stack.
- If you need fast lookups or frequency counts, consider a hash map or frequency array.

These are starting points, not rigid rules. Some problems require combining multiple patterns.

---

# 📝 19. Beginner-to-Advanced Practice Problems

Practice these problems in order. Try to solve each problem independently before looking at a solution.

## 🟢 Beginner Level

- [ ] Print all array elements.
- [ ] Find the sum of array elements.
- [ ] Find the minimum and maximum element.
- [ ] Count even and odd numbers.
- [ ] Reverse an array.
- [ ] Search for an element using linear search.
- [ ] Count the occurrences of a target element.
- [ ] Check whether an array is sorted.
- [ ] Find the second-largest distinct element.
- [ ] Calculate the average of array elements.

## 🟡 Intermediate Level

- [ ] Remove duplicates from a sorted array.
- [ ] Move all zeroes to the end.
- [ ] Rotate an array by K positions.
- [ ] Find a pair with a target sum.
- [ ] Merge two sorted arrays.
- [ ] Find the missing number in a sequence.
- [ ] Find the majority element.
- [ ] Build a prefix-sum array.
- [ ] Answer multiple range-sum queries.
- [ ] Find the maximum sum of K consecutive elements.
- [ ] Find the longest valid window for a target condition.
- [ ] Find the first and last occurrence of a target in a sorted array.

## 🔴 Advanced Level

- [ ] Maximum subarray sum using Kadane's algorithm.
- [ ] Product of array except self.
- [ ] Three Sum.
- [ ] Maximum product subarray.
- [ ] Trapping Rain Water.
- [ ] Subarray Sum Equals K.
- [ ] Search in a rotated sorted array.
- [ ] Find the minimum in a rotated sorted array.
- [ ] Find the median of two sorted arrays.
- [ ] Allocate books among students.
- [ ] Find minimum ship capacity within a deadline.
- [ ] Find the next greater element.
- [ ] Find the largest rectangle in a histogram.
- [ ] Find the maximum in every sliding window.

## Recommended Practice Platforms

- [LeetCode](https://leetcode.com/)
- [GeeksforGeeks](https://www.geeksforgeeks.org/)
- [HackerRank](https://www.hackerrank.com/)
- [Codeforces](https://codeforces.com/)

---

# 💻 20. How to Run C++ Programs

You need a C++ compiler, such as GCC through MinGW on Windows, or a compatible compiler on Linux or macOS.

## Step 1: Install a Compiler

Install GCC or another C++ compiler and ensure that it is available through your terminal.

## Step 2: Create a File

Create a file named:

```text
array_traversal.cpp
```

## Step 3: Write Your Program

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[] = {10, 20, 30, 40, 50};

    for (int i = 0; i < 5; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Step 4: Compile the Program

```bash
g++ array_traversal.cpp -o array_traversal
```

## Step 5: Run the Program

On Windows:

```bash
array_traversal.exe
```

On Linux or macOS:

```bash
./array_traversal
```

Output:

```text
10 20 30 40 50
```

You can also use the integrated terminal in Visual Studio Code after installing and configuring a C++ compiler.

---

# 🗺️ 21. Learning Roadmap

Follow this roadmap to build your array problem-solving skills step by step.

### Phase 1: Understand the Basics

Learn array declaration, initialization, indexing, traversal, insertion, deletion, and memory representation.

### Phase 2: Master Basic Problems

Practice finding minimum and maximum elements, reversing arrays, counting frequencies, and performing linear search.

### Phase 3: Learn Searching and Sorting

Understand binary search, bubble sort, selection sort, insertion sort, merge sort, and quick sort.

### Phase 4: Learn Problem-Solving Patterns

Practice two pointers, prefix sums, sliding windows, hashing, and subarray problems.

### Phase 5: Solve Advanced Problems

Study Kadane's algorithm, binary search on answer, monotonic stacks, and optimization techniques.

### Phase 6: Analyze Every Solution

For every problem, try to answer these questions:

1. What is the input and expected output?
2. What is the simplest solution?
3. Can I reduce the number of operations?
4. What is the time complexity?
5. What is the auxiliary space complexity?
6. Does my solution handle empty, small, negative, duplicate, or boundary values appropriately?

---

# 🎯 Final Goal

The goal of this repository is to develop a strong foundation in **Data Structures and Algorithms using C++**.

By completing the theory and practice problems, I aim to improve:

- Logical thinking and problem-solving skills.
- Understanding of arrays and memory.
- Knowledge of common DSA patterns.
- Ability to analyze time and space complexity.
- Preparation for coding interviews and competitive programming.

**Learn the concept → Understand the example → Write the code → Test edge cases → Analyze complexity → Solve more problems.**

Keep practicing, stay consistent, and improve one problem at a time! 🚀

---

## ⭐ Contributions and Feedback

Suggestions, corrections, and improvements are welcome. This repository is intended to be a continuously growing collection of C++ array theory and problem-solving solutions.
