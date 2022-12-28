#### Common patterns 1: Iteration in the recurence relation

 [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

* `dp(i)=min(dp(i - 1) + cost[i - 1], dp(i - 2) + cost[i - 2])`

* if the question was rephrased so that we could take up to k steps at a time
* `dp(i)=min(dp(j) + cost[j])` (i - k)≤j<i

Instead of choosing from a static number of options, we usually add a **for-loop to iterate through a dynamic number of options and choose the best one.**



* In each state, we need to iterate (**for loop**) all the possible options

[322. Coin Change](https://leetcode.com/problems/coin-change)

* In each state(remaining money), we should **iterate** through all the denominations in coins

[1335. Minimum Difficulty of a Job Schedule](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule)

* In each state(work index, day index), we should **iterate** all the possible ending work index
  * We need to remain enough work before and after `dth` day, because at least one work per day

[139. Word Break](https://leetcode.com/problems/word-break)

* 2 * 2 * 2 * 2 approaches
  * Dp / Bfs (Brute force)
  * Top down / bottom up
  * Left / right
  * Iterate s.substring or workDict

[300. Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence)

* in each state dp(i) we iterate dp(j) which j < i
* It has a better idea: intelligence + Binary Search