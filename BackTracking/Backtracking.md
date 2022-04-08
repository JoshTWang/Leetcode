### Backtracking

* As a reminder, [backtracking](https://en.wikipedia.org/wiki/Backtracking) is a general algorithm for finding all (or some) solutions to some computational problems. The idea is that it **incrementally** builds candidates to the solutions, and abandons a candidate ("backtrack") as soon as it determines that this candidate cannot lead to a final solution.
* like **DFS**
* Using **recursion**

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