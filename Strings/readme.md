# Strings in C++ — Complete Beginner's Guide

A complete guide to Strings in C++ and Data Structures & Algorithms (DSA), covering basic concepts, important operations, algorithms, and coding interview questions.

## Table of Contents

1. [Introduction to Strings](#1-introduction-to-strings)
2. [What Is a String?](#2-what-is-a-string)
3. [Declaring and Initializing Strings](#3-declaring-and-initializing-strings)
4. [Character vs String](#4-character-vs-string)
5. [String Memory and Indexing](#5-string-memory-and-indexing)
6. [String Input and Output](#6-string-input-and-output)
7. [String Length and Access](#7-string-length-and-access)
8. [Modifying Strings](#8-modifying-strings)
9. [Important String Operations](#9-important-string-operations)
10. [ASCII Values](#10-ascii-values)
11. [String Traversal](#11-string-traversal)
12. [String Comparison](#12-string-comparison)
13. [String Reversal](#13-string-reversal)
14. [Palindrome Strings](#14-palindrome-strings)
15. [Frequency Counting](#15-frequency-counting)
16. [Anagrams](#16-anagrams)
17. [Substrings and Subsequences](#17-substrings-and-subsequences)
18. [Two-Pointer Technique](#18-two-pointer-technique)
19. [Sliding Window Technique](#19-sliding-window-technique)
20. [String Searching Algorithms](#20-string-searching-algorithms)
21. [String Sorting](#21-string-sorting)
22. [Important STL Functions](#22-important-stl-functions)
23. [Time Complexity](#23-time-complexity)
24. [Common Coding Interview Questions](#24-common-coding-interview-questions)
25. [Practice Problems](#25-practice-problems)
26. [Common Mistakes](#26-common-mistakes)
27. [Quick Revision](#27-quick-revision)

---

## 1. Introduction to Strings

A string is a sequence of characters used to represent text.

Examples:

```text
Hello
Harshal
Computer Science
```

Strings are useful for storing names, processing text, searching words, validating passwords, and solving DSA problems.

[Back to Table of Contents](#table-of-contents)

---

## 2. What Is a String?

In C++, a string is commonly represented using the `string` class.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name = "Harshal";

    cout << name;

    return 0;
}
```

Output:

```text
Harshal
```

A string can contain letters, numbers, spaces, and special characters.

[Back to Table of Contents](#table-of-contents)

---

## 3. Declaring and Initializing Strings

```cpp
string s1 = "Hello";
string s2 = "";
string s3(5, 'A');
```

Output of `s3`:

```text
AAAAA
```

You can also declare an empty string and assign a value later.

```cpp
string s;

s = "Welcome";
```

[Back to Table of Contents](#table-of-contents)

---

## 4. Character vs String

| Character | String |
|---|---|
| One character | Sequence of characters |
| Uses single quotes | Uses double quotes |
| `char ch = 'A';` | `string s = "Apple";` |

[Back to Table of Contents](#table-of-contents)

---

## 5. String Memory and Indexing

Consider:

```cpp
string s = "CODE";
```

| Index | Character |
|---|---|
| 0 | C |
| 1 | O |
| 2 | D |
| 3 | E |

Access a character:

```cpp
cout << s[0];
```

Output:

```text
C
```

The last valid index is:

```cpp
s.length() - 1
```

Remember that string indexing starts from zero.

[Back to Table of Contents](#table-of-contents)

---

## 6. String Input and Output

Using `cin`:

```cpp
string name;

cin >> name;
```

`cin` stops at whitespace.

Using `getline()`:

```cpp
string name;

getline(cin, name);
```

`getline()` reads a complete line, including spaces.

[Back to Table of Contents](#table-of-contents)

---

## 7. String Length and Access

```cpp
string s = "Hello";

cout << s.length();
cout << s.size();
```

Both return:

```text
5
```

Access characters using:

```cpp
s[0]
s[1]
s.at(2)
```

`at()` performs bounds checking and throws an exception if the index is out of range.

[Back to Table of Contents](#table-of-contents)

---

## 8. Modifying Strings

Change a character:

```cpp
string s = "Hello";

s[0] = 'Y';
```

Add a character:

```cpp
s.push_back('!');
```

Remove the last character:

```cpp
s.pop_back();
```

Do not call `pop_back()` on an empty string.

[Back to Table of Contents](#table-of-contents)

---

## 9. Important String Operations

### Concatenation

```cpp
string a = "Hello";
string b = "World";

string c = a + " " + b;
```

### Substring

```cpp
string s = "Programming";

cout << s.substr(0, 4);
```

Output: `Prog`

### Search

```cpp
string s = "Hello World";

cout << s.find("World");
```

Output: `6`

If the pattern is not found, `find()` returns `string::npos`.

### Erase

```cpp
string s = "Hello World";

s.erase(5, 6);
```

Output: `Hello`

### Insert

```cpp
string s = "HelloWorld";

s.insert(5, " ");
```

Output: `Hello World`

### Replace

```cpp
string s = "Hello World";

s.replace(6, 5, "C++");
```

Output: `Hello C++`

[Back to Table of Contents](#table-of-contents)

---

## 10. ASCII Values

ASCII assigns numerical values to characters.

| Character | ASCII |
|---|---:|
| A | 65 |
| Z | 90 |
| a | 97 |
| z | 122 |
| 0 | 48 |
| 9 | 57 |

Example:

```cpp
char ch = 'A';

cout << int(ch);
```

Output: `65`

Use `toupper()` and `tolower()` from `<cctype>` for character case conversion.

[Back to Table of Contents](#table-of-contents)

---

## 11. String Traversal

Traversal means visiting every character.

```cpp
string s = "Hello";

for (int i = 0; i < s.length(); i++) {
    cout << s[i] << " ";
}
```

Output:

```text
H e l l o
```

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 12. String Comparison

```cpp
string a = "Apple";
string b = "Banana";

if (a < b) {
    cout << "Apple comes first";
}
```

C++ compares strings lexicographically.

Uppercase and lowercase letters are different:

```cpp
"Apple" != "apple"
```

[Back to Table of Contents](#table-of-contents)

---

## 13. String Reversal

Example:

```text
Original: Hello
Reversed: olleH
```

Using `reverse()`:

```cpp
#include <algorithm>

string s = "Hello";

reverse(s.begin(), s.end());
```

Using two pointers:

```cpp
int left = 0;
int right = s.length() - 1;

while (left < right) {
    swap(s[left], s[right]);

    left++;
    right--;
}
```

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 14. Palindrome Strings

A palindrome reads the same forward and backward.

Examples:

```text
madam
level
racecar
```

Code:

```cpp
bool isPalindrome(string s) {
    int left = 0;
    int right = s.length() - 1;

    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}
```

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 15. Frequency Counting

Frequency means counting how many times each character appears.

Example:

```text
String: banana
```

| Character | Frequency |
|---|---:|
| a | 3 |
| b | 1 |
| n | 2 |

For lowercase English letters:

```cpp
int freq[26] = {0};

for (char ch : s) {
    freq[ch - 'a']++;
}
```

This indexing method assumes every character is between `a` and `z`.

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 16. Anagrams

Two strings are anagrams if they contain the same characters with the same frequencies.

Example:

```text
listen
silent
```

Method using sorting:

```cpp
sort(a.begin(), a.end());
sort(b.begin(), b.end());

bool result = (a == b);
```

Time complexity: O(n log n)

A frequency-counting solution can achieve O(n) time for a fixed character set.

[Back to Table of Contents](#table-of-contents)

---

## 17. Substrings and Subsequences

### Substring

A substring contains continuous characters.

Example:

```text
String: abcde
Substring: bcd
```

### Subsequence

A subsequence preserves the relative order of characters but does not require them to be continuous.

Example:

```text
String: abcde
Subsequence: ace
```

Number of non-empty substrings of a string of length `n`:

\[
\frac{n(n+1)}{2}
\]

[Back to Table of Contents](#table-of-contents)

---

## 18. Two-Pointer Technique

Two pointers are useful for:

- Reversing a string
- Checking palindromes
- Comparing characters from both ends

Example:

```cpp
int left = 0;
int right = s.length() - 1;

while (left < right) {
    // Process s[left] and s[right]

    left++;
    right--;
}
```

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 19. Sliding Window Technique

Sliding window processes a continuous part of a string.

Useful for:

- Longest substring without repeating characters
- Longest substring with at most K distinct characters
- Minimum window substring

The window is expanded or contracted to satisfy a condition.

Time complexity of many optimized sliding-window solutions: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 20. String Searching Algorithms

### Naive Search

Checks the pattern at every possible position.

Worst-case time complexity: O(n × m)

### KMP Algorithm

KMP uses the LPS (Longest Proper Prefix which is also a Suffix) array to avoid repeated comparisons.

Time complexity: O(n + m)

[Back to Table of Contents](#table-of-contents)

---

## 21. String Sorting

```cpp
#include <algorithm>

string s = "dcba";

sort(s.begin(), s.end());

cout << s;
```

Output:

```text
abcd
```

Time complexity: O(n log n)

[Back to Table of Contents](#table-of-contents)

---

## 22. Important STL Functions

| Function | Purpose |
|---|---|
| `length()` | Get string length |
| `empty()` | Check if string is empty |
| `push_back()` | Add character |
| `pop_back()` | Remove last character |
| `substr()` | Extract substring |
| `find()` | Search text |
| `erase()` | Remove characters |
| `insert()` | Insert text |
| `replace()` | Replace text |
| `reverse()` | Reverse characters |
| `sort()` | Sort characters |

[Back to Table of Contents](#table-of-contents)

---

## 23. Time Complexity

| Operation | Complexity |
|---|---|
| Character access | O(1) |
| String traversal | O(n) |
| Reversal | O(n) |
| Palindrome check | O(n) |
| Frequency counting | O(n) |
| Anagram using sorting | O(n log n) |
| KMP searching | O(n + m) |

[Back to Table of Contents](#table-of-contents)

---

## 24. Common Coding Interview Questions

1. Reverse a string.
2. Check whether a string is a palindrome.
3. Count vowels and consonants.
4. Check whether two strings are anagrams.
5. Find the first non-repeating character.
6. Remove duplicate characters.
7. Find the longest word in a sentence.
8. Find all occurrences of a pattern.
9. Find the longest common prefix.
10. Find the longest substring without repeating characters.

[Back to Table of Contents](#table-of-contents)

---

## 25. Practice Problems

### Beginner

- Print each character of a string.
- Find string length without using `length()`.
- Count vowels.
- Reverse a string.
- Check palindrome.
- Count spaces and digits.

### Intermediate

- Check anagrams.
- Find the first repeating character.
- Remove duplicates.
- Find the longest word.
- Find all occurrences of a pattern.

### Advanced

- Longest palindromic substring.
- Minimum window substring.
- Implement KMP.
- Edit distance.
- Longest common subsequence.

[Back to Table of Contents](#table-of-contents)

---

## 26. Common Mistakes

- Using `i <= s.length()` instead of `i < s.length()`.
- Confusing single quotes and double quotes.
- Using `cin` for a sentence with spaces.
- Forgetting case sensitivity.
- Using `freq[ch - 'a']` for arbitrary characters.
- Calling `pop_back()` on an empty string.
- Accessing an invalid index.

[Back to Table of Contents](#table-of-contents)

---

## 27. Quick Revision

- A string is a sequence of characters.
- Indexing starts at zero.
- Last valid index = `length() - 1`.
- Use `getline()` for complete sentences.
- Use `substr()` to extract text.
- Use `find()` to search.
- Use two pointers for reversal and palindrome checking.
- Use frequency counting for anagrams and duplicates.
- Use sliding window for substring problems.
- Use KMP for efficient pattern searching.

[Back to Table of Contents](#table-of-contents)
