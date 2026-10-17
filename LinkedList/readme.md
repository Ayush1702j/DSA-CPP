# Linked List in C++

A beginner-friendly guide to understanding Linked Lists in C++ with explanations, examples, operations, and practice questions.

## 1. What is a Linked List?

A **Linked List** is a linear data structure in which elements are stored in separate memory locations called **nodes**.

Each node contains two main parts:

1. **Data:** Stores the actual value.
2. **Pointer:** Stores the address of the next node.

Unlike arrays, linked list elements are not stored in consecutive memory locations.

### Example

```text
Head
 |
 v
[10 | next] -> [20 | next] -> [30 | NULL]
```

Here:
- `10`, `20`, and `30` are data values.
- Each node points to the next node.
- `NULL` indicates the end of the list.

## 2. Why Do We Need Linked Lists?

Arrays have a fixed size in traditional static allocation, and inserting or deleting elements in the middle may require shifting other elements.

Linked Lists provide:
- Dynamic memory allocation.
- Easy insertion and deletion when the relevant node is known.
- Flexible memory usage as elements are added or removed.

However, linked lists also have limitations:
- Extra memory is required for pointers.
- Random access is not possible.
- Searching for an element can take O(n) time.

## 3. Structure of a Node

In C++, a node can be created using a structure.

```cpp
struct Node {
    int data;
    Node* next;
};
```

Explanation:

| Component | Meaning |
|---|---|
| `int data` | Stores the value |
| `Node* next` | Stores the address of the next node |
| `Node` | Represents one element of the linked list |

The `next` pointer is of type `Node*` because it points to another node.

## 4. Creating a Node

The `new` keyword dynamically allocates memory for a node.

```cpp
Node* newNode = new Node;

newNode->data = 10;
newNode->next = nullptr;
```

Here:
- `new Node` creates a new node.
- `->` is used to access members through a pointer.
- `nullptr` means the pointer does not point to another node.

## 5. Types of Linked Lists

### A. Singly Linked List

Each node contains data and a pointer to the next node.

```text
[10] -> [20] -> [30] -> NULL
```

Features:
- Traversal is possible only in the forward direction.
- Each node contains one link.
- It is memory-efficient compared to a doubly linked list.

### B. Doubly Linked List

Each node contains three parts:

- Pointer to the previous node.
- Data.
- Pointer to the next node.

```text
NULL <- [10] <-> [20] <-> [30] -> NULL
```

Features:
- Traversal is possible in both directions.
- Deletion of a known node is easier.
- Requires extra memory for the previous pointer.

### C. Circular Singly Linked List

The last node points back to the first node instead of `NULL`.

```text
       +-------------------+
       |                   |
       v                   |
[10] -> [20] -> [30] ------+
```

Features:
- There is no `NULL` at the end.
- Traversal can continue in a circular manner.
- Useful in round-robin scheduling and cyclic processes.

### D. Circular Doubly Linked List

The nodes contain both previous and next pointers, and the first and last nodes are connected.

```text
[10] <-> [20] <-> [30]
 ^                   |
 |___________________|
```

Features:
- Forward and backward traversal.
- Circular connection between the first and last nodes.
- Useful for playlists and navigation systems.

## 6. Basic Linked List Operations

The main operations are:

| Operation | Description |
|---|---|
| Traversal | Visit every node |
| Insertion | Add a new node |
| Deletion | Remove an existing node |
| Searching | Find a particular value |
| Counting | Calculate the number of nodes |
| Reversing | Change the direction of links |

## 7. Complete C++ Program: Singly Linked List

This program demonstrates creating a linked list, inserting nodes, displaying the list, searching, counting, deleting, and reversing.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

// Insert a node at the end
void insertAtEnd(Node*& head, int value) {
    Node* newNode = new Node{value, nullptr};

    if (head == nullptr) {
        head = newNode;
        return;
    }

    Node* temp = head;

    while (temp->next != nullptr) {
        temp = temp->next;
    }

    temp->next = newNode;
}

// Insert a node at the beginning
void insertAtBeginning(Node*& head, int value) {
    Node* newNode = new Node{value, head};
    head = newNode;
}

// Display the linked list
void display(Node* head) {
    Node* temp = head;

    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }

    cout << "NULL" << endl;
}

// Search for an element
bool search(Node* head, int key) {
    Node* temp = head;

    while (temp != nullptr) {
        if (temp->data == key) {
            return true;
        }

        temp = temp->next;
    }

    return false;
}

// Count the number of nodes
int countNodes(Node* head) {
    int count = 0;
    Node* temp = head;

    while (temp != nullptr) {
        count++;
        temp = temp->next;
    }

    return count;
}

// Delete a node by value
void deleteNode(Node*& head, int key) {
    if (head == nullptr) {
        return;
    }

    // If the first node contains the key
    if (head->data == key) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }

    Node* temp = head;

    while (temp->next != nullptr &&
           temp->next->data != key) {
        temp = temp->next;
    }

    // Key was not found
    if (temp->next == nullptr) {
        return;
    }

    Node* nodeToDelete = temp->next;
    temp->next = nodeToDelete->next;

    delete nodeToDelete;
}

// Reverse the linked list
void reverseList(Node*& head) {
    Node* previous = nullptr;
    Node* current = head;
    Node* nextNode = nullptr;

    while (current != nullptr) {
        nextNode = current->next;
        current->next = previous;
        previous = current;
        current = nextNode;
    }

    head = previous;
}

// Free all allocated memory
void freeList(Node*& head) {
    while (head != nullptr) {
        Node* temp = head;
        head = head->next;
        delete temp;
    }
}

