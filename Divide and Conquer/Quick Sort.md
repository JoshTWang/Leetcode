#### Quick Sort

* Developed by Tony Hoare in 1959
* Faster than other sorting
* Acturally construct a balanced **binary search tree**

#### Steps

* Select a **pivot** and then **Partitioning**
* Quicksort the left and right sublist recursively

![img](https://assets.leetcode.com/uploads/2019/03/24/quicksort.png)

#### Complexity

* Time : O(*N* log *N*) on average, O(N ^ 2) on worst case



```java
class Solution {
    // Bottom up merge sort
    public int[] sortArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        
        quickSort(nums, 0, nums.length - 1);
        return nums;
    }
    
    private void quickSort(int[] nums, int left, int right) {
        if (left >= right) {
            return;
        }
        int pivot = partition(nums, left, right);
        quickSort(nums, left, pivot - 1);
        quickSort(nums, pivot + 1, right);
    }
    
    private int partition(int[] nums, int left, int right) {
        int pivot = nums[left];
        while (left < right) {
            while (left < right && nums[right] >= pivot) right -= 1;
          	// right find a smaller
            nums[left] = nums[right];
            while (left < right && nums[left] <= pivot) left += 1;
          	// left find a larger
            nums[right] = nums[left];
        }
        nums[left] = pivot;
        return left;
    }
}
```



#### Several Partitioning

* Basic

```java
		private int partition(int[] nums, int left, int right) {
        int pivot = nums[right];
      	int originalRight = right;
        while (left < right) {
        	  while (left < right && nums[left] <= pivot) {
        				left += 1;
            }
            while (left < right && nums[right] >= pivot) {
              	right -= 1;
            }
            swap(nums, left, right);
        }
      	// when left = right we come out of the array, at that time nums[left] will always larger than pivot. 
      	// In one case, the first inner loop breaks, at that time the right is pointing to a larger num and left meet right at that time.
      	// In another case, the second inner loop breaks, at that time the left is pointing to a larger num and wait until right find a smaller num. The right keeps moving until it meet this left pointer.
      	// If all the elements are smaller than pivot than the swap just swap itself
        swap(nums, left, originalRight);
        return left;
    }
		
		private void swap(int[] nums, int left, int right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
```

* Another basic

```java
    private int partition(int[] nums, int left, int right) {
        int pivot = nums[right];
        int i = left;

        for(int j = left; j <= right - 1; j += 1) {
            // make sure all the nums before i are smaller than pivot
            if (nums[j] < pivot) {
                swap(nums, i, j);
              	i += 1;
            }
        }
        swap(nums, i, right);
        return i;
    }
		private void swap(int[] nums, int left, int right) {
        int temp = nums[left];
        nums[left] = nums[right];
        nums[right] = temp;
    }
```



* Concise but not understanding yet

```java
		private int partition(int[] nums, int left, int right) {
        int pivot = nums[left];
        while (left < right) {
            while (left < right && nums[right] >= pivot) right -= 1;
            nums[left] = nums[right];
            while (left < right && nums[left] <= pivot) left += 1;
            nums[right] = nums[left];
        }
        nums[left] = pivot;
        return left;
    }
```



