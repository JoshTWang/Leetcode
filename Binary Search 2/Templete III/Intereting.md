#### 278 First Bad

* T T T F F F -- find first F

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        // both boundary is inclusive
        int left = 1;
        int right = n;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid)) {
                // mid may be the final answer
                right = mid;
            } else {
                // mid will never be the final answer, so left = mid + 1
                left = mid + 1;
            }
        }
        return left;
    }
}
```



#### Key part

```java
T T T T T T T T T T F F F F F F F

Leetcode 278
// find first False
while(left < right) {
	int mid = left + (right - left) / 2;
	if (false) {
    // we want to find the first F so when we meet F we want to find the leftmost F so we move right pointer. Because we don't know whether this F is the lestmost so we treat this mid be inclusive 
		right = mid;
	} else {
    // when come to True it is absolutely exclusive
		left = mid + 1;
	}
}




// Leetcode 2226
// find last True
while(left < right) {
	int mid = left + (right - left + 1) / 2;
  // when left and right are next to each other(on the last search), we check the right to avoid infinite loop
  
	if (false) {
    // we want to find the last T, so if we find false, we move right pointer to check left and this mid is exlusive
		right = mid - 1;
	} else {
    // we find T but we do not know whether it is the rightmost T so we try to move the left pointer
		left = mid;
	}
}


// First: left < right is more general than left <= right

// Second: we need to decide whether left = mid + 1 && right = mid
//														  or   left = mid && right = mid - 1

// Third: Based on second choice we choose the mid considering the infinite loop issues


// why not 
  if (piles < k) {
    // 5 children 4 piles
    right = mid - 1;
  } else if (piles > k){
    // 5 children 6 piles
    left = mid + 1;
  } else {
    // 5 children 5 piles
    left = mid;
  }
// Even though we got 6 piles but we can not make sure that if we add left we still have enouth piles for 5 children. It means that in some situation, we must divided to 6 piles for 5 children because the possible solution is not continuous
```



#### 2226 Last Good

```java
class Solution {
    // this question is to find the last element valid 
    // T T T F F, we would find the last T
    
    // mid = (left + right) / 2      to find first element valid
    // mid = (left + right + 1) / 2  to find last element valid
    public int maximumCandies(int[] candies, long k) {
        int max = 0;
        long sum = 0;
        for (int c : candies) {
            if (c > max) {
                max = c;
            }
            sum += c;
        }
        if (sum < k) {
            return 0;
        } else if (sum == k) {
            return 1;
        }
        // binary search
        int left = 1;
        int right = max;
        while (left < right) {
            int mid = left + (right - left + 1) / 2; // find the t t t t f f -- last t
            long piles = 0;
            for (int c: candies) {
                piles += c / mid;
            }
            if (piles < k) {
                // 5 children 4 piles
                right = mid - 1;
            } else {
                // piles >= k --- we have 5 children but we got 5 or 6 piles
                left = mid;
            }
        }
        return left;
    }
}
```

