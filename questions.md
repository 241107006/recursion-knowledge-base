## Question 1

**Q**: What is a base case in recursion?

**A**: It's the condition that stops the recursive calls, preventing infinite loops and triggering the function to start returning.

---

## Question 2

**Q**: What happens if a recursive function does not have a base case?

**A**: The function will keep calling itself indefinitely, leading to a stack overflow error.

---

## Question 3

**Q**: How is backtracking different from simple recursion?

**A**: Backtracking explores all possible solutions by trying options and undoing choices (backtracking) when a path leads to an invalid state, whereas simple recursion doesn’t necessarily undo steps.

---

## Question 4

**Q**: Why is the N-Queens problem often solved using backtracking?

**A**: Because it requires trying many configurations while pruning invalid ones early, which is exactly what backtracking is designed to do.

---

## Question 5

**Q**: What is the main drawback of recursive algorithms without memoization?

**A**: They may recompute the same subproblems repeatedly, leading to exponential time complexity in some cases (e.g., Fibonacci).