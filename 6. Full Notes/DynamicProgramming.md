when looking to solve a dynamic programming question
1. Define the subproblem
2. Whats the base case
3. Find recusrive formula for general solution


More than likely you are going to solve the same problem multiple times, memoize the results of each sub problem to increase time efficency
```
python

memo = {}
def SomeRecursive(n):

  if answer in memo:
    return memo[answer]

logic....


```
