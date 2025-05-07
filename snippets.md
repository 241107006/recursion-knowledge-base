## Snippet 1: What is Recursion?

Recursion is a method where a function calls itself to solve smaller instances of a problem.

```python
def factorial(n):
    return 1 if n == 0 else n * factorial(n - 1)
```

---

## Snippet 2: Base and Recursive Cases

Every recursive function needs:
- A base case to stop recursion.
- A recursive case to solve smaller subproblems.

```python
def countdown(n):
    if n == 0:
        return
    countdown(n - 1)
```

---

## Snippet 3: Call Stack Behavior

Recursive calls are stored on the call stack. When the base case is hit, the stack unwinds in LIFO order.

```python
def greet(n):
    if n == 0:
        return
    print("Hello")
    greet(n - 1)
```

---

## Snippet 4: Recursion vs Iteration

Recursion can simplify code but may use more memory than loops. Use iteration for simple loops, recursion for divide-and-conquer.

---

## Snippet 5: What is Backtracking?

Backtracking is a form of recursion where we abandon a path if it violates constraints.

```python
def permute(path, options):
    if not options:
        print(path)
    for i in range(len(options)):
        permute(path + [options[i]], options[:i] + options[i+1:])
```

---

## Snippet 6: N-Queens Backtracking

Try placing queens row by row and backtrack if placement is invalid.

```python
def solve(board, row):
    if row == len(board): return True
    for col in range(len(board)):
        if is_safe(board, row, col):
            board[row] = col
            if solve(board, row + 1): return True
            board[row] = -1  # backtrack
```

---

## Snippet 7: Pruning in Backtracking

Pruning cuts off branches that can’t lead to a valid solution, improving efficiency.

```python
if not is_valid(partial_solution):
    return  # prune
```

---

## Snippet 8: Recursive Tree Visualization

Recursive problems can often be visualized as trees where each node represents a function call.

---

## Snippet 9: Memoization with Recursion

Memoization caches results to avoid redundant calculations.

```python
@lru_cache(None)
def fib(n):
    return n if n < 2 else fib(n-1) + fib(n-2)
```

---

## Snippet 10: Classic Recursive Problems

Common examples: factorial, Fibonacci, binary search, tree traversal, permutations, N-Queens.