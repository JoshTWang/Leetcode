#### Divide and conquer(D & C)

* A **divide and conquer** algorithm works by **recursively** breaking the problem down into **two or more subproblems** of the same or related type, until these subproblems become simple enough to be solve directly. Then one **combines** the results of subproblems to form the final solution.

###### Steps

1. **Divide.** Divide the problem {S} into a set of subproblems: {*S*1,*S*2,...*Sn*} where n*≥2, *i.e.* there are usually more than one subproblem.

2. **Conquer.** Solve each subproblem recursively. 

3. **Combine.** Combine the results of each subproblem.

![img](https://assets.leetcode.com/uploads/2019/04/24/d_c.png)

#### Classic examples

* Merge sort
* Quick Sort
* Binary Tree Recursion



#### Template

```python
def divide_and_conquer( S ):
    # (1). Divide the problem into a set of subproblems.
    [S1, S2, ... Sn] = divide(S)

    # (2). Solve the subproblem recursively,
    #   obtain the results of subproblems as [R1, R2... Rn].
    rets = [divide_and_conquer(Si) for Si in [S1, S2, ... Sn]]
    [R1, R2,... Rn] = rets

    # (3). combine the results from the subproblems.
    #   and return the combined result.
    return combine([R1, R2,... Rn])
```



#### Divide and conquer vs. Backtracking

1. Often the case, the divide-and-conquer problem has a **sole** solution, while the backtracking problem has **unknown** number of solutions. 

   * For example, when we apply the merge sort algorithm to sort a list, we obtain a single sorted list, 

   * while there are many solutions to place the queens for the N-queen problem.

2. Each step in the divide-and-conquer problem is **indispensable** to build the final solution, while many steps in backtracking problem might not be useful to build the solution, but serve as **attempts** to search for the potential solutions.

   *  For example, each step in the merge sort algorithm, *i.e.* divide, conquer and combine, are all indispensable to build the final solution, 
   * while there are many trials and errors during the process of building solutions for the N-queen problem.

3. When building the solution in the divide-and-conquer algorithm, we have a **clear and predefined** path, though there might be several different manners to build the path. While in the backtracking problems, one does not know in advance the **exact path** to the solution. 

   * For example, in the top-down merge sort algorithm, we first recursively divide the problems into two subproblems and then combine the solutions of these subproblems. The steps are clearly defined and the number of steps is fixed as well. 
   * While in the N-queen problem, if we know exactly where to place the queens, it would only take N steps to do so. When applying the backtracking algorithm to the N-queen problem, we try many candidates and many of them do not eventually lead to a solution but abandoned at the end. As a result, we do not know beforehand how many steps exactly it would take to build a valid solution. 
