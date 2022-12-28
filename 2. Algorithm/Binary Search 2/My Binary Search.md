#### Template I -- Basic Binary Search

> Find the exact number

```java
class binarySearch{
		int binarySearchI(int[] nums, int target){
        int left = 0, right = nums.length - 1;
        while(left <= right){
            // Prevent (left + right) overflow
            int mid = left + (right - left) / 2;
            if(nums[mid] == target){ return mid; }
            else if(nums[mid] < target) { left = mid + 1; }
            else { right = mid - 1; }
        }

        // End Condition: left > right
        return -1;
    }
}
```

---



**The main difference between `Template II` and `Template III` is whether `nums[mid] == target` belongs to  `left` or `right`**

#### Template II

> In the last iteration`right - left == 1`:
>
> * We will search `num[left]`
> * `left` is used to avoid infinite loop

* Find the element >= target

```java
class binarySearch{
		int binarySearchII(int[] nums, int target){
        int left = 0, right = nums.length; // we will try left but never try right so right = nums.length
        while(left < right){
            int mid = left + (right - left) / 2;
            if(nums[mid] < target) { 
              	left = mid + 1; 
            }
            else { 
              	right = mid; 
            }
        }
        return mid;
    }
}
```

* Find first F:  `T T T T F F`

```java
public class Solution extends VersionControl {
  	// 1-index
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

---



#### Template III

> In the last iteration`right - left == 1`:
>
> * We will search `num[right]`
> * `right` is used to avoid infinite loop

* Find Last T:  `T T T T F F`

```java
public class Solution extends VersionControl {
  	// 1-index
    public int firstBadVersion(int n) { // T T T F
        int left = 1;
        int right = n;
        while (left < right) {
            int mid = left + (right - left + 1) / 2;
            if (isBadVersion(mid)) {
                right = mid - 1;
            } else {
                left = mid;
            }
        }
        return left;
    }
}
```

* Find the element <= target

```java
class binarySearch{
		int binarySearchIII(int[] nums, int target){
        int left = -1, right = nums.length - 1; // we will try right but never try left so left = -1
        while(left < right){
            int mid = left + (right - left + 1) / 2;
            if(nums[mid] <= target) { 
              	left = mid; 
            }
            else { 
              	right = mid - 1; 
            }
        }
        return mid;
    }
}
```

