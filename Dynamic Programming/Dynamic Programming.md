### DP

Dynamic Programming(DP) is a programming paradigm that can systematically and efficiently explore **all** possible solutions to a problem.As such, it is capable of solving a wide variety of problems that often have the following characteristics:

1. The problem can be broken down into "**overlapping** subproblems" - smaller versions of the original problem that are **re-used** multiple times.
2. The problem has an "**optimal substructure**" - an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem.

##### DP vs. Greedy vs. D&C

* Greedy problems have **optimal substructure**, but not overlapping subproblems. 
* Divide and conquer algorithms break a problem into subproblems, but these subproblems are **not overlapping** 
  * Divide and conquer approaches can be **parallelized** while dynamic programming approaches cannot be (easily) parallelized. This is because the subproblems in divide an conquer approaches are **independent** of one another (they do not overlap) while in dynamic programming, the subproblems do **overlap**.

##### Fibonacci sequence

* Brute force -- exponential time
* DP -- linear time

---

### Top-down vs. Bottom up

* Bottom up also known as **tabulation**
* Top down also known as **memoization**

##### Bottom up

* Bottom up is implemented with **iteration** and starts at the base case.
* A bottom-up implementation's runtime is usually **faster**, as iteration does not have the overhead that recursion does.

```pseudocode
// Pseudocode example for bottom-up

F = array of length (n + 1)
F[0] = 0
F[1] = 1
for i from 2 to n:
    F[i] = F[i - 1] + F[i - 2]
```

##### Top down

* Top down is implemented with **recursion** and made efficient with **memoization**.

* **memoizing** a result means to store the result of a function call, usually in a **hashmap** or an **array**, so that when the same function call is made again, we can simply **return the memoized result** instead of recalculating the result.
* A top-down implementation is usually much **easier to write**. This is because with recursion, the **ordering** of subproblems does not matter, whereas with tabulation, we need to go through a logical ordering of solving subproblems.

```pseudocode
// Pseudocode example for top-down

memo = hashmap
Function F(integer i):
    if i is 0 or 1: 
        return i
    if i doesn't exist in memo:
        memo[i] = F(i - 1) + F(i - 2)
    return memo[i]
```

---

#### When to use DP

##### Characteristic 1 --- Greedy or DP

* The problem will ask for the optimum value (**maximum** or **minimum**) of something, or the **number of ways** there are to do something. 

  - What is the **minimum** cost of doing...

  - What is the **maximum** profit from...

  - How many **ways** are there to do...

  - What is the **longest** possible...

  - Is it possible to reach a **certain** point...

##### Characteristic 2 --- DP

* **Future "decisions" depend on earlier decisions**. 

* Deciding to do something at one step may affect the ability to do something in a later step. 
* If the problem has constraints that cause decisions to affect other decisions, such as using one element **prevents** the usage of other elements, then we should consider using dynamic programming to solve the problem. 

###### Two examples

[House Robber](https://leetcode.com/problems/house-robber/)

[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)



#### Framework for DP

##### state

* In a DP problem, a state is a set of variables that can sufficiently describe a scenario.

* These variables are called **state variables**

##### 3 things to combine

1. **A function or data structure that will compute/contain the answer to the problem for every given state**.
   * Typically, top-down is implemented with a **recursive function** and **hash map**, whereas bottom-up is implemented with **nested for loops** and an **array**.
   * When designing this function or array, we also need to decide on **state variables to pass as arguments.** 
   * This problem is very simple, so all we need to describe a state is to know what step we are currently on i.

2. **A recurrence relation to transition between states.**
   * Information about some states gives us information about other states.
   * Finding the **recurrence relation** is the most difficult part of solving a DP problem.

3. **Base cases, so that our recurrence relation doesn't go on infinitely.**



#### Multidimensional DP

* The dimensions of a DP algorithm refer to the number of state variables used to define each state.
* Problems that require multiple dimensions

##### state variable

* An **index** along some input.
  * An input is given as an array or string

* A **second** index along some input
  * dp(1,3) -- start and end index
* Explicit numerical **constraints**
  * you are only allowed to complete k transactions
* Variables that describe statuses in a given state
  * true or false holding a key
* Some sort of data like a tuple
  * **Visited** or **used**



#### Top down to bottom up

1. Start with a completed top-down implementation.

2. Initialize an **array** dp that is sized according to your state variables. 
   * For example, let's say the input to the problem was an array nums and an integer k that represents the maximum number of actions allowed. Your array dp would be **2D** with one dimension of length nums.length and the other of length k. 
   * The values should be initialized as some default value opposite of what the problem is asking for. For example, if the problem is asking for the **maximum** of something, set the values to **negative infinity**. If it is asking for the minimum of something, set the values to infinity.

3. Set your base cases
4. Write a for-loop
   * If you have multiple state variables, you will need nested for-loops.
   * These loops should **start iterating from the base cases**.

5. Each iteration of the **inner-most loop** represents a given **state**. Change dp() into dp[]





#### Time and Space Complexity

* We only compute each state once

* If we had 3 state variables: i, k and holding for some made up problem
  * i is an integer used to keep track of an index for an input array nums
  * k is an integer represents the maximum actions
  * holding is a Boolean variable
  * O(n * K * 2)
* In many DP problems, there are optimizations that can inprove both complexities.



#### State Reduction

* State reduction usually comes from a clever trick or observation.
* It can result in lower time and space complexity.
* State reductions for **space** complexity usually only apply to **bottom-up** implementations, while improving **time** complexity by reducing the number of state variables applies to **both** implementations.

[1770. Maximum Score from Performing Multiplication Operations](https://leetcode.com/problems/maximum-score-from-performing-multiplication-operations)

* We could use 2 state variables instead of 3 because we could derive the information the 3rd one would have given us from the other 2. (left, i --> right)

[198. House Robber](https://leetcode.com/problems/house-robber)

* We could adding an extra boolean state variable `prev` that indicates if we robbed the previous house or not.

[509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number)

* Save **space complexity**
* To calculate the ith Fibonacci number, we only ever care about the previous two numbers, that means if we are using a bottom up approach and start from the base cases, we don't actually need to use an array and remember every single Fibonacci number

##### Advice

* The best advice is to try and think if any of the state variables are related to each other, and if an equation can be created among them. 
* If a problem **does not require iteration**, there is usually some form of state reduction possible.