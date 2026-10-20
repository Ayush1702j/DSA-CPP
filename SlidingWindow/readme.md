# Sliding Window in DSA — Complete C++ Notes

A detailed beginner-to-intermediate guide to the Sliding Window technique, with C++ code examples.

## 1. What is Sliding Window?

Sliding Window is an algorithmic technique for processing a **contiguous range** of an array or string (a subarray or substring).

Instead of recalculating every range from scratch, maintain a window and update its information as it moves.

For example, in `[2, 1, 5, 1, 3, 2]`, the windows of length 3 are:
- `[2, 1, 5]`, sum 8
- `[1, 5, 1]`, sum 7
- `[5, 1, 3]`, sum 9
- `[1, 3, 2]`, sum 6

When a fixed-size window slides, remove the outgoing element and add the incoming element:

`newSum = oldSum - outgoing + incoming`

This can reduce a brute-force `O(n*k)` solution to `O(n)`.

## 2. Vocabulary

- **Array:** ordered collection of values.
- **Subarray:** a contiguous part of an array.
- **Substring:** a contiguous part of a string.
- **Window:** the current range being processed.
- **left:** start index of the window.
- **right:** end index of the window.
- **Fixed window:** window size stays equal to `k`.
- **Variable window:** window grows or shrinks according to a condition.

Sliding Window is normally for contiguous ranges. If a question allows selecting elements from anywhere, not necessarily consecutive, it may require another technique.

## 3. How to recognize it

Sliding Window may be suitable when a problem asks for:
- maximum/minimum sum of `k` consecutive elements
- average of every window of length `k`
- longest or shortest subarray satisfying a condition
- longest substring with a property
- maximum vowels/characters in a fixed-length substring

Ask:
1. Is the required range contiguous?
2. Can the answer be updated when an element enters or leaves?
3. Is the window length fixed or controlled by a condition?

## 4. Type A — Fixed-size Sliding Window

Use when `k` is provided.

### Example: Maximum sum of k consecutive elements

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

long long maxSumSubarray(const vector<int>& arr, int k) {
    int n = arr.size();

    if (k <= 0 || k > n) return -1;

    // Build the first window
    long long windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }

    long long best = windowSum;

    // Slide: remove old left element, add new right element
    for (int right = k; right < n; right++) {
        windowSum -= arr[right - k];
        windowSum += arr[right];
        best = max(best, windowSum);
    }

    return best;
}

int main() {
    vector<int> arr = {2, 1, 5, 1, 3, 2};
    cout << maxSumSubarray(arr, 3) << endl; // 9
}
```

**Complexity:** Time `O(n)`, extra space `O(1)`.

### Fixed-window template

```cpp
// First calculate the initial window
// Then, for each new right index:
windowSum -= arr[right - k]; // outgoing
windowSum += arr[right];     // incoming
updateAnswer(windowSum);
```

## 5. Type B — Variable-size Sliding Window

Use when the length is not given. Usually:
- `right` expands the window.
- Update sum, count, or frequency data.
- While the window is invalid, remove the leftmost element and increment `left`.
- Update the best answer when the window is valid.

### Example: Minimum length subarray with sum >= target

For positive/non-negative values:
`arr = [2, 3, 1, 2, 4, 3]`, target `7`.
The shortest valid subarray is `[4, 3]`, length 2.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

int minSubarrayLength(int target, const vector<int>& arr) {
    int left = 0;
    int sum = 0;
    int best = INT_MAX;

    for (int right = 0; right < (int)arr.size(); right++) {
        sum += arr[right]; // expand

        while (sum >= target) {
            best = min(best, right - left + 1);
            sum -= arr[left]; // shrink
            left++;
        }
    }

    return best == INT_MAX ? 0 : best;
}

int main() {
    vector<int> arr = {2, 3, 1, 2, 4, 3};
    cout << minSubarrayLength(7, arr) << endl; // 2
}
```

**Complexity:** Time `O(n)`, extra space `O(1)`.

**Limitation:** This sum-based pattern requires non-negative (commonly positive) array values. Negative numbers can make the sum decrease when expanding, so the ordinary sliding-window logic may not work.

## 6. Example: Longest substring without repeating characters

For `"abcabcbb"`, the answer is 3 (`"abc"`).

Keep a set of characters in the current window. When a repeated character appears, shrink from the left until it is no longer repeated.

