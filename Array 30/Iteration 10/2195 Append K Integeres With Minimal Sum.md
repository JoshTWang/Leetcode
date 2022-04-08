#### My Time Limit Exceeded Solution

```java
class Solution {
    public long minimalKSum(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        long sum = 0;
        for (int i: nums) {
            set.add(i);
        }
        int num = 1; 
        while (k > 0) {
            while (set.contains(num)) {
                num += 1;
            }
            sum += num;
            k -= 1;
            num += 1;
        }
        return sum;
    }
}
```

#### Not totally understanding idea

```java
class Solution {
    public long minimalKSum(int[] nums, int k) {
        Arrays.sort(nums);        
        int prev = 0; // we use prev to check whether curr == prev
        long occupied = 0; // the sum of unique number in nums that occupied the position

        for (int num: nums) {
            // The key idea is to find how many unique number in nums is in the range of 0 - k. Each time we find one, we need to increase the k by 1
            // for example if we want to add 5 numbers in the array [3, 4, 77, 77,12123, 24441], 3 and 4 occupy the position we want to add into the array, so actually we need to add 5 + 2 number and then we minus 3 and 4 in the end.
            // if we want to add 5 numbers in the array [4, 4, 4, 77, 12123, 24441], we only need to add only 5 + 1 number and then we minus 4 in the end.(because multiple 4s only occupy one position)
            if (num != prev && num <= k) {
                k += 1;
                occupied += num;        
            }            
            prev = num;
        }
        // using n * (n + 1) / 2 to calculate the sum of k integers
        long res = (long)(1 + k) * k / 2 - occupied;
        return res;        
    }
}
```

