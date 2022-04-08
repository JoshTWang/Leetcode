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

