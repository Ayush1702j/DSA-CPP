# Strings in C++ — Complete Beginner's Guide

A complete guide to understanding strings, solving string-based problems, and preparing for coding interviews.

## Table of Contents

1. Introduction to Strings
2. What Is a String?
3. Declaring and Initializing Strings
4. Character vs String
5. How Strings Are Stored in Memory
6. String Input and Output
7. String Length and Access
8. Modifying Strings
9. Important String Operations
10. ASCII Values
11. String Traversal
12. String Comparison
13. String Reversal
14. Palindrome Strings
15. Frequency Counting
16. Anagrams
17. Substrings and Subsequences
18. Two-Pointer Technique
19. Sliding Window Technique
20. String Searching Algorithms
21. String Sorting
22. Important STL Functions
23. Time Complexity
24. Common Coding Interview Questions
25. Practice Problems
26. Common Mistakes
27. Quick Revision

---

# 1. Introduction to Strings

A string is a sequence of characters used to represent text.

Examples:

```text
"Hello"
"Harshal"
"Computer Science"
"12345"
```

Strings are used in almost every programming application:

- Storing names and addresses
- Searching for words in a document
- Checking passwords
- Processing text
- Detecting palindromes
- Searching for patterns
- Validating email addresses

In Data Structures and Algorithms (DSA), string problems often involve searching, comparing, modifying, or rearranging characters.

---

# 2. What Is a String?

In C++, a string can be represented using the `string` class from the Standard Template Library (STL).

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

Here:

- `string` is the data type.
- `name` is the variable.
- `"Harshal"` is the string value.

A string can contain letters, numbers, spaces, and special characters.

```cpp
string a = "Hello";
string b = "12345";
string c = "Hello World!";
```

**Important:** A string containing digits, such as `"12345"`, is text. It is not automatically treated as an integer.

---

# 3. Declaring and Initializing Strings

There are several ways to create a string.

## Method 1: Direct initialization

```cpp
string s = "Hello";
```

## Method 2: Empty string

```cpp
string s = "";
```

An empty string contains zero characters.

```cpp
cout << s.length();
```

Output:

```text
0
```

## Method 3: Assign later

```cpp
string s;

s = "Welcome";
```

## Method 4: Using a constructor

```cpp
string s(5, 'A');

cout << s;
```

Output:

```text
AAAAA
```

This creates a string containing five `A` characters.

---

# 4. Character vs String

A character and a string are different.

| Character | String |
|---|---|
| Represents one character | Represents zero or more characters |
| Uses single quotes | Uses double quotes |
| Data type: `char` | Data type: `string` |
| Example: `'A'` | Example: `"Apple"` |

Example:

```cpp
char ch = 'A';

string s = "Apple";
```

Incorrect:

```cpp
char ch = "A";
```

Correct:

```cpp
char ch = 'A';
```

---

# 5. How Strings Are Stored in Memory

Consider:

```cpp
string s = "CODE";
```

Conceptually, the characters are stored in sequence:

| Index | Character |
|---|---|
| 0 | C |
| 1 | O |
| 2 | D |
| 3 | E |

The first character is at index `0`, not index `1`.

```cpp
cout << s[0];
```

Output:

```text
C
```

```cpp
cout << s[3];
```

Output:

```text
E
```

The last character is at index:

```cpp
s.length() - 1
```

For `"CODE"`:

```cpp
4 - 1 = 3
```

Therefore, the last valid index is `3`.

**Important:** Accessing a string using an invalid index can cause undefined behavior. Always check the string length before accessing an index.

---

# 6. String Input and Output

## Using cin

```cpp
string name;

cin >> name;

cout << name;
```

Input:

```text
Harshal Nimje
```

Output:

```text
Harshal
```

`cin` normally stops reading at whitespace.

## Using getline

```cpp
string name;

getline(cin, name);

cout << name;
```

Input:

```text
Harshal Nimje
```

Output:

```text
Harshal Nimje
```

`getline()` reads the entire line, including spaces.

## Common getline mistake

```cpp
int age;
string name;

cin >> age;
getline(cin, name);
```

The newline remaining after entering the age may be consumed by `getline()`.

Correct:

```cpp
int age;
string name;

cin >> age;
cin.ignore();
getline(cin, name);
```

For more robust input handling:

```cpp
#include <limits>

cin >> age;

cin.ignore(numeric_limits<streamsize>::max(), '\n');

getline(cin, name);
```

---

# 7. String Length and Character Access

## length()

Returns the number of characters.

```cpp
string s = "Hello";

cout << s.length();
```

Output:

