#### Kadane's Algorithm

* Kadane's Algorithm is an algorithm that can find the maximum sum subarray given an array of numbers in O(n) time and O(1) space.
* Simple but useful algorithm of dynamic programming
  * Kadane's Algorithm utilizes optimal sub-structures - **it keeps the maximum subarray ending at the previous position in current**

> Kadane's Algorithm:
>
> Iterating through the array using an integer variable **current**, and at each index i, determines if elements before index i are "**worth**" keeping or if they should be "discard".
>
> The algorithm is only useful when the array can contain negative number.
>
> If current becomes negative, it is reset, and we start considering a new subarray starting at the current index.

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        // Initialize our variables using the first element.
        int currentSubarray = nums[0];
        int maxSubarray = nums[0];
        
        // Start with the 2nd element since we already used the first one.
        for (int i = 1; i < nums.length; i++) {
            int num = nums[i];
            // If current_subarray is negative, throw it away. Otherwise, keep adding to it.
            currentSubarray = Math.max(num, currentSubarray + num);
            maxSubarray = Math.max(maxSubarray, currentSubarray);
        }
        
        return maxSubarray;
    }
}
```

