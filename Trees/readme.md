# 🌳 Tree Data Structures in C++

A comprehensive, beginner-friendly guide to **Tree Data Structures and their implementation in C++**. This repository covers fundamental tree concepts, binary trees, Binary Search Trees (BST), tree traversal algorithms, insertion, searching, deletion, balanced trees, heaps, and other important concepts used in Data Structures and Algorithms (DSA).

The goal is to help learners understand not only how trees work but also why different tree structures are useful and how to analyze their performance.

---

## 📚 Table of Contents

1. [Introduction to Trees](#-1-introduction-to-trees)
2. [Why Do We Need Trees?](#-2-why-do-we-need-trees)
3. [Basic Tree Terminology](#-3-basic-tree-terminology)
4. [Types of Trees](#-4-types-of-trees)
5. [Binary Tree](#-5-binary-tree)
6. [Binary Search Tree (BST)](#-6-binary-search-tree-bst)
7. [BST Operations](#-7-bst-operations)
8. [Tree Traversal Algorithms](#-8-tree-traversal-algorithms)
9. [Height and Depth of a Tree](#-9-height-and-depth-of-a-tree)
10. [Balanced Trees and AVL Trees](#-10-balanced-trees-and-avl-trees)
11. [Heap Data Structure](#-11-heap-data-structure)
12. [B-Tree and B+ Tree](#-12-b-tree-and-b-tree)
13. [Trie Data Structure](#-13-trie-data-structure)
14. [Time Complexity Analysis](#-14-time-complexity-analysis)
15. [Applications of Trees](#-15-applications-of-trees)
16. [C++ Implementation](#-16-c-implementation)
17. [How to Run the Code](#-17-how-to-run-the-code)
18. [Common Interview Questions](#-18-common-interview-questions)
19. [Learning Roadmap](#-19-learning-roadmap)

---

## 🌱 1. Introduction to Trees

A **Tree** is a non-linear data structure that organizes data in a hierarchical manner using nodes and edges.

Unlike arrays and linked lists, which usually represent data sequentially, trees represent relationships between parent and child nodes.

### Example

```text
          10
         /  \
        20   30
       / \
      40  50
```

In this tree:

- `10` is the root node.
- `20` and `30` are children of `10`.
- `40` and `50` are children of `20`.
- `30`, `40`, and `50` are leaf nodes.

### Important Properties

- A non-empty tree has one root node.
- Every node except the root has one parent in a rooted tree.
- A tree contains no cycles.
- There is exactly one simple path between any two nodes in a tree.
- A tree containing `n` nodes has `n - 1` edges.

---

## 🎯 2. Why Do We Need Trees?

Trees are useful when information has a hierarchical structure or when searching and organizing data efficiently is important.

Consider a directory system:

```text
Computer
├── Documents
│   ├── Notes.txt
│   └── Report.pdf
├── Pictures
│   ├── Photo1.jpg
│   └── Photo2.jpg
└── Downloads
```

A tree represents this structure naturally because folders can contain subfolders and files.

### Advantages

- Represents hierarchical relationships clearly.
- Supports efficient searching in suitable tree structures.
- Makes sorted data retrieval possible with Binary Search Trees.
- Supports efficient minimum and maximum retrieval with heaps.
- Forms the foundation of several advanced data structures.

### Limitations

- Nodes may require additional memory for pointers.
- Some trees can become unbalanced.
- Operations can become slow if a tree becomes highly skewed.
- Implementing balancing and deletion can be complex.

---

## 🧠 3. Basic Tree Terminology

| Term | Definition |
|---|---|
| Node | An element that stores data. |
| Root | The topmost node of a tree. |
| Edge | A connection between two nodes. |
| Parent | A node that has one or more children. |
| Child | A node directly below its parent. |
| Sibling | Nodes that share the same parent. |
| Leaf node | A node with no children. |
| Internal node | A node that has at least one child. |
| Degree of a node | The number of children of that node. |
| Depth | Number of edges from the root to a node. |
| Height of a node | Number of edges on the longest downward path from that node to a leaf. |
| Height of a tree | Height of the root. |
| Subtree | A node together with its descendants. |
| Ancestor | A node that appears above another node on its path from the root. |
| Descendant | A node contained below another node. |

For an empty tree, height conventions may vary. In this repository, height is measured in **edges**, so a leaf has height `0`.

---

## 🌲 4. Types of Trees

### 4.1 General Tree

A general tree allows each node to have any number of children.

**Applications:** File systems, organization charts, and hierarchical information.

### 4.2 Binary Tree

A binary tree allows each node to have at most two children:

- Left child
- Right child

### 4.3 Full Binary Tree

A full binary tree is one in which every node has either zero or exactly two children.

### 4.4 Complete Binary Tree

A complete binary tree has every level completely filled except possibly the last level. The last level is filled from left to right.

Binary heaps use this structure.

### 4.5 Perfect Binary Tree

A perfect binary tree has all internal nodes with exactly two children, and every leaf is at the same depth.

### 4.6 Balanced Binary Tree

A balanced binary tree maintains a height that grows logarithmically with the number of nodes, according to its balancing rules.

AVL trees are one example.

### 4.7 Skewed Binary Tree

A skewed binary tree has nodes arranged mainly on one side.

```text
Left-skewed:

      30
     /
    20
   /
  10
```

A skewed BST can behave like a linked list, making search operations take O(n) time.

### 4.8 Binary Search Tree (BST)

A binary tree that maintains an ordering rule to support searching, insertion, and deletion.

### 4.9 AVL Tree

A self-balancing Binary Search Tree that uses rotations to maintain balance.

### 4.10 Red-Black Tree

A self-balancing Binary Search Tree that uses node colors and structural rules to keep its height logarithmic.

### 4.11 Heap

A complete binary tree that satisfies the min-heap or max-heap property.

### 4.12 B-Tree and B+ Tree

Balanced multiway search trees designed to store multiple keys per node. They are useful for disk-based storage and database indexing.

### 4.13 Trie

A tree-like structure that stores sequences, commonly strings and prefixes. It is useful for dictionaries and autocomplete.

---

## 🌳 5. Binary Tree

A Binary Tree is a tree in which every node has at most two children.

### Node Structure in C++

```cpp
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};
```

### Explanation

- `data` stores the node value.
- `left` points to the left child.
- `right` points to the right child.
- `nullptr` indicates that a child does not exist.

### Creating a Binary Tree

```cpp
Node* root = new Node(10);

root->left = new Node(20);
root->right = new Node(30);

root->left->left = new Node(40);
root->left->right = new Node(50);
```

The resulting tree is:

```text
          10
         /  \
        20   30
       / \
      40  50
```

This code creates a specific tree manually. It does not automatically insert values according to BST ordering rules.

---

## 🔍 6. Binary Search Tree (BST)

A **Binary Search Tree** is a binary tree that follows an ordering property.

For a standard BST with distinct keys:

- Every key in the left subtree is smaller than the current node.
- Every key in the right subtree is greater than the current node.
- Both subtrees must also satisfy the BST property.

### Example

Insert the values:

`50, 30, 70, 20, 40, 60, 80`

The resulting BST is:

```text
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
```

### How BST Insertion Works

1. The first value becomes the root.
2. If a new value is smaller than the current node, move left.
3. If it is greater, move right.
4. Continue until an empty child position is found.
5. Insert the new node there.

For this example:

- `30` is smaller than `50`, so it goes left.
- `70` is greater than `50`, so it goes right.
- `20` is smaller than `50` and `30`, so it goes to the left of `30`.

### Advantages of BST

- Supports ordered data storage.
- Inorder traversal produces sorted values.
- Searching can be efficient when the tree is balanced.
- Insertion and deletion preserve the ordering property.

### Limitations of BST

- A normal BST does not automatically balance itself.
- Sorted insertion can produce a skewed tree.
- Search, insertion, and deletion can take O(n) time in the worst case.

---

## ⚙️ 7. BST Operations

### 7.1 Insertion

Insertion adds a new value while preserving the BST ordering property.

**Example:** Insert `25` into the previous tree.

```text
             50
           /    \
         30      70
        /  \    /  \
       20  40  60  80
         \
          25
```

The new value is smaller than `30` but greater than `20`, so it becomes the right child of `20`.

### 7.2 Searching

Searching checks whether a key exists in the BST.

For example, to find `60`:

1. Compare `60` with `50`.
2. Move right because `60 > 50`.
3. Compare with `70`.
4. Move left because `60 < 70`.
5. The value is found.

At each step, the ordering property helps eliminate part of the search space.

### 7.3 Deletion

Deleting a node has three main cases.

**Case 1: Leaf node**

A leaf has no children, so it can be removed directly.

Example: Delete `20` when it has no children.

**Case 2: Node with one child**

Remove the node and connect its parent to its only child.

**Case 3: Node with two children**

Replace the node's value with either:

- Its inorder successor: the smallest value in its right subtree.
- Its inorder predecessor: the largest value in its left subtree.

Then remove the successor or predecessor from its original position.

### 7.4 Minimum and Maximum

- The minimum value is the leftmost node.
- The maximum value is the rightmost node.

These operations take O(h) time, where `h` is the tree height.

---

## 🔄 8. Tree Traversal Algorithms

Tree traversal means visiting each node in a specified order.

Consider this tree:

```text
          1
         / \
        2   3
       / \
      4   5
```

### 8.1 Inorder Traversal

**Order:** Left → Root → Right

Output:

```text
4 2 5 1 3
```

In a BST, inorder traversal returns values in ascending order when the tree follows the standard distinct-key ordering rule.

### 8.2 Preorder Traversal

**Order:** Root → Left → Right

Output:

```text
1 2 4 5 3
```

Preorder traversal is useful when a node must be processed before its children.

### 8.3 Postorder Traversal

**Order:** Left → Right → Root

Output:

```text
4 5 2 3 1
```

Postorder traversal is useful for processing children before their parent, such as when freeing a tree.

### 8.4 Level-Order Traversal

Level-order traversal visits nodes level by level from left to right, typically using a queue.

Output:

```text
1 2 3 4 5
```

### Recursive Traversal Code

```cpp
void inorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

void postorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}
```

### Level-Order Traversal Code

```cpp
#include <queue>

void levelOrder(Node* root) {
    if (root == nullptr) {
        return;
    }

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();

        cout << current->data << " ";

        if (current->left != nullptr) {
            q.push(current->left);
        }

        if (current->right != nullptr) {
            q.push(current->right);
        }
    }
}
```

---

## 📏 9. Height and Depth of a Tree

### Height

Height measures the number of edges on the longest path from a node down to a leaf.

Using the edge-based convention:

- A leaf has height `0`.
- An empty tree has height `-1`.
- A tree with one node has height `0`.

### C++ Code to Calculate Height

```cpp
int height(Node* root) {
    if (root == nullptr) {
        return -1;
    }

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + max(leftHeight, rightHeight);
}
```

Include `<algorithm>` to use `max()`.

### Depth

Depth measures the number of edges from the root to a node.

- The root has depth `0`.
- Its direct children have depth `1`.
- Their children have depth `2`.

### Why Height Matters

The height of a tree strongly influences the efficiency of searching, insertion, and deletion in a BST.

A balanced tree generally has logarithmic height, while a skewed tree can have linear height.

---

## ⚖️ 10. Balanced Trees and AVL Trees

### What Is a Balanced Tree?

A balanced tree controls its height to prevent long, inefficient paths.

A self-balancing BST automatically adjusts its structure after certain insertions or deletions.

### AVL Tree

An AVL tree is a self-balancing Binary Search Tree.

For every node, the balance factor is:

`Balance Factor = Height of Left Subtree - Height of Right Subtree`

For an AVL tree, the balance factor of every node must be `-1`, `0`, or `+1`.

### AVL Rotations

Four common imbalance cases are:

| Case | Correction |
|---|---|
| LL | Right rotation |
| RR | Left rotation |
| LR | Left rotation on the left child, then right rotation |
| RL | Right rotation on the right child, then left rotation |

### Why Use AVL Trees?

AVL trees maintain O(log n) search, insertion, and deletion time.

They are useful when predictable search performance is important.

### Red-Black Trees

Red-Black Trees maintain balance using node colors, rotations, and recoloring.

They guarantee O(log n) search, insertion, and deletion.

The exact balancing rules differ from AVL trees, and Red-Black Trees generally allow less strict balance.

---

## 🏔️ 11. Heap Data Structure

A Heap is a complete binary tree that satisfies a heap-ordering property.

### Min-Heap

Every parent is less than or equal to its children.

```text
          10
         /  \
        20   15
       / \
      30  40
```

The smallest element is at the root.

### Max-Heap

Every parent is greater than or equal to its children.

```text
          50
         /  \
        30   40
       / \
      10  20
```

The largest element is at the root.

### Common Heap Operations

| Operation | Time Complexity |
|---|---|
| Get minimum in min-heap | O(1) |
| Get maximum in max-heap | O(1) |
| Insert | O(log n) |
| Remove root | O(log n) |
| Build heap from an array | O(n) |

### Applications

- Priority queues
- Heap sort
- Task scheduling
- Graph algorithms such as Dijkstra's algorithm

In C++, `priority_queue` from the standard library provides a convenient max-heap by default.

---

## 🗃️ 12. B-Tree and B+ Tree

### B-Tree

A B-Tree is a balanced multiway search tree in which nodes can store multiple keys and have multiple children.

It is designed to reduce the number of storage accesses needed when working with large datasets.

### B+ Tree

A B+ Tree is a related structure in which records or record pointers are typically stored in leaf nodes, and internal nodes guide the search. Leaf nodes are commonly linked to support efficient range queries.

### Differences

| Feature | B-Tree | B+ Tree |
|---|---|---|
| Internal nodes | Can store keys and associated records or pointers | Primarily guide searches using keys and child pointers |
| Leaf nodes | Store keys and may store records | Store records or record pointers |
| Range queries | Supported | Particularly efficient due to linked leaves in common implementations |
| Typical use | Storage and indexing systems | Database and storage indexes |

Exact implementation details vary by database and storage system.

---

## 🔤 13. Trie Data Structure

A Trie, also called a prefix tree, stores strings by sharing common prefixes.

For example, consider the words:

- `car`
- `cat`
- `care`

They share the prefix `ca`, so a Trie can reuse nodes for the common characters.

### Applications

- Autocomplete
- Dictionary lookup
- Prefix searching
- Spell checking
- Word games

For a word of length `L`, a standard Trie can perform insertion and search in O(L) time, assuming constant-time child access.

Memory usage depends on the number of nodes and the child-storage representation.

---

## ⏱️ 14. Time Complexity Analysis

Let:

- `n` = number of nodes.
- `h` = height of the tree.

### Binary Search Tree

| Operation | Average for a balanced-shaped BST | Worst case |
|---|---|---|
| Search | O(log n) | O(n) |
| Insertion | O(log n) | O(n) |
| Deletion | O(log n) | O(n) |
| Find minimum/maximum | O(log n) | O(n) |
| Traversal | O(n) | O(n) |

The average-case figures assume a suitably balanced tree or typical insertion order. They are not guaranteed for every ordinary BST.

### Other Tree Structures

| Structure | Important performance property |
|---|---|
| AVL Tree | Search, insertion, and deletion are O(log n). |
| Red-Black Tree | Search, insertion, and deletion are O(log n). |
| Binary Heap | Root access O(1), insertion and root removal O(log n). |
| Trie | Search and insertion are typically O(L), where L is key length. |
| B-Tree | Search and updates take logarithmic time in the number of stored keys, with cost also depending on node capacity and storage access. |

### Traversal Complexity

Inorder, preorder, postorder, and level-order traversal each take O(n) time because every node is visited once.

Recursive traversals use O(h) auxiliary stack space. Level-order traversal can use O(n) queue space in the worst case.

---

## 🌍 15. Applications of Trees

Trees are widely used in computer science.

1. **File systems:** Represent folders and files hierarchically.
2. **Databases:** Use B-Trees and B+ Trees for indexing.
3. **Compilers:** Use syntax trees to represent program structure.
4. **Machine learning:** Use decision trees to make predictions.
5. **Networking:** Represent hierarchical routing or organization structures.
6. **Autocomplete:** Use Tries to search prefixes.
7. **Operating systems:** Use trees for some scheduling and resource-management structures.
8. **Priority queues:** Use heaps to retrieve the highest- or lowest-priority item efficiently.
9. **Search algorithms:** Use BSTs and balanced trees to maintain ordered data.
10. **Data compression:** Use Huffman trees to build variable-length codes.

---

## 💻 16. C++ Implementation

The following complete program demonstrates binary tree creation and traversal.

**File name:** `tree_traversal.cpp`

```cpp
#include <iostream>
#include <queue>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

void inorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

void postorder(Node* root) {
    if (root == nullptr) {
        return;
    }

    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

void levelOrder(Node* root) {
    if (root == nullptr) {
        return;
    }

    queue<Node*> q;
    q.push(root);

    while (!q.empty()) {
        Node* current = q.front();
        q.pop();

        cout << current->data << " ";

        if (current->left != nullptr) {
            q.push(current->left);
        }

        if (current->right != nullptr) {
            q.push(current->right);
        }
    }
}

int main() {
    Node* root = new Node(1);

    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);

    cout << "Inorder: ";
    inorder(root);

    cout << "\nPreorder: ";
    preorder(root);

    cout << "\nPostorder: ";
    postorder(root);

    cout << "\nLevel Order: ";
    levelOrder(root);

    cout << '\n';

    return 0;
}
```

### Expected Output

```text
Inorder: 4 2 5 1 3
Preorder: 1 2 4 5 3
Postorder: 4 5 2 3 1
Level Order: 1 2 3 4 5
```

This program demonstrates traversal, not BST insertion, searching, or deletion. Those operations can be added as separate exercises.

---

## ⚙️ 17. How to Run the Code

### Prerequisites

- A C++ compiler such as GCC or MinGW.
- Visual Studio Code or another C++ editor.

### Step 1: Save the File

Save the program as `tree_traversal.cpp`.

### Step 2: Compile the Program

Open a terminal in the folder containing the source file and run:

```bash
g++ tree_traversal.cpp -o tree_traversal
```

### Step 3: Run on Windows

```bash
tree_traversal.exe
```

On Linux or macOS:

```bash
./tree_traversal
```

The program should print the four traversal sequences shown above.

---

## ❓ 18. Common Interview Questions

### Beginner Level

1. What is a tree data structure?
2. What is the difference between a linear and a non-linear data structure?
3. What is the difference between a binary tree and a BST?
4. What are leaf nodes?
5. What is tree traversal?
6. Explain inorder, preorder, and postorder traversal.
7. What is the height of a tree?

### Intermediate Level

1. How do you insert a node into a BST?
2. How do you search for an element in a BST?
3. Explain the three cases of BST deletion.
4. How do you find the minimum and maximum in a BST?
5. How do you calculate tree height?
6. How does level-order traversal work?
7. Why can a BST become skewed?
8. What is the difference between a heap and a BST?

### Advanced Level

1. What is an AVL tree?
2. Explain LL, RR, LR, and RL rotations.
3. How does a Red-Black Tree maintain balance?
4. What are the differences between B-Trees and B+ Trees?
5. What is a Trie, and where is it used?
6. How can you check whether a binary tree is a valid BST?
7. How do you find the lowest common ancestor of two nodes?
8. How can you construct a tree from traversal sequences?

---

## 🗺️ 19. Learning Roadmap

Follow this order to learn tree data structures effectively.

### Level 1: Fundamentals

- Understand nodes, edges, root, leaves, height, and depth.
- Learn binary tree representation.
- Practice recursive functions.

### Level 2: Traversals

- Inorder traversal
- Preorder traversal
- Postorder traversal
- Level-order traversal

### Level 3: Binary Search Trees

- Insertion
- Searching
- Minimum and maximum
- Deletion
- Validate BST
- Calculate height

### Level 4: Advanced Binary Trees

- AVL trees
- Red-Black Trees
- Tree balancing
- Lowest common ancestor
- Diameter of a binary tree

### Level 5: Specialized Trees

- Min-heap and max-heap
- B-Tree and B+ Tree
- Trie
- Segment tree
- Fenwick tree

**Recommended learning strategy:** Start with binary tree creation and traversals. Then learn BST operations before moving on to balanced trees and specialized structures.

---

⭐ If this guide helps you understand tree data structures, consider giving the repository a star on GitHub.