```text
5
```

`size()` also returns the number of characters.

```cpp
cout << s.size();
```

## Accessing characters

```cpp
string s = "Hello";

cout << s[0] << endl;
cout << s[1] << endl;
cout << s[4] << endl;
```

Output:

```text
H
e
o
```

## Using at()

```cpp
string s = "Hello";

cout << s.at(1);
```

Output:

```text
e
```

Unlike `operator[]`, `at()` checks whether the index is valid and throws an exception if it is out of range.

---

# 8. Modifying Strings

Strings can be modified after declaration.

## Changing a character

```cpp
string s = "Hello";

s[0] = 'Y';

cout << s;
```

Output:

```text
Yello
```

## Adding a character

```cpp
string s = "Hell";

s.push_back('o');

cout << s;
```

Output:

```text
Hello
```

## Removing the last character

```cpp
string s = "Hello";

s.pop_back();

cout << s;
```

Output:

```text
Hell
```

**Note:** Do not call `pop_back()` on an empty string.

---

# 9. Important String Operations

## 9.1 Concatenation

Combining two strings is called concatenation.

```cpp
string a = "Hello";
string b = "World";

string c = a + " " + b;

cout << c;
```

Output:

```text
Hello World
```

Using `+=`:

```cpp
string s = "Hello";

s += " World";
```

## 9.2 append()

```cpp
string s = "Hello";

s.append(" World");

cout << s;
```

Output:

```text
Hello World
```

## 9.3 substr()

Extracts a substring from a string.

Syntax:

```cpp
s.substr(start, length);
```

Example:

```cpp
string s = "Programming";

cout << s.substr(0, 4);
```

Output:

```text
Prog
```

Another example:

```cpp
string s = "Programming";

cout << s.substr(3);
```

Output:

```text
gramming
```

If the length is omitted, the substring continues until the end.

## 9.4 find()

Searches for a character or substring.

```cpp
string s = "Hello World";

cout << s.find("World");
```

Output:

```text
6
```

If the searched text is not found, `find()` returns `string::npos`.

```cpp
if (s.find("Python") == string::npos) {
    cout << "Not found";
}
```

Output:

```text
Not found
```

## 9.5 erase()

Removes characters from a string.

```cpp
string s = "Hello World";

s.erase(5, 6);

cout << s;
```

Output:

```text
Hello
```

Here:

- Starting index: `5`
- Number of characters removed: `6`

## 9.6 insert()

Inserts text at a specified index.

```cpp
string s = "HelloWorld";

s.insert(5, " ");

cout << s;
```

Output:

```text
Hello World
```

## 9.7 replace()

Replaces a section of a string.

```cpp
string s = "Hello World";

s.replace(6, 5, "C++");

cout << s;
```

Output:

```text
Hello C++
```

---

# 10. ASCII Values

ASCII assigns numerical values to common characters.

For example:

| Character | ASCII value |
|---|---:|
| A | 65 |
| B | 66 |
| Z | 90 |
| a | 97 |
| b | 98 |
| z | 122 |
| 0 | 48 |
| 9 | 57 |

Example:

```cpp
char ch = 'A';

cout << int(ch);
```

Output:

```text
65
```

Converting a lowercase letter to uppercase:

```cpp
char ch = 'a';

ch = ch - 32;

cout << ch;
```

Output:

```text
A
```

A safer and clearer method is:

```cpp
#include <cctype>

char ch = 'a';

ch = toupper(static_cast<unsigned char>(ch));
```

For actual text processing, prefer `toupper()` and `tolower()` instead of relying on ASCII arithmetic.

---

# 11. String Traversal

Traversal means visiting every character of a string.

## Using a for loop

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

Space complexity: O(1)

## Using a range-based loop

```cpp
string s = "Hello";

for (char ch : s) {
    cout << ch << " ";
}
```

This is useful when you do not need the character index.

## When to use indexed traversal?

Use indexed traversal when:

- You need the current index.
- You need to compare neighboring characters.
- You need to modify characters at specific positions.
- You are using a two-pointer technique.

---

# 12. String Comparison

Strings can be compared using comparison operators.

```cpp
string a = "Apple";
string b = "Banana";

if (a < b) {
    cout << "Apple comes first";
}
```

Output:

```text
Apple comes first
```

C++ compares strings lexicographically, based on character values.

Important:

```cpp
"apple" != "Apple"
```

Uppercase and lowercase letters are different.

For case-insensitive comparison, convert both strings to the same case first.

---

# 13. String Reversal

Reversing a string means changing the order of its characters.

Example:

