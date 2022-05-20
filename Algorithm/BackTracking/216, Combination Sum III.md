#### Copy the answer

| Recursion | Combination      |
| --------- | ---------------- |
| 1         | 1                |
| 2         | 1 2              |
| 3         | 1 2 3            |
| 4         | 1 2 4            |
| 5         | **1 2 5**        |
| 6         | 1 2 6            |
| 7         | 1 2 7            |
| 8         | 1 2 8            |
|           | 1 2 9            |
|           | **1 3 5**        |
|           | 1 3 6            |
|           | 1 8 9            |
|           | 1 9 out of scope |
|           | 2 3 4            |
|           | 2 3 5            |
|           |                  |
|           |                  |



```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        LinkedList<Integer> comb = new LinkedList<Integer>();
        
        this.backtrack(n, k, comb, 0, results);
        return results;       
    }
    
    // remain -- remain sum
    // k -- how many numbers to add to sum
    // com -- current combination
    // next start -- from 0 to 9
    // results -- to return
    protected void backtrack(int remain, int k, LinkedList<Integer> comb, int next_start, List<List<Integer>> results) {
        
        // we need to make a deep copy
        // otherwise the comb would be reverted in orther branch of backtracking
        if (remain == 0 && comb.size() == k) {
            // find a qualified combination
            results.add(new ArrayList<Integer>(comb));
            return;
        } else if (remain < 0 || comb.size() == k) {
            // Exceed the scope
            // 1. the number is larger than 9 -- 5, 7, _
            // 2. we have already got 3 numbers -- 1, 2, 3
            return;
        }
        
        for (int i = next_start; i < 9; i += 1) {
            // we use i + 1 to avoid the dupilcate
            comb.add(i + 1);
            this.backtrack(remain - i - 1, k, comb, i + 1, results);
            // remove the digit we just tried out
            comb.removeLast();
        }
    }
}
```

