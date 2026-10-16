# 🔍 Binary Search

## 📌 Introduction

Binary Search is an efficient searching algorithm used to find a specific element in a **sorted array or list**.

It works by repeatedly dividing the search range into two halves. Instead of checking every element one by one, Binary Search eliminates half of the remaining elements in each step.

## 🎯 Objectives

- Understand how the Binary Search algorithm works.
- Learn how to search for an element in a sorted array.
- Implement Binary Search using C++.
- Understand the time and space complexity of the algorithm.

## ⚙️ How Does Binary Search Work?

Binary Search follows these steps:

1. Start with the first and last positions of the sorted array.
2. Calculate the middle index.
3. Compare the middle element with the target element.
4. If both are equal, the element is found.
5. If the target is smaller, search the left half.
6. If the target is larger, search the right half.
7. Repeat until the element is found or the search range becomes empty.

**Important:** Binary Search requires the array to be sorted.

## 💡 Example

Consider the following sorted array:

```text
Array:  [10, 20, 30, 40, 50, 60, 70]
Target: 50
```

**Step 1:**

The middle element is `40`.

Since `50 > 40`, search the right half.

```text
[50, 60, 70]
```

**Step 2:**

The middle element of the remaining range is `60`.

Since `50 < 60`, search the left half.

**Step 3:**

The element `50` is found.

```text
Output: Element found at index 4
```

Remember that array indexing starts from `0` in C++.

## 💻 C++ Implementation

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int size, int target)
{
    int low = 0;
    int high = size - 1;

    while (low <= high)
    {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
        {
            return mid;
        }
        else if (arr[mid] < target)
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    return -1;
}

int main()
{
    int arr[] = {10, 20, 30, 40, 50, 60, 70};
    int size = sizeof(arr) / sizeof(arr[0]);
    int target = 50;

    int result = binarySearch(arr, size, target);

    if (result != -1)
    {
        cout << "Element found at index " << result << endl;
    }
    else
    {
        cout << "Element not found" << endl;
    }

    return 0;
}
```

## ▶️ Output

```text
Element found at index 4
```

## 📊 Time and Space Complexity

| Case | Complexity |
|---|---|
| Best Case | O(1) |
| Average Case | O(log n) |
| Worst Case | O(log n) |
| Space Complexity (iterative) | O(1) |

### Explanation

- **Best Case — O(1):** The target element is found at the middle during the first comparison.
- **Average Case — O(log n):** The search range is reduced by half repeatedly.
- **Worst Case — O(log n):** The algorithm continues dividing the range until the target is found or the range becomes empty.
- **Space Complexity — O(1):** The iterative implementation uses only a constant amount of extra memory.

## ⚖️ Binary Search vs Linear Search

| Feature | Binary Search | Linear Search |
|---|---|---|
| Data requirement | Sorted data | Sorted or unsorted data |
| Searching method | Divides the range into halves | Checks elements one by one |
| Worst-case time | O(log n) | O(n) |
| Efficiency on large sorted arrays | High | Lower |

## ✅ Advantages

- Fast and efficient for large sorted arrays.
- Requires fewer comparisons than Linear Search in many cases.
- Uses constant extra space in its iterative implementation.
- Easy to implement and understand.

## ❌ Limitations

- The data must be sorted before searching.
- Maintaining sorted data can require additional work.
- It is not always suitable for data structures that do not support efficient middle-element access, such as a standard linked list.

## 🌍 Real-World Applications

Binary Search is useful in:

- Finding a word in a sorted dictionary.
- Searching for a student record by a sorted roll number.
- Finding an element in a sorted database index.
- Searching for a value in a sorted array.
- Solving problems that use binary search on a range of possible answers.

## 🛠️ Requirements

- C++ compiler (GCC, MinGW, or another compatible compiler).
- Visual Studio Code, Code::Blocks, or any C++ IDE.
- Basic knowledge of arrays, loops, and conditional statements.

## 🚀 How to Run the Program

1. Copy the C++ code into a file named `binary_search.cpp`.
2. Open a terminal in the folder containing the file.
3. Compile the program:

   ```bash
   g++ binary_search.cpp -o binary_search
   ```

4. Run the program:

   ```bash
   ./binary_search
   ```

   On Windows, you can run:

   ```bash
   .\binary_search.exe
   ```

## 📚 Key Takeaways

- Binary Search works on sorted data.
- It repeatedly divides the search range into two halves.
- Its worst-case time complexity is O(log n).
- The iterative implementation uses O(1) extra space.
- It is an important searching technique in Data Structures and Algorithms (DSA).

---

**Happy Coding! 💻**

If you are learning Data Structures and Algorithms, practice implementing Binary Search with different arrays and target values to strengthen your understanding.