```text
Original:  Hello
Reversed:  olleH
```

## Method 1: Using reverse()

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s = "Hello";

    reverse(s.begin(), s.end());

    cout << s;

    return 0;
}
```

Output:

```text
olleH
```

Time complexity: O(n)

## Method 2: Using two pointers

```cpp
string s = "Hello";

int left = 0;
int right = s.length() - 1;

while (left < right) {
    swap(s[left], s[right]);

    left++;
    right--;
}

cout << s;
```

The left pointer moves forward, while the right pointer moves backward.

Time complexity: O(n)

Extra space complexity: O(1)

---

# 14. Palindrome Strings

A palindrome reads the same forward and backward.

Examples:

```text
madam
level
racecar
```

Non-examples:

```text
hello
apple
```

## Palindrome checking using two pointers

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "madam";

    int left = 0;
    int right = s.length() - 1;

    bool palindrome = true;

    while (left < right) {
        if (s[left] != s[right]) {
            palindrome = false;
            break;
        }

        left++;
        right--;
    }

    if (palindrome)
        cout << "Palindrome";
    else
        cout << "Not palindrome";

    return 0;
}
```

Output:

```text
Palindrome
```

Time complexity: O(n)

Extra space complexity: O(1)

## Case-insensitive palindrome

For example:

```text
Madam
```

This is a palindrome if uppercase and lowercase letters are treated as equivalent.

To support that, convert the string to lowercase before checking.

If spaces and punctuation should be ignored, first remove them or skip them during traversal.

For example:

```text
A man, a plan, a canal: Panama
```

This is a palindrome after ignoring spaces, punctuation, and case.

---

# 15. Frequency Counting

Frequency means counting how many times each character appears.

Example:

```text
String: banana
```

| Character | Frequency |
|---|---:|
| b | 1 |
| a | 3 |
| n | 2 |

## Using an array for lowercase letters

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "banana";

    int freq[26] = {0};

    for (char ch : s) {
        freq[ch - 'a']++;
    }

    for (int i = 0; i < 26; i++) {
        if (freq[i] > 0) {
            cout << char('a' + i)
                 << " : " << freq[i] << endl;
        }
    }

    return 0;
}
```

Output:

```text
a : 3
b : 1
n : 2
```

This approach works when all characters are lowercase English letters.

For uppercase letters, digits, punctuation, or other characters, use a map or an appropriately sized character-frequency structure.

---

# 16. Anagrams

Two strings are anagrams if they contain the same characters with the same frequencies, but possibly in a different order.

Examples:

```text
listen
silent
```

These are anagrams.

```text
hello
world
```

These are not anagrams.

## Method 1: Sorting

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

bool isAnagram(string a, string b) {
    if (a.length() != b.length()) {
        return false;
    }

    sort(a.begin(), a.end());
    sort(b.begin(), b.end());

    return a == b;
}

int main() {
    cout << isAnagram("listen", "silent");
}
```

Output:

```text
1
```

Time complexity: O(n log n)

## Method 2: Frequency counting

For lowercase English letters, count the frequencies in the first string and subtract the frequencies in the second.

Time complexity: O(n)

Extra space complexity: O(1), because the frequency array has 26 entries.

---

# 17. Substrings and Subsequences

## Substring

A substring is a continuous sequence of characters.

Example:

```text
String: abcde
```

Valid substrings:

```text
abc
bcd
cde
bc
```

The characters must be continuous.

## Subsequences

A subsequence is created by removing zero or more characters without changing the relative order of the remaining characters.

Example:

```text
String: abcde
```

Valid subsequences:

```text
ace
abd
bde
abcde
```

`ace` is a subsequence because the characters appear in the same order.

`aec` is not a subsequence because the order is different.

**Remember:**

- Every substring is a subsequence.
- Not every subsequence is a substring.

## Number of substrings

For a string of length `n`, the total number of non-empty substrings is:

\[
\frac{n(n+1)}{2}
\]

For `"abc"`:

```text
a
b
c
ab
bc
abc
```

Total: 6

---

# 18. Two-Pointer Technique

Two pointers are useful for solving string problems efficiently.

Example problems:

- Reverse a string.
- Check a palindrome.
- Compare strings from both ends.
- Find a pair of characters satisfying a condition.

Example: Check whether a string is a palindrome.

```cpp
string s = "level";

int left = 0;
int right = s.size() - 1;

while (left < right) {
    if (s[left] != s[right]) {
        cout << "Not palindrome";
        return 0;
    }

    left++;
    right--;
}

cout << "Palindrome";
```

