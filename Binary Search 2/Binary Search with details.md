#### Basic Binary Search -- Search a number in a sorted array

```java
class binarySearch{
		int binarySearch(int[] nums, int target){
        if(nums == null || nums.length == 0)
            return -1;

        int left = 0, right = nums.length - 1;  // notice
        while(left <= right){  //notice
            int mid = left + (right - left) / 2;
            if(nums[mid] == target){
                return mid; 
            }
            else if(nums[mid] < target) { 
                left = mid + 1; // notice
            }
            else { 
              right = mid - 1; // notice
            }
        }
        return -1;
    }
}
```

* `while left <= right` && `right == nums.length - 1`

  * Each time the **Search Space [left, right]**

  * We search every element in the array

  * We terminate when left > right (left cross right) -- e.g. search space is [3, 2]

  * We can do a little change here

    * ```java
      while(left < right) {
      	// ...
      }
      return nums[left] == target ? left: -1;
      ```

* `left = mid + 1` && `right = mid - 1`
  * The goal is to search the element we want. Each time we find `nums[mid] != target`, we should exclude mid from our **search space**

#### Binary Search -- find the left bound

```java
class binarySearch{		
		int leftBound(int[] nums, int target){
        if(nums == null || nums.length == 0)
            return -1;

        int left = 0, right = nums.length; // notice
        
      	while(left < right){ // notice
            int mid = left + (right - left) / 2;
            if(nums[mid] < target) { 
                left = mid + 1; // notice
            }
            else { 
              right = mid; // notice
            }
        }

        return left;
    }
}
```

* `while left <= right` && `right == nums.length - 1`

  * Each time the **Search Space [left, right)**, so the nums[nums.length] will never be considered

  * We terminate when `left == right` -- only one element is left in the array in this time, the only element in the array must be better than anyone else in the array
    * [153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array) -- the most qualified element will remain in the array
    * [278. First Bad Version](https://leetcode.com/problems/first-bad-version) -- left boundary

* `left = mid + 1` && `right = mid`

  * Each time we divide the space into [left, mid) and [mid + 1, right)
  * In other words, when we find `nums[mid] == target` we narrow the search space but we don't want mid to be exclude
  * We return left because all the other elements are exclusive.

#### Binary Search -- find the righ bound

```java
class binarySearch{		
		int leftBound(int[] nums, int target){
        if(nums == null || nums.length == 0)
            return -1;

        int left = 0, right = nums.length; 
        
      	while(left < right){ 
            int mid = left + (right - left) / 2;
            if(nums[mid] <= target) { // notice
                left = mid + 1; 
            }
            else { 
              right = mid; // notice
            }
        }

        return left - 1;
    }
}
```

