## Problem 1: Climbing Stairs (Ladder Problem)

**Problem**:  
You are climbing a ladder with `n` steps. You can climb either 1 or 2 steps at a time. How many distinct ways can you climb to the top?

**Idea**:  
This is a classic recursive problem similar to computing Fibonacci numbers:  
To reach step `n`, you could have come from `n-1` or `n-2`.

**Hint**:  
Base cases: 1 way to climb 1 step, 2 ways to climb 2 steps.

**Solution**:
```python
def climb_stairs(n):
    if n <= 1:
        return 1
    return climb_stairs(n - 1) + climb_stairs(n - 2)
```

---

## Problem 2: Sum of Digits (Recursive)

**Problem**:  
Write a recursive function to calculate the sum of digits of a non-negative integer `n`.

**Idea**:  
Peel off the last digit and add it to the sum of the remaining digits.

**Hint**:  
Use modulo `%` and integer division `//` to split digits.

**Solution**:
```python
def sum_of_digits(n):
    if n == 0:
        return 0
    return n % 10 + sum_of_digits(n // 10)
```

---

## Problem 3: Word Search in a Grid

**Problem**:  
Given a 2D board of characters and a word, check if the word exists in the grid. The word can be formed by sequentially adjacent cells.

**Idea**:  
Use DFS with backtracking from every cell that matches the first letter.

**Hint**:  
Mark visited cells temporarily and restore them on backtrack.

**Solution**:
```python
def exist(board, word):
    rows, cols = len(board), len(board[0])

    def backtrack(i, j, k):
        if k == len(word):
            return True
        if i < 0 or i >= rows or j < 0 or j >= cols or board[i][j] != word[k]:
            return False
        temp = board[i][j]
        board[i][j] = '#'  # mark visited
        found = (
            backtrack(i + 1, j, k + 1) or
            backtrack(i - 1, j, k + 1) or
            backtrack(i, j + 1, k + 1) or
            backtrack(i, j - 1, k + 1)
        )
        board[i][j] = temp  # unmark
        return found

    for i in range(rows):
        for j in range(cols):
            if backtrack(i, j, 0):
                return True
    return False
```

---

## Problem 4: Sudoku Solver

**Problem**:  
Write a program to solve a Sudoku puzzle by filling empty cells (represented by '.') with digits `1-9`, ensuring each row, column, and 3x3 box contains each digit exactly once.

**Idea**:  
Use backtracking to fill cells. Try digits one by one, and backtrack if constraints are violated.

**Hint**:  
Validate row, column, and box constraints before placing a digit.

**Solution**:
```python
def solve_sudoku(board):
    def is_valid(r, c, ch):
        for i in range(9):
            if board[i][c] == ch or board[r][i] == ch:
                return False
            box_r, box_c = 3 * (r // 3) + i // 3, 3 * (c // 3) + i % 3
            if board[box_r][box_c] == ch:
                return False
        return True

    def backtrack():
        for r in range(9):
            for c in range(9):
                if board[r][c] == '.':
                    for ch in '123456789':
                        if is_valid(r, c, ch):
                            board[r][c] = ch
                            if backtrack():
                                return True
                            board[r][c] = '.'  # backtrack
                    return False
        return True

    backtrack()
```