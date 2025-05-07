# 📘 Topic: Recursion and Backtracking

## 🧠 Overview

Recursion and backtracking are foundational algorithmic techniques. Recursion allows a function to call itself to solve smaller subproblems, while backtracking builds on recursion to explore multiple possibilities and "backtrack" when constraints are violated.

These techniques are widely used in problems involving trees, permutations, combinations, puzzles, and constraint satisfaction.

For example, the most popular problem solved using recursion is Fibonacci number, where each number is a sum of previous 2 numbers.

---

## 🔁 Recursion

### What is Recursion?

Recursion is when a function calls itself to solve a smaller instance of the same problem.

A recursive function must have:

- **Base case** – stops the recursion.
- **Recursive case** – breaks the problem down into simpler versions.

### Example: Factorial

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

### Call Stack Behavior

Each recursive call is added to the call stack. Once the base case is reached, the stack begins to unwind, returning values back up the chain.

In the above example you can see a factorial function. The function returns factorial which is F(n)=1 * 2 * 3 * ... * n. Function multiplies each number until it gets to 1.

---

### When to Use Recursion

- Natural hierarchical structure (e.g., trees).
- Repetitive tasks with smaller inputs (e.g., divide and conquer).
- Problems reducible to similar subproblems (e.g., Fibonacci, Tower of Hanoi).

---

## 🧮 Step-by-Step: Writing a Fibonacci Function (Recursion)

The Fibonacci sequence is defined as:
```
F(0) = 0
F(1) = 1
F(n) = F(n-1) + F(n-2)
```

### Step 1: Understand the base cases
Fibonacci has two base cases:
- If `n == 0`, return `0`
- If `n == 1`, return `1`

### Step 2: Express the recurrence
Each Fibonacci number is the **sum** of the previous two:
```python
F(n) = F(n - 1) + F(n - 2)
```

### Step 3: Write the code
```python
def fibonacci(n):
    if n == 0:
        return 0  # Base case
    if n == 1:
        return 1  # Base case
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### Step 4: Test and visualize
Call `fibonacci(5)`:
```
fibonacci(5) 
= fibonacci(4) + fibonacci(3)
= (fibonacci(3) + fibonacci(2)) + (fibonacci(2) + fibonacci(1))
...
```

This creates a tree of recursive calls. Each level computes smaller subproblems.

### Step 5: Optimize (Optional - Memoization)
The recursive solution repeats work. Add caching to improve:
```python
def fibonacci(n, memo={}):
    if n in memo:
        return memo[n]
    if n == 0:
        return 0
    if n == 1:
        return 1
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]
```

---

## 🔍 Analyzing Recursion

Recursive time complexity is often expressed with **recurrence relations**.

**Example**: Merge Sort

```
T(n) = 2T(n/2) + O(n)
```

Using the **Master Theorem**:
- If `T(n) = aT(n/b) + O(n^d)`
- Compare `d` and `log_b(a)` to find time complexity.

For Merge Sort: `a = 2`, `b = 2`, `d = 1` ⇒ `T(n) = O(n log n)`

---

## 🔙 Backtracking

Backtracking is an extension of recursion used to build solutions incrementally, abandoning ("backtracking") a path when it violates a constraint.

Used for:
- Combinatorial problems (e.g., permutations, subsets).
- Constraint satisfaction (e.g., N-Queens, Sudoku).
- Puzzles (e.g., maze solvers).

### Example: Generate All Subsets

```python
def subsets(nums):
    result = []
    def backtrack(index, path):
        if index == len(nums):
            result.append(path[:])
            return
        path.append(nums[index])
        backtrack(index + 1, path)
        path.pop()
        backtrack(index + 1, path)
    backtrack(0, [])
    return result
```

In the above example the function generates subsets from a given array. The function in each iteration takes both option of taking the current number and not taking it. Which explores all possible subsets.

---

### ♟️ Step-by-Step: Writing a Backtracking Algorithm (Simplified N-Queens)

Let’s solve a **mini-version** of the N-Queens problem: place 2 Queens on a 2x2 board such that no two queens attack each other.

#### Step 1: Understand the constraints
Queens attack along:
- Same row
- Same column
- Diagonals

So, we need to **only allow valid placements**.

#### Step 2: Define the board
Use a 2D array or a list to track queen positions.

```python
board = [[0, 0], [0, 0]]
```

#### Step 3: Create helper to check safety
```python
def is_safe(board, row, col):
    for i in range(row):
        if board[i][col]:  # Same column
            return False
    for i, j in zip(range(row - 1, -1, -1), range(col - 1, -1, -1)):
        if board[i][j]:  # Left diagonal
            return False
    for i, j in zip(range(row - 1, -1, -1), range(col + 1, 2)):
        if board[i][j]:  # Right diagonal
            return False
    return True
```

#### Step 4: Write backtracking function
```python
def solve(board, row):
    if row == 2:
        print("Solution:")
        for r in board:
            print(r)
        return

    for col in range(2):
        if is_safe(board, row, col):
            board[row][col] = 1  # Place queen
            solve(board, row + 1)
            board[row][col] = 0  # Backtrack
```

#### Step 5: Call it
```python
board = [[0, 0], [0, 0]]
solve(board, 0)
```

#### Output:
```
Solution:
[1, 0]
[0, 1]

Solution:
[0, 1]
[1, 0]
```

We found two valid arrangements where queens don't attack each other.

---

## ✂️ Pruning and Optimization

To make backtracking efficient:
- **Prune** branches early that cannot lead to valid solutions.
- Use **constraints** to reduce the search space.

---

## 💡 Recursion vs Backtracking

| Feature       | Recursion                                | Backtracking                                      |
|---------------|-------------------------------------------|---------------------------------------------------|
| Purpose       | Solve a problem by breaking into subparts | Explore all solutions and backtrack on failures   |
| Control Flow  | One recursive path at a time              | Tries all paths using recursion + backtracking    |
| Use Case      | Mathematical problems, divide & conquer   | Permutations, constraint problems, puzzles        |

---

## 🧩 Key Takeaways

- Recursion solves problems by dividing into subproblems.
- Backtracking explores all valid configurations.
- Prune early to improve efficiency.
- Many problems in algorithms use these patterns.