int main() {
    Node* head = nullptr;

    insertAtEnd(head, 10);
    insertAtEnd(head, 20);
    insertAtEnd(head, 30);

    cout << "Original List: ";
    display(head);

    insertAtBeginning(head, 5);

    cout << "After Insertion: ";
    display(head);

    cout << "Number of Nodes: "
         << countNodes(head) << endl;

    if (search(head, 20)) {
        cout << "20 found in the list" << endl;
    } else {
        cout << "20 not found" << endl;
    }

    deleteNode(head, 20);

    cout << "After Deletion: ";
    display(head);

    reverseList(head);

    cout << "After Reversing: ";
    display(head);

    freeList(head);

    return 0;
}
```

## 8. Expected Output

```text
Original List: 10 -> 20 -> 30 -> NULL
After Insertion: 5 -> 10 -> 20 -> 30 -> NULL
Number of Nodes: 4
20 found in the list
After Deletion: 5 -> 10 -> 30 -> NULL
After Reversing: 30 -> 10 -> 5 -> NULL
```

## 9. Understanding Important Operations

### Traversal

Traversal means visiting each node from the beginning to the end.

```cpp
Node* temp = head;

while (temp != nullptr) {
    cout << temp->data << " ";
    temp = temp->next;
}
```

The pointer moves to the next node until it reaches `nullptr`.

### Insertion at the Beginning

```text
Before:  10 -> 20 -> 30 -> NULL

Insert 5

After:   5 -> 10 -> 20 -> 30 -> NULL
```

Steps:
1. Create a new node.
2. Make its `next` point to the current head.
3. Update the head to the new node.

Time complexity: O(1).

### Insertion at the End

```text
Before: 10 -> 20 -> NULL

Insert 30

After:  10 -> 20 -> 30 -> NULL
```

For a list without a tail pointer, we must traverse to the last node.

Time complexity: O(n).

### Deletion

```text
Before: 10 -> 20 -> 30 -> NULL

Delete 20

After:  10 -> 30 -> NULL
```

The previous node is connected directly to the next node, and the deleted node's memory is released.

## 10. Reversing a Linked List

Reversing changes the direction of every link.

```text
Before:
10 -> 20 -> 30 -> NULL

After:
30 -> 20 -> 10 -> NULL
```

The algorithm uses three pointers:

- `previous`: The previous node.
- `current`: The node currently being processed.
- `nextNode`: Temporarily stores the next node so the remaining list is not lost.

Time complexity: O(n).

Space complexity: O(1).

## 11. Time Complexity

For a singly linked list without a tail pointer:

| Operation | Time Complexity |
|---|---|
| Access first node | O(1) |
| Access node at index | O(n) |
| Search | O(n) |
| Insert at beginning | O(1) |
| Insert at end | O(n) |
| Delete first node | O(1) |
| Delete by value | O(n) |
| Count nodes | O(n) |
| Reverse list | O(n) |

Note: Insertion at the end can be O(1) if the linked list maintains a tail pointer. Deletion can also be O(1) when the relevant node and its previous node are already known.

## 12. Linked List vs Array

| Feature | Array | Linked List |
|---|---|---|
| Memory | Usually contiguous | Nodes can be scattered |
| Size | Fixed for static arrays | Dynamic |
| Random access | O(1) | O(n) |
| Insert at beginning | O(n) | O(1) |
| Extra pointer memory | No | Yes |
| Cache performance | Usually better | Usually lower |

## 13. Common Mistakes Beginners Make

1. Forgetting to initialize `next` with `nullptr`.
2. Losing the head pointer while traversing.
3. Updating pointers in the wrong order while reversing.
4. Forgetting to handle an empty list.
5. Not handling deletion of the first node separately.
6. Forgetting `delete` after removing dynamically allocated nodes.
7. Accessing a node after it has been deleted.
8. Creating an infinite loop in a circular linked list by checking for `nullptr`.

## 14. Practice Questions

### Beginner Level

1. Create a singly linked list of five integers and display it.
2. Insert a node at the beginning.
3. Insert a node at the end.
4. Count the number of nodes.
5. Search for an element in a linked list.

### Intermediate Level

6. Delete the first node.
7. Delete the last node.
8. Delete a node containing a specific value.
9. Insert a node at a particular position.
10. Reverse a singly linked list.
11. Find the middle node.
12. Find the maximum and minimum values.

### Advanced Level

13. Detect a loop in a linked list.
14. Remove duplicates from a sorted linked list.
15. Merge two sorted linked lists.
16. Find the nth node from the end.
17. Check whether a linked list is a palindrome.
18. Implement a doubly linked list.
19. Implement a circular linked list.

## 15. Applications of Linked Lists

Linked Lists are used in:

- Implementing stacks and queues.
- Music playlists.
- Browser navigation.
- Memory management.
- Hash table collision handling.
- Graph adjacency lists.
- Round-robin scheduling.

## 16. How to Compile and Run

Save the program in a file named `main.cpp`.

Using the GCC compiler:

```bash
g++ main.cpp -o linkedlist
```

Run on Windows:

```bash
linkedlist.exe
```

Run on Linux or macOS:

```bash
./linkedlist
```

## 17. Key Takeaways

- A linked list consists of nodes connected through pointers.
- The head pointer identifies the first node.
- A singly linked list supports forward traversal.
- Insertion at the beginning is O(1).
- Searching and accessing an arbitrary position are O(n).
- Pointers must be updated carefully to avoid losing nodes.
- Dynamically allocated nodes should be released using `delete`.

**The best way to learn linked lists is to draw the nodes and arrows on paper while executing each operation step by step.**
