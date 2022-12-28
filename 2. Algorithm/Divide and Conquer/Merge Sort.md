#### Top down merge sort

![img](https://assets.leetcode.com/uploads/2019/04/15/topdown_mergesort.png)

1. In the first step, we divide the list into two sublists. (**Divide**)
2. Then in the next step, we ***recursively*** sort the sublists in the previous step. (**Conquer**)
   * Reach the base case where the input list is either empty or contains a single element
3. Finally we merge the sorted sublists in the above step repeatedly to obtain the final list of sorted elements. (**Combine**)

```java
class Solution {
    // Top down merge sort
    public int[] sortArray(int[] nums) {
        mergeSort(nums, 0, nums.length - 1);
        return nums;
    }
    
    private void mergeSort(int[] nums, int left, int right) {
        if (left >= right) {
            // not right - left <= 1 because right - left = 1 has two numbers
            return;
        }
        int mid = left + (right - left) / 2;
        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);
        merge(nums, left, right);
    }
    
    private void merge(int[] nums, int left, int right) {
        int mid = left + (right - left) / 2;
        int[] res = new int[right - left + 1];
        int lpointer = left;
        int rpointer = mid + 1;
        int pointer = 0;
        while (lpointer <= mid || rpointer <= right) {
            if (lpointer > mid || rpointer <= right && nums[lpointer] > nums[rpointer]) {
              	// The && operator has higher precedence than the ||
                res[pointer] = nums[rpointer];
                rpointer += 1;
            } else {
                res[pointer] = nums[lpointer];
                lpointer += 1; 
            }
            pointer += 1;
        }
        System.arraycopy(res, 0, nums, left, right - left + 1);
    }
}
```



#### Bottom up merge sort

![img](https://assets.leetcode.com/uploads/2019/04/06/mergesort.png)

1. We divide the list into sublists of a single element at the beginning. Each of the sublists is then sorted already. 
2. Then from this point on, we merge the sublists two at a time until a single list remains.

#### Complexity

* The overall **time complexity** of the merge sort is O(*N* log *N*)
  * (log *N* levels) * (N work each level)
* **Space complexity** is O(N)

```java
class Solution {
    // Bottom up merge sort
    public int[] sortArray(int[] nums) {
        mergeSort(nums);
        return nums;
    }
    
    private void mergeSort(int[] nums) {
        // merge directly
        for (int size = 1; size < nums.length; size *= 2) {
            for (int left = 0; left < nums.length - size; left += 2 * size) {
                int mid = left + size - 1;
                // Can not use: int mid = left + (right - left) / 2;
                // (xx xx  xx xx)  (xx xx x)
                // xxxx xxxx (xxxx x) the mid is not the mid of left and right
                int right = Math.min(left + 2 * size - 1, nums.length - 1);
                merge(nums, left, mid, right);
            }
        }
    }
    private void merge(int[] nums, int left, int mid, int right) {
        int[] res = new int[right - left + 1];
        int lpointer = left;
        int rpointer = mid + 1;
        int pointer = 0;
        while (lpointer <= mid || rpointer <= right) {
            if (lpointer > mid || rpointer <= right && nums[lpointer] > nums[rpointer]) {
              	// The && operator has higher precedence than the ||
                res[pointer] = nums[rpointer];
                rpointer += 1;
            } else {
                res[pointer] = nums[lpointer];
                lpointer += 1; 
            }
            pointer += 1;
        }
        System.arraycopy(res, 0, nums, left, right - left + 1);
    }
}
```

* Why we need to add variable `mid`?
* If we have 6 elements
  * In top down recursion, before last merging it should be (1 4 7) (2 5 8)
  * In bottom up recursion, before last merging it could be (1 2 4 7) (5, 8) --> if we use mid = (right + left / 2) it would be merging (1 2 4) (7 5 8) so we need to add` mid` to record the end of left subarray