Instead of repeatedly creating reversed strings, two pointers can solve the problem in O(n) time and O(1) extra space.

---

# 19. Sliding Window Technique

Sliding window is used when a problem asks about a continuous part of a string.

Typical problems:

- Longest substring without repeating characters.
- Longest substring with at most K distinct characters.
- Minimum window containing all required characters.
- Counting substrings that satisfy certain conditions.

Example:

Find the longest substring without repeating characters.

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int longestUniqueSubstring(string s) {
    int last[256];

    fill(last, last + 256, -1);

    int left = 0;
    int best = 0;

    for (int right = 0; right < s.size(); right++) {
        unsigned char ch = s[right];

        if (last[ch] >= left) {
            left = last[ch] + 1;
        }

        last[ch] = right;

        best = max(best, right - left + 1);
    }

    return best;
}

int main() {
    cout << longestUniqueSubstring("abcabcbb");
}
```

Output:

```text
3
```

The longest substrings without repeated characters include:

```text
abc
bca
cab
```

Time complexity: O(n)

Extra space complexity: O(1), for the fixed 256-entry array.

---

# 20. String Searching Algorithms

String searching means finding a pattern inside a larger string.

Example:

```text
Text:    ababcabc
Pattern: abc
```

The pattern occurs at indices:

```text
2
5
```

## 20.1 Naive string matching

Check the pattern at every possible starting position.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string text = "ababcabc";
    string pattern = "abc";

    for (int i = 0; i <= text.size() - pattern.size(); i++) {
        int j = 0;

        while (j < pattern.size() &&
               text[i + j] == pattern[j]) {
            j++;
        }

        if (j == pattern.size()) {
            cout << i << " ";
        }
    }
}
```

Output:

```text
2 5
```

Worst-case time complexity: O(n × m)

Where:

- `n` is the text length.
- `m` is the pattern length.

## 20.2 KMP algorithm

Knuth-Morris-Pratt (KMP) is a more efficient pattern-searching algorithm.

It uses an LPS array:

**LPS = Longest Proper Prefix which is also a Suffix.**

KMP avoids repeating comparisons by remembering information about the pattern.

Time complexity:

```text
O(n + m)
```

KMP is useful when:

- The text is large.
- The pattern occurs many times.
- Repeated comparisons make naive searching slow.

---

# 21. String Sorting

Sorting rearranges characters into a specific order.

Example:

```text
Original: dcba
Sorted:   abcd
```

C++:

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main() {
    string s = "dcba";

    sort(s.begin(), s.end());

    cout << s;

    return 0;
}
```

Output:

```text
abcd
```

Time complexity: O(n log n)

Sorting is frequently used for:

- Anagram checking
- Grouping words
- Finding duplicate characters
- Comparing character distributions

---

# 22. Important STL Functions

| Function | Purpose | Example |
|---|---|---|
| `length()` | Returns string length | `s.length()` |
| `size()` | Returns string length | `s.size()` |
| `empty()` | Checks whether string is empty | `s.empty()` |
| `push_back()` | Adds a character | `s.push_back('a')` |
| `pop_back()` | Removes last character | `s.pop_back()` |
| `append()` | Adds text | `s.append("abc")` |
| `substr()` | Extracts substring | `s.substr(1, 3)` |
| `find()` | Searches for text | `s.find("abc")` |
| `erase()` | Removes text | `s.erase(2, 1)` |
| `insert()` | Inserts text | `s.insert(2, "xy")` |
| `replace()` | Replaces text | `s.replace(0, 2, "hi")` |
| `reverse()` | Reverses a string | `reverse(s.begin(), s.end())` |
| `sort()` | Sorts characters | `sort(s.begin(), s.end())` |
| `tolower()` | Converts a character to lowercase | `tolower(ch)` |
| `toupper()` | Converts a character to uppercase | `toupper(ch)` |

---

# 23. Time Complexity

Let `n` be the length of the string.

| Operation | Typical complexity |
|---|---|
| Access character by index | O(1) |
| Get string length | O(1) |
| Traverse entire string | O(n) |
| Reverse entire string | O(n) |
| Palindrome check | O(n) |
| Frequency counting | O(n) |
| Anagram using sorting | O(n log n) |
| Anagram using frequency array | O(n) |
| Naive pattern searching | O(n × m) worst case |
| KMP pattern searching | O(n + m) |
| Sorting characters | O(n log n) |

Note: Actual performance can depend on the specific operation, input, and implementation.

---

# 24. Common Coding Interview Questions

## Question 1: Reverse a string

Input:

```text
hello
```

Output:

```text
olleh
```

Concepts: Two pointers, `reverse()`.

## Question 2: Check palindrome

Input:

```text
madam
```

Output:

```text
Palindrome
```

Concepts: Two pointers.

## Question 3: Count vowels

Input:

```text
education
```

Output:

```text
5
```

Concepts: Traversal, condition checking.

## Question 4: Count words

Input:

```text
I love programming
```

Output:

```text
3
```

Concepts: String traversal, whitespace handling.

## Question 5: Find the first non-repeating character

Input:

```text
aabbcdde
```

Output:

```text
c
```

Concepts: Frequency counting, traversal.

## Question 6: Check anagrams

Input:

```text
listen
silent
```

Output:

```text
Anagrams
```

Concepts: Sorting, frequency arrays.

## Question 7: Remove duplicate characters

Input:

```text
programming
```

Output:

```text
progamin
```

Concepts: Frequency counting, preserving order.

## Question 8: Find the longest word

Input:

```text
I love computer programming
```

Output:

```text
programming
```

Concepts: Word boundaries, length comparison.

## Question 9: Find a substring

Input:

```text
Text: abcdef
Pattern: cd
```

Output:

```text
Found at index 2
```

Concepts: Pattern searching.

## Question 10: Longest substring without repeating characters

Input:

```text
abcabcbb
```

Output:

```text
3
```

Concepts: Sliding window, last-seen positions.

---

# 25. Practice Problems

Try solving these problems in order.

## Beginner Level

1. Print every character of a string on a new line.
2. Find the length of a string without using `length()`.
3. Count vowels and consonants.
4. Convert lowercase characters to uppercase.
5. Reverse a string.
6. Check whether a string is a palindrome.
7. Count the number of spaces in a string.
8. Count the number of digits in a string.
9. Find the largest and smallest character.
10. Remove all spaces from a string.

## Intermediate Level

1. Check whether two strings are anagrams.
2. Find the first repeating character.
3. Find the first non-repeating character.
4. Remove duplicate characters.
5. Find the frequency of each character.
6. Find the longest word in a sentence.
7. Find all occurrences of a pattern.
8. Find the longest common prefix.
9. Reverse every word in a sentence.
10. Check whether one string is a rotation of another.

## Advanced Level

1. Longest substring without repeating characters.
2. Longest palindromic substring.
3. Minimum window substring.
4. Implement the KMP algorithm.
5. Implement the Rabin-Karp algorithm.
6. Group anagrams.
7. Edit distance between two strings.
8. Longest common subsequence.
9. Wildcard pattern matching.
10. Regular expression matching.

---

# 26. Common Mistakes

## Mistake 1: Using the wrong index

Incorrect:

```cpp
for (int i = 0; i <= s.length(); i++) {
    cout << s[i];
}
```

Correct:

```cpp
for (int i = 0; i < s.length(); i++) {
    cout << s[i];
}
```

The last valid index is `length() - 1`.

## Mistake 2: Confusing character and string

Incorrect:

```cpp
char ch = "a";
```

Correct:

```cpp
char ch = 'a';
```

## Mistake 3: Using cin for a complete sentence

If a string contains spaces, use `getline()`.

## Mistake 4: Forgetting uppercase and lowercase

```text
Apple
apple
```

These strings are different unless you explicitly perform case-insensitive comparison.

## Mistake 5: Using ASCII indexing incorrectly

This is appropriate only for lowercase letters:

```cpp
freq[ch - 'a']++;
```

Do not use it directly for uppercase letters, digits, or punctuation.

## Mistake 6: Calling pop_back on an empty string

Always verify that the string is not empty before removing its last character.

---

# 27. Quick Revision

Remember these important points:

- A string is a sequence of characters.
- C++ strings use the `string` class.
- String indexing starts from `0`.
- The last valid index is `length() - 1`.
- Use `getline()` to read a sentence containing spaces.
- Use `substr()` to extract a substring.
- Use `find()` to search for a pattern.
- Use two pointers for palindrome and reversal problems.
- Use frequency counting for anagrams and duplicate characters.
- Use sliding window for substring problems involving continuous characters.
- Use KMP for efficient pattern matching.

## Final Advice for Beginners

When solving a string problem:

1. Understand what the input represents.
2. Identify whether the question involves characters, words, substrings, or subsequences.
3. Check whether case, spaces, and punctuation matter.
4. Start with a simple brute-force solution.
5. Analyze its time and space complexity.
6. Optimize using two pointers, frequency counting, sliding window, or an efficient searching algorithm.

**The best way to master strings is to write the code yourself, test it with different inputs, and understand why each step works.**