```cpp
#include <iostream>
#include <string>
#include <unordered_set>
#include <algorithm>
using namespace std;

int longestUniqueSubstring(const string& s) {
    int left = 0;
    int best = 0;
    unordered_set<char> seen;

    for (int right = 0; right < (int)s.size(); right++) {
        while (seen.count(s[right])) {
            seen.erase(s[left]);
            left++;
        }

        seen.insert(s[right]);
        best = max(best, right - left + 1);
    }

    return best;
}

int main() {
    cout << longestUniqueSubstring("abcabcbb") << endl; // 3
}
```

**Complexity:** Average time `O(n)`, extra space up to `O(min(n, character_set_size))`.

## 7. Example: Maximum vowels in any substring of length k

Count vowels in the first window, then slide by removing the outgoing character and adding the incoming character.

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

bool isVowel(char c) {
    c = tolower(c);
    return c == 'a' || c == 'e' || c == 'i' ||
           c == 'o' || c == 'u';
}

int maxVowels(string s, int k) {
    int n = s.size();
    if (k <= 0 || k > n) return 0;

    int count = 0;
    for (int i = 0; i < k; i++) {
        if (isVowel(s[i])) count++;
    }

    int best = count;

    for (int right = k; right < n; right++) {
        if (isVowel(s[right - k])) count--;
        if (isVowel(s[right])) count++;
        best = max(best, count);
    }

    return best;
}

int main() {
    cout << maxVowels("abciiidef", 3) << endl; // 3
}
```

**Complexity:** Time `O(n)`, extra space `O(1)`.

## 8. Fixed vs Variable Window

| | Fixed-size | Variable-size |
|---|---|---|
| Length | Known `k` | Changes |
| Movement | One step at a time | Expand and shrink |
| Common answer | Maximum sum / average | Longest / shortest valid range |
| Example | Max sum of 3 consecutive numbers | Smallest sum-at-least-target range |

## 9. Brute Force vs Sliding Window

For an array of length `n` and fixed window length `k`:

- **Brute force:** calculate each window sum independently: about `O(n*k)`.
- **Sliding Window:** calculate first sum once, then update: `O(n)`.

Example: if `n = 100,000` and `k = 500`, brute force may perform about 50 million additions, while the sliding-window update performs around 100,000 steps.

## 10. How to solve a new problem

1. Confirm the range is contiguous.
2. Decide fixed or variable window.
3. Choose `left` and `right` pointers.
4. Track the required state: sum, frequency map, set, or count.
5. Add the new right element.
6. For fixed windows, remove the outgoing element.
7. For variable windows, shrink while the condition says to shrink.
8. Update the answer.
9. Test edge cases: empty input, `k = 1`, `k = n`, repeated values, and no valid range.

## 11. Common mistakes

- Recalculating each window sum from scratch.
- Forgetting to remove the outgoing element.
- Using `if` instead of `while` when a variable window needs multiple shrinks.
- Confusing subarray with subsequence.
- Using a positive-number sum pattern on arrays containing negative numbers.
- Off-by-one window length: `right - left + 1`.
- Not handling invalid `k` or no valid window.

## 12. Practice problems

Try in this order:

### Easy
1. Maximum sum of `k` consecutive elements.
2. Average of every window of length `k`.
3. Maximum vowels in a substring of length `k`.

### Medium
4. Minimum length subarray with sum at least target (positive values).
5. Longest substring without repeating characters.
6. Longest subarray with at most two distinct values.

### Advanced
7. Minimum Window Substring.
8. Longest Repeating Character Replacement.
9. Count subarrays with exactly `k` distinct values (often use `atMost(k) - atMost(k-1)`).

## 13. Quick revision

- Sliding Window handles contiguous ranges.
- Fixed window: initialize, then subtract outgoing and add incoming.
- Variable window: expand with `right`; shrink with `left`.
- Window length: `right - left + 1`.
- Many solutions are `O(n)` because each pointer moves forward at most `n` times.
- Check input constraints carefully, especially negative values in sum problems.

## 14. A single C++ file with all examples

The examples above are standalone programs, each with its own `main()`. Do not paste all of them into one file at once because a C++ program can only have one `main()` function. Keep each example in a separate file, or copy only the desired function into your own program.

**Recommended study order:** maximum sum of fixed-size window → minimum sum-at-least-target window → longest unique substring.
