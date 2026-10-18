# Stack in C++ — Complete Beginner's Guide

A complete guide to Stack Data Structure, covering basic concepts, implementation, operations, applications, and coding interview questions.

## Table of Contents

1. [Introduction to Stack](#1-introduction-to-stack)
2. [What Is a Stack?](#2-what-is-a-stack)
3. [LIFO Principle](#3-lifo-principle)
4. [Real-Life Applications of Stack](#4-real-life-applications-of-stack)
5. [Basic Stack Operations](#5-basic-stack-operations)
6. [Stack Implementation Using Array](#6-stack-implementation-using-array)
7. [Stack Implementation Using Linked List](#7-stack-implementation-using-linked-list)
8. [Stack Using STL](#8-stack-using-stl)
9. [Stack Overflow and Stack Underflow](#9-stack-overflow-and-stack-underflow)
10. [Time and Space Complexity](#10-time-and-space-complexity)
11. [Reversing a String Using Stack](#11-reversing-a-string-using-stack)
12. [Balanced Parentheses](#12-balanced-parentheses)
13. [Infix, Prefix, and Postfix Expressions](#13-infix-prefix-and-postfix-expressions)
14. [Next Greater Element](#14-next-greater-element)
15. [Min Stack](#15-min-stack)
16. [Recursion and Call Stack](#16-recursion-and-call-stack)
17. [Important Stack STL Functions](#17-important-stack-stl-functions)
18. [Common Coding Interview Questions](#18-common-coding-interview-questions)
19. [Practice Problems](#19-practice-problems)
20. [Common Mistakes](#20-common-mistakes)
21. [Quick Revision](#21-quick-revision)

---

## 1. Introduction to Stack

A stack is a linear data structure used to store and manage elements.

It is one of the most important data structures in DSA.

Stacks are useful in:

- Undo and redo operations
- Browser history
- Function calls
- Expression evaluation
- Parentheses checking
- Backtracking algorithms

A stack allows insertion and deletion from one end only, called the **top**.

[Back to Table of Contents](#table-of-contents)

---

## 2. What Is a Stack?

A stack is a collection of elements where insertion and deletion happen at the same end.

Example:

```text
       TOP
        |
       30
       20
       10
```

Here, `30` is the top element.

If we remove an element, `30` is removed first.

If we insert a new element, it is placed above `30`.

[Back to Table of Contents](#table-of-contents)

---

## 3. LIFO Principle

Stack follows the **LIFO** principle.

LIFO means:

**Last In, First Out**

The element inserted last is removed first.

Example:

Push:

```text
Push 10
Push 20
Push 30
```

Stack:

```text
TOP → 30
      20
      10
```

Pop:

```text
Removed: 30
```

Remaining stack:

```text
TOP → 20
      10
```

Another example:

Imagine a stack of plates.

You place a plate on top of the stack. When you take a plate, you normally remove the topmost plate first.

That is how a stack works.

[Back to Table of Contents](#table-of-contents)

---

## 4. Real-Life Applications of Stack

### 4.1 Undo Operation

When you type text in an editor, the application can store your previous actions in a stack.

Example:

```text
Type A
Type B
Type C
```

Undo removes the latest action first.

```text
Undo → Remove C
Undo → Remove B
```

### 4.2 Browser History

A browser can use stacks to manage navigation history.

When you open a new page, the current page can be stored in a history structure.

The Back operation takes you to the previous page.

### 4.3 Function Calls

When a function is called, the program stores information about the function's execution.

When the function finishes, its execution information is removed.

This is managed using the call stack.

### 4.4 Expression Evaluation

Stacks are used to evaluate mathematical expressions.

Example:

```text
2 + 3 * 4
```

The multiplication must be handled before addition.

Stacks help manage operators and operands during expression evaluation.

### 4.5 Backtracking

Backtracking means trying a choice and returning to an earlier state if the choice does not work.

Examples:

- Maze solving
- Sudoku
- Depth First Search
- Finding paths

[Back to Table of Contents](#table-of-contents)

---

## 5. Basic Stack Operations

A stack mainly supports the following operations.

| Operation | Meaning |
|---|---|
| Push | Insert an element |
| Pop | Remove the top element |
| Top / Peek | Access the top element |
| Empty | Check whether stack is empty |
| Size | Find the number of elements |

### Push

Push inserts an element at the top.

Before:

```text
TOP → 20
      10
```

Push 30:

```text
TOP → 30
      20
      10
```

### Pop

Pop removes the top element.

Before:

```text
TOP → 30
      20
      10
```

After pop:

```text
TOP → 20
      10
```

### Peek

Peek returns the top element without removing it.

```text
TOP → 30
      20
      10
```

Peek returns `30`, and the stack remains unchanged.

[Back to Table of Contents](#table-of-contents)

---

## 6. Stack Implementation Using Array

An array can be used to implement a stack.

We use a variable called `top` to track the topmost element.

Initially:

```cpp
top = -1;
```

This means the stack is empty.

### Complete C++ Code

```cpp
#include <iostream>
using namespace std;

class Stack {
private:
    int arr[5];
    int top;

public:
    Stack() {
        top = -1;
    }

    // Insert an element
    void push(int value) {
        if (top == 4) {
            cout << "Stack Overflow\n";
            return;
        }

        top++;
        arr[top] = value;
    }

    // Remove the top element
    void pop() {
        if (top == -1) {
            cout << "Stack Underflow\n";
            return;
        }

        cout << "Removed: " << arr[top] << endl;
        top--;
    }

    // Display top element
    void peek() {
        if (top == -1) {
            cout << "Stack is empty\n";
            return;
        }

        cout << "Top: " << arr[top] << endl;
    }

    // Display all elements
    void display() {
        if (top == -1) {
            cout << "Stack is empty\n";
            return;
        }

        for (int i = top; i >= 0; i--) {
            cout << arr[i] << " ";
        }

        cout << endl;
    }
};

int main() {
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);

    s.display();

    s.peek();

    s.pop();

    s.display();

    return 0;
}
```

Output:

```text
30 20 10
Top: 30
Removed: 30
20 10
```

### How the top variable works

Initially:

```text
top = -1
```

Push 10:

```text
top = 0
arr[0] = 10
```

Push 20:

```text
top = 1
arr[1] = 20
```

Push 30:

```text
top = 2
arr[2] = 30
```

The stack looks like:

```text
Index     Value
  2        30  ← TOP
  1        20
  0        10
```

Pop:

```cpp
top--;
```

The top moves from index `2` to index `1`.

The element `30` is no longer part of the active stack.

### Advantages

- Simple to implement
- Fast operations
- No extra pointer required

### Disadvantages

- Fixed capacity
- Cannot grow beyond the array size
- May waste memory if the array is too large

[Back to Table of Contents](#table-of-contents)

---

## 7. Stack Implementation Using Linked List

A linked list can also be used to implement a stack.

Each node contains:

- Data
- Pointer to the next node

The top pointer points to the first node.

### Complete C++ Code

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;

    Node(int value) {
        data = value;
        next = nullptr;
    }
};

class Stack {
private:
    Node* top;

public:
    Stack() {
        top = nullptr;
    }

    // Insert at top
    void push(int value) {
        Node* newNode = new Node(value);

        newNode->next = top;
        top = newNode;
    }

    // Remove top node
    void pop() {
        if (top == nullptr) {
            cout << "Stack Underflow\n";
            return;
        }

        Node* temp = top;

        cout << "Removed: " << temp->data << endl;

        top = top->next;

        delete temp;
    }

    // Access top element
    void peek() {
        if (top == nullptr) {
            cout << "Stack is empty\n";
            return;
        }

        cout << "Top: " << top->data << endl;
    }

    // Display stack
    void display() {
        Node* temp = top;

        while (temp != nullptr) {
            cout << temp->data << " ";
            temp = temp->next;
        }

        cout << endl;
    }

    // Free allocated memory
    ~Stack() {
        while (top != nullptr) {
            Node* temp = top;
            top = top->next;
            delete temp;
        }
    }
};

int main() {
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);

    s.display();

    s.peek();

    s.pop();

    s.display();

    return 0;
}
```

Output:

```text
30 20 10
Top: 30
Removed: 30
20 10
```

### How it works

Push 10:

```text
TOP → 10 → NULL
```

Push 20:

```text
TOP → 20 → 10 → NULL
```

Push 30:

```text
TOP → 30 → 20 → 10 → NULL
```

Pop removes the first node.

```text
TOP → 20 → 10 → NULL
```

### Advantages

- Dynamic size
- No fixed array capacity
- Memory allocated as required

### Disadvantages

- Extra memory for pointers
- Dynamic memory management is required
- More complicated than array implementation

[Back to Table of Contents](#table-of-contents)

---

## 8. Stack Using STL

C++ provides a ready-made stack through the STL.

Header:

```cpp
#include <stack>
```

### Complete Code

```cpp
#include <iostream>
#include <stack>
using namespace std;

int main() {
    stack<int> s;

    s.push(10);
    s.push(20);
    s.push(30);

    cout << "Top: " << s.top() << endl;

    s.pop();

    cout << "Top after pop: " << s.top() << endl;

    cout << "Size: " << s.size() << endl;

    cout << "Empty: " << s.empty() << endl;

    return 0;
}
```

Output:

```text
Top: 30
Top after pop: 20
Size: 2
Empty: 0
```

### Important STL Functions

| Function | Meaning |
|---|---|
| `push(x)` | Insert element |
| `pop()` | Remove top element |
| `top()` | Access top element |
| `empty()` | Check if stack is empty |
| `size()` | Return number of elements |

### Important Point

`pop()` removes an element but does not return it.

Incorrect:

```cpp
int x = s.pop();
```

Correct:

```cpp
int x = s.top();
s.pop();
```

Always check whether the stack is empty before calling `top()` or `pop()`.

[Back to Table of Contents](#table-of-contents)

---

## 9. Stack Overflow and Stack Underflow

### Stack Overflow

Stack overflow happens when we try to insert an element into a full fixed-capacity stack.

Example:

```text
Stack capacity = 3

Push 10
Push 20
Push 30
Push 40
```

The fourth insertion causes overflow.

For the array implementation:

```cpp
if (top == capacity - 1) {
    cout << "Stack Overflow";
}
```

### Stack Underflow

Stack underflow happens when we try to remove an element from an empty stack.

Example:

```cpp
stack<int> s;

s.pop();
```

Calling `pop()` on an empty STL stack is invalid.

Correct:

```cpp
if (!s.empty()) {
    s.pop();
}
```

[Back to Table of Contents](#table-of-contents)

---

## 10. Time and Space Complexity

For a stack implemented using an array or linked list:

| Operation | Time Complexity |
|---|---|
| Push | O(1) |
| Pop | O(1) |
| Peek | O(1) |
| Empty | O(1) |
| Size | O(1) |
| Display all elements | O(n) |

Space complexity:

```text
O(n)
```

Where `n` is the number of elements stored in the stack.

[Back to Table of Contents](#table-of-contents)

---

## 11. Reversing a String Using Stack

A stack reverses a sequence because it follows LIFO.

Example:

```text
Original: HELLO
```

Push each character:

```text
H
E
L
L
O ← TOP
```

Pop all characters:

```text
OLLEH
```

### C++ Code

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

int main() {
    string s = "HELLO";

    stack<char> st;

    for (char ch : s) {
        st.push(ch);
    }

    string reversed = "";

    while (!st.empty()) {
        reversed += st.top();
        st.pop();
    }

    cout << reversed;

    return 0;
}
```

Output:

```text
OLLEH
```

Time complexity: O(n)

Space complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 12. Balanced Parentheses

A string of parentheses is balanced if every opening bracket has a matching closing bracket in the correct order.

Examples:

```text
()
(())
()()
```

Unbalanced examples:

```text
(
())
)(
```

### Algorithm

1. Create an empty stack.
2. Traverse the expression.
3. If an opening bracket is found, push it.
4. If a closing bracket is found, check the stack.
5. If the stack is empty or brackets do not match, return false.
6. At the end, the stack must be empty.

### C++ Code

```cpp
#include <iostream>
#include <stack>
#include <string>
using namespace std;

bool isBalanced(string s) {
    stack<char> st;

    for (char ch : s) {
        if (ch == '(' || ch == '{' || ch == '[') {
            st.push(ch);
        }
        else {
            if (st.empty()) {
                return false;
            }

            char top = st.top();
            st.pop();

            if (ch == ')' && top != '(') return false;
            if (ch == '}' && top != '{') return false;
            if (ch == ']' && top != '[') return false;
        }
    }

    return st.empty();
}

int main() {
    string s = "{[()]}";

    if (isBalanced(s))
        cout << "Balanced";
    else
        cout << "Not Balanced";

    return 0;
}
```

Output:

```text
Balanced
```

Time complexity: O(n)

Space complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 13. Infix, Prefix, and Postfix Expressions

Mathematical expressions can be represented in three forms.

### Infix

Operator is between operands.

```text
A + B
```

### Prefix

Operator comes before operands.

```text
+ A B
```

### Postfix

Operator comes after operands.

```text
A B +
```

Example:

```text
Infix:   A + B * C
Postfix: A B C * +
Prefix:   + A * B C
```

Stacks are used to convert and evaluate these expressions.

Why?

Because stacks help manage:

- Operator precedence
- Parentheses
- Operand order

[Back to Table of Contents](#table-of-contents)

---

## 14. Next Greater Element

The Next Greater Element problem asks us to find the first greater element on the right for each array element.

Example:

```text
Array:  4  5  2  10
```

Answer:

```text
       5  10  10  -1
```

For `4`, the next greater element is `5`.

For `5`, the next greater element is `10`.

For `2`, the next greater element is `10`.

For `10`, no greater element exists, so answer is `-1`.

### C++ Code

```cpp
#include <iostream>
#include <stack>
#include <vector>
using namespace std;

int main() {
    vector<int> arr = {4, 5, 2, 10};

    int n = arr.size();

    vector<int> ans(n, -1);

    stack<int> st;

    for (int i = n - 1; i >= 0; i--) {

        while (!st.empty() && st.top() <= arr[i]) {
            st.pop();
        }

        if (!st.empty()) {
            ans[i] = st.top();
        }

        st.push(arr[i]);
    }

    for (int x : ans) {
        cout << x << " ";
    }

    return 0;
}
```

Output:

```text
5 10 10 -1
```

Time complexity: O(n)

[Back to Table of Contents](#table-of-contents)

---

## 15. Min Stack

A Min Stack is a stack that supports:

- Push
- Pop
- Top
- Getting the minimum element

All in O(1) time.

A simple approach is to maintain a second stack that stores the minimum value at each level.

### Example

Push:

```text
10
20
5
```

Main stack:

```text
TOP → 5
      20
      10
```

Minimum stack:

```text
TOP → 5
      10
      10
```

The minimum value is `5`.

After popping `5`, the minimum becomes `10`.

[Back to Table of Contents](#table-of-contents)

---

## 16. Recursion and Call Stack

When a function calls another function, the program stores information about each function call.

This information is managed using the call stack.

Example:

```cpp
void fun1() {
    fun2();
}

void fun2() {
    fun3();
}

void fun3() {
    // Work
}
```

Execution:

```text
fun1()
  ↓
fun2()
  ↓
fun3()
```

When `fun3()` finishes, it returns to `fun2()`.

When `fun2()` finishes, it returns to `fun1()`.

This follows LIFO.

### Recursion Example

```cpp
#include <iostream>
using namespace std;

void countdown(int n) {
    if (n == 0) {
        return;
    }

    cout << n << " ";

    countdown(n - 1);
}

int main() {
    countdown(3);

    return 0;
}
```

Output:

```text
3 2 1
```

Each recursive call adds a new call-stack frame.

When the base case is reached, the calls return in reverse order.

[Back to Table of Contents](#table-of-contents)

---

## 17. Important Stack STL Functions

| Function | Description |
|---|---|
| `push(x)` | Adds an element |
| `pop()` | Removes the top element |
| `top()` | Returns the top element |
| `empty()` | Returns true if stack is empty |
| `size()` | Returns number of elements |
| `swap(s2)` | Exchanges elements with another stack |

Example:

```cpp
stack<int> s;

s.push(10);
s.push(20);

cout << s.top();
```

Output:

```text
20
```

[Back to Table of Contents](#table-of-contents)

---

## 18. Common Coding Interview Questions

### Beginner

1. Implement a stack using an array.
2. Implement a stack using a linked list.
3. Reverse a string using a stack.
4. Check balanced parentheses.
5. Implement push, pop, and peek.

### Intermediate

1. Next Greater Element.
2. Next Smaller Element.
3. Min Stack.
4. Stock Span Problem.
5. Evaluate Postfix Expression.
6. Infix to Postfix Conversion.

### Advanced

1. Largest Rectangle in Histogram.
2. Maximal Rectangle.
3. Trapping Rain Water using Stack.
4. Basic Calculator.
5. Remove K Digits.
6. Asteroid Collision.

[Back to Table of Contents](#table-of-contents)

---

## 19. Practice Problems

### Easy

- Implement stack using array.
- Implement stack using linked list.
- Reverse a string using stack.
- Check balanced parentheses.
- Find the middle element of a stack.

### Medium

- Next Greater Element.
- Next Smaller Element.
- Stock Span.
- Min Stack.
- Evaluate Postfix Expression.

### Hard

- Largest Rectangle in Histogram.
- Trapping Rain Water.
- Maximal Rectangle.
- Remove K Digits.
- Basic Calculator.

[Back to Table of Contents](#table-of-contents)

---

## 20. Common Mistakes

### Mistake 1: Popping an empty stack

Incorrect:

```cpp
stack<int> s;

s.pop();
```

Correct:

```cpp
if (!s.empty()) {
    s.pop();
}
```

### Mistake 2: Accessing top of empty stack

Incorrect:

```cpp
cout << s.top();
```

Correct:

```cpp
if (!s.empty()) {
    cout << s.top();
}
```

### Mistake 3: Thinking pop returns the element

Incorrect:

```cpp
int x = s.pop();
```

Correct:

```cpp
int x = s.top();
s.pop();
```

### Mistake 4: Array stack overflow

Check whether the array is full before pushing.

### Mistake 5: Wrong linked list pointer update

When popping a linked list stack, update `top` before deleting the old node.

[Back to Table of Contents](#table-of-contents)

---

## 21. Quick Revision

- Stack is a linear data structure.
- Stack follows LIFO.
- Push inserts an element.
- Pop removes the top element.
- Peek or top accesses the top element.
- Stack overflow occurs when inserting into a full fixed-capacity stack.
- Stack underflow occurs when removing from an empty stack.
- Stack can be implemented using arrays, linked lists, or STL.
- Push, pop, and peek typically take O(1) time.
- Stacks are used in recursion, expression evaluation, backtracking, and parentheses checking.

## Final Advice

To master stacks:

1. Understand LIFO.
2. Implement stack using an array.
3. Implement stack using a linked list.
4. Practice balanced parentheses.
5. Solve Next Greater Element.
6. Learn monotonic stack problems.
7. Analyze time and space complexity.

**Practice each problem by tracing the stack after every push and pop. This makes stack-based algorithms much easier to understand.**
