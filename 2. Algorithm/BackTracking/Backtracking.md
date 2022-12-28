https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)

Subset - permutations - combination sum - palindrome portioning



### Backtracking

* [Backtracking](https://en.wikipedia.org/wiki/Backtracking) is a general algorithm for finding all (or some) solutions to some computational problems (notably Constraint satisfaction problems or CSPs).
* The idea is that it incrementally **builds** candidates to the solutions, and **abandons** a candidate ("backtrack") **as soon as** it determines that this candidate cannot lead to a final solution.
* Backtracking algorithms are often much **faster** than the brute force search algorithm, since it eliminates many unnecessary explocation.
  * **Pruning(裁剪)** the recursion tree

* like **DFS** -- tree traversal
* Using **recursion**

#### Template

```pseudocode
public void backtracking() {

	if (find solution) {
      res.add();
      return;
	}
	
	for (iterate all possible candidates) {
			if (isValid) {
        change state;

        backtracking(next);

        revert state;
			}
	}
}
```



##### Example 1 N -- Queen puzzle

[52. N-Queens II](https://leetcode.com/problems/n-queens-ii)

[51. N-Queens](https://leetcode.com/problems/n-queens)

```java
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```

* The function is implemented as **recursion**.
* At each occurrence of recursion, the functino is **one step further** to the final solution
* Within the recursion, we have an iteration that allows us to explore all the **candidates** that are of the same progress to the final solution
* The **backtracking** should **happen at the level of the iteration** within the recursion. 
* Unlike brute-force search, in backtracking algorithms we are often able to determine if a partial solution candidate is worth exploring further (*i.e.* `is_valid(next_candidate)`), which allows us to **prune the search zones**. This is also known as the constraint, *e.g.* the attacking zone of queen in N-queen game.

* There are two symmetric functions that allow us to **mark the decision** (`place(candidate)`) and **revert the decision** (`remove(candidate)`). 

[489. Robot Room Cleaner](https://leetcode.com/problems/robot-room-cleaner)

[37. Sudoku Solver](https://leetcode.com/problems/sudoku-solver)

















###### 39 - Combination Sum

* we could *incrementally* build the combination, and once we find the current combination is not valid, we ***backtrack*** and **try another option**.
* An important detail on choosing the next number for the combination is that we select the candidates **in order**, where the total candidates are treated as a list. Once a candidate is added into the current combination, we will not **look back** to all the previous candidates in the next explorations.



###### 216 - Combination Sum III





- [Subsets](https://leetcode.com/problems/subsets)
- [Subsets II](https://leetcode.com/problems/subsets-ii)
- [Permutations](https://leetcode.com/problems/permutations/)
- [Permutations II](https://leetcode.com/problems/permutations-ii/)
- [Combinations](https://leetcode.com/problems/combinations/)
- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
- [Combination Sum III](https://leetcode.com/problems/combination-sum-iii/)
- [Palindrome Partition](https://leetcode.com/problems/palindrome-partitioning/)