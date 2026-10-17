# Backtracking in C++

A beginner-friendly guide to learning Backtracking with simple explanations, algorithms, C++ programs, examples, and practice questions.

## 1. What is Backtracking?

**Backtracking** is an algorithmic technique used to solve problems by trying different possible solutions step by step.

If a choice leads to an incorrect solution, the algorithm goes back to the previous step and tries another choice.

In simple words:

1. Make a choice.
2. Check whether the choice is valid.
3. If valid, continue solving the problem.
4. If it leads to a dead end, undo the choice.
5. Try another possibility.

This process is called **choose, explore, and undo**.

## 2. Real-Life Example

Imagine you are solving a maze.

You start at the entrance and move forward.

If you reach a dead end:
- Go back to the previous position.
- Choose another path.
- Continue until you reach the exit.

This is exactly how backtracking works.

## 3. What is Recursion?

Recursion is a programming technique in which a function calls itself.

Backtracking commonly uses recursion to explore different possibilities.

Example:

```cpp
#include <iostream>
using namespace std;

void countDown(int n) {
    if (n == 0) {
        return;
    }

    cout << n << " ";
    countDown(n - 1);
}

int main() {
    countDown(5);
    return 0;
}
```

Output:

```text
5 4 3 2 1
```

The function keeps calling itself with a smaller value until it reaches the base condition.

## 4. Difference Between Recursion and Backtracking

| Recursion | Backtracking |
|---|---|
| A function calls itself | Uses recursion or another search strategy to explore choices |
| Does not always involve undoing choices | Usually undoes a choice when it fails |
| Used for factorial, Fibonacci, tree traversal | Used for maze solving, N-Queens, Sudoku |

Backtracking is often implemented using recursion, but recursion alone is not backtracking.

## 5. How Backtracking Works

The general algorithm follows these steps:

```text
Backtracking(problem):

    If the problem is solved:
        Return success

    For each possible choice:
        If the choice is valid:
            Make the choice

            If Backtracking(problem) succeeds:
                Return success

            Undo the choice

    Return failure
```

The most important step is **undoing the choice**.

Without undoing the choice, the algorithm cannot properly explore alternative paths.

## 6. First Backtracking Program: Generate All Subsets

A subset is a collection of elements selected from a given set.

For example, for the array:

```text
[1, 2]
```

All possible subsets are:

```text
[]
[1]
[2]
[1, 2]
```

At each position, we have two choices:

- Include the current element.
- Exclude the current element.

### C++ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void generateSubsets(vector<int>& arr,
                     vector<int>& current,
                     int index) {

    // Base case
    if (index == arr.size()) {
        cout << "[ ";

        for (int value : current) {
            cout << value << " ";
        }

        cout << "]" << endl;
        return;
    }

    // Choice 1: Include the current element
    current.push_back(arr[index]);

    generateSubsets(arr, current, index + 1);

    // Backtrack: Remove the current element
    current.pop_back();

    // Choice 2: Exclude the current element
    generateSubsets(arr, current, index + 1);
}

int main() {
    vector<int> arr = {1, 2, 3};
    vector<int> current;

    generateSubsets(arr, current, 0);

    return 0;
}
```

### Explanation

For every element, the algorithm explores two possibilities.

```text
                  []
               /    \
          Include  Exclude
            /        \
          [1]         []
```

The algorithm continues until all elements have been considered.

The `push_back()` function adds an element to the current subset.

The `pop_back()` function removes that element before exploring the next possibility.

This is the backtracking step.

## 7. Understanding the Backtracking Code

### Base Case

```cpp
if (index == arr.size()) {
    // Print the subset
    return;
}
```

The base case stops recursion when every element has been considered.

### Making a Choice

```cpp
current.push_back(arr[index]);
```

The current element is included in the subset.

### Exploring the Choice

```cpp
generateSubsets(arr, current, index + 1);
```

The function moves to the next element.

### Undoing the Choice

```cpp
current.pop_back();
```

The element is removed so that the next possibility can be explored without the previous choice.

This process is called backtracking.

## 8. Important Backtracking Problems

### A. Rat in a Maze

The rat must move from the starting cell to the destination in a maze.

The algorithm:
1. Starts from the first cell.
2. Checks possible directions.
3. Moves only to valid cells.
4. Marks the current cell as visited.
5. Backtracks if no valid path is available.

Typical constraints:
- Cannot move outside the maze.
- Cannot enter blocked cells.
- Cannot visit the same cell repeatedly in a path.

### B. N-Queens Problem

The N-Queens problem requires placing N queens on an N × N chessboard so that no two queens attack each other.

A queen can attack:
- Horizontally.
- Vertically.
- Diagonally.

The algorithm places one queen in each row.

If a position is safe:
- Place the queen.
- Move to the next row.

If the next row has no safe position:
- Remove the previously placed queen.
- Try another column.

### C. Sudoku Solver

The Sudoku problem requires filling a 9 × 9 grid.

Each row, column, and 3 × 3 box must contain digits from 1 to 9 without repetition.

The algorithm:
1. Finds an empty cell.
2. Tries digits from 1 to 9.
3. Checks whether a digit is valid.
4. Places the digit if valid.
5. Continues recursively.
6. Removes the digit if it leads to an invalid solution.

### D. Permutations

A permutation is an arrangement of elements in a particular order.

For example, the permutations of `[1, 2, 3]` include:

```text
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

Backtracking generates each possible arrangement by choosing an unused element at each position.

## 9. N-Queens Problem: Complete C++ Program

This program solves the N-Queens problem for a given board size.

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(vector<vector<int>>& board,
             int row, int col, int n) {

    // Check the same column above
    for (int i = 0; i < row; i++) {
        if (board[i][col] == 1) {
            return false;
        }
    }

    // Check upper-left diagonal
    for (int i = row - 1, j = col - 1;
         i >= 0 && j >= 0; i--, j--) {

        if (board[i][j] == 1) {
            return false;
        }
    }

    // Check upper-right diagonal
    for (int i = row - 1, j = col + 1;
         i >= 0 && j < n; i--, j++) {

        if (board[i][j] == 1) {
            return false;
        }
    }

    return true;
}

bool solveNQueens(vector<vector<int>>& board,
                  int row, int n) {

    // All queens have been placed
    if (row == n) {
        return true;
    }

    // Try every column in the current row
    for (int col = 0; col < n; col++) {

        if (isSafe(board, row, col, n)) {

            // Make the choice
            board[row][col] = 1;

            // Explore the next row
            if (solveNQueens(board, row + 1, n)) {
                return true;
            }

            // Undo the choice
            board[row][col] = 0;
        }
    }

    return false;
}

int main() {
    int n = 4;

    vector<vector<int>> board(
        n, vector<int>(n, 0)
    );

    if (solveNQueens(board, 0, n)) {

        cout << "Solution:" << endl;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                cout << board[i][j] << " ";
            }

            cout << endl;
        }

    } else {
        cout << "No solution exists." << endl;
    }

    return 0;
}
```

### Sample Output

One possible solution for a 4 × 4 board:

```text
Solution:
0 1 0 0
0 0 0 1
1 0 0 0
0 0 1 0
```

Here, `1` represents a queen and `0` represents an empty cell.

The program places one queen in each row and checks whether the column and diagonal positions are safe.

## 10. Backtracking vs Brute Force

| Brute Force | Backtracking |
|---|---|
| Tries all possible combinations | Stops exploring a path as soon as it becomes invalid |
| May perform unnecessary work | Prunes invalid paths early |
| Often slower for constraint problems | Can be significantly faster when pruning is effective |

Backtracking does not always guarantee a faster solution. In the worst case, it may still explore an exponential number of possibilities.

## 11. Time Complexity

Backtracking time complexity depends on the problem.

| Problem | Typical Worst-Case Complexity |
|---|---|
| Generate all subsets | O(2ⁿ × n) including copying or printing subsets |
| Generate all permutations | O(n × n!) including output construction |
| N-Queens | O(n!) as a common upper-bound description for row-by-row search with column constraints; safety checks add overhead |
| Sudoku | O(9ᵐ), where m is the number of empty cells, as a loose upper bound |

These are upper bounds, not exact running times for every input. Pruning can reduce the amount of search significantly.

## 12. Common Mistakes Beginners Make

1. Forgetting the base condition.
2. Not undoing a choice after recursive exploration.
3. Checking only one direction in a maze or board problem.
4. Forgetting to mark visited cells.
5. Not restoring the original state after a failed choice.
6. Returning success before all required conditions are satisfied.
7. Confusing recursion with backtracking.
8. Assuming every backtracking problem has the same time complexity.

## 13. Practice Questions

### Beginner Level

1. Generate all subsets of an array.
2. Generate all binary strings of length N.
3. Print all combinations of numbers from 1 to N.
4. Generate all permutations of a string.
5. Find all paths in a simple maze.

### Intermediate Level

6. Solve the Rat in a Maze problem.
7. Solve the N-Queens problem.
8. Generate combinations whose sum equals a target.
9. Find all possible valid parentheses.
10. Solve a Sudoku puzzle.

### Advanced Level

11. Word Search in a 2D grid.
12. Hamiltonian Path problem.
13. Knight's Tour problem.
14. Graph coloring problem.
15. Partition an array into subsets with equal sum.

## 14. Applications of Backtracking

Backtracking is useful in:

- Puzzle solving.
- Chess and board games.
- Path finding.
- Constraint satisfaction problems.
- Generating permutations and combinations.
- Scheduling and allocation problems.
- Finding possible arrangements.

## 15. How to Compile and Run

Save the code in a file named `main.cpp`.

Using the GCC compiler:

```bash
g++ main.cpp -o backtracking
```

Run on Windows:

```bash
backtracking.exe
```

Run on Linux or macOS:

```bash
./backtracking
```

## 16. Key Takeaways

- Backtracking explores possible solutions step by step.
- It uses the choose, explore, and undo approach.
- Recursion is commonly used to implement backtracking.
- Invalid paths are abandoned early through pruning.
- The base case determines when a solution is complete.
- Undoing a choice is the most important part of backtracking.
- N-Queens, Sudoku, permutations, and maze solving are classic examples.

**Beginner Tip:** Before writing the code, draw a recursion tree and trace the choices on paper. Understanding when to make a choice and when to undo it is the key to mastering backtracking.
