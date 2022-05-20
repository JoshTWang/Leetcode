![img](https://leetcode.com/explore/learn/card/binary-search/136/template-analysis/Figures/binary_search/Template_Diagram.png)

### Binary Search

* Binary Search is an algorithm that **divides the search space** in 2 after every comparison.
* Binary Search should be considered every time you need to **search for an index or element** in a collection. 
* If the collection is unordered, we can always **sort** it first before applying Binary Search.

#### Three sections

1. ***Pre-processing*** - Sort if collection is unsorted.
2. ***Binary Search*** - Using a loop or recursion to divide search space in half after each comparison.
3. ***Post-processing*** - Determine viable candidates in the remaining space.



#### Template I

```java
class binarySearch{
		int binarySearch(int[] nums, int target){
        if(nums == null || nums.length == 0)
            return -1;

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

**Key Attributes:**

------

- Most basic and elementary form of Binary Search
- Search Condition can be determined without comparing to the element's neighbors (or use specific elements around it)
- No post-processing required because at each step, you are checking to see if the element has been found. If you reach the end, then you know the element is not found

**Distinguishing Syntax:**

------

- Initial Condition:` left = 0, right = length-1`
- Termination: `left > right`
- Searching Left: `right = mid-1`
- Searching Right: `left = mid+1`



#### Template II -- accessing curr and right

```java
int binarySearch(int[] nums, int target){
  if(nums == null || nums.length == 0)
    return -1;

  int left = 0, right = nums.length;
  while(left < right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid; }
  }

  // Post-processing:
  // End Condition: left == right
  if(left != nums.length && nums[left] == target) return left;
  return -1;
}
```

**Key Attributes:**

------

- An advanced way to implement Binary Search.
- Search Condition needs to **access the element's immediate right neighbor**
- Use the element's right neighbor to determine if the condition is met and decide whether to go left or right
- Guarantees Search Space is at least 2 in size at each step
- **Post-processing** required. Loop/Recursion ends when you have 1 element left. Need to assess if the remaining element meets the condition.

 

**Distinguishing Syntax:**

------

- Initial Condition: `left = 0, right = length`
- Termination: `left == right`
- Searching Left: `right = mid`
- Searching Right: `left = mid+1`

##### Explanation

---

* the loop end when left == right --- one element in the array that we do not work on
* one of the left and right should be mid + 1/ mid - 1 to avoid infinite loop

* `.....0, 0, 0, 0, 1, 1, 1, 1, ....`

  * if we want to find the first 1 -- left = mid + 1, right = mid

  * if we want to find the last 0 -- left = mid, right = mid - 1

---

###### 162 - Find Peak Element

###### 278 - First Bad Version



#### Templete III -- accessing curr and left and right

```java
int binarySearch(int[] nums, int target) {
    if (nums == null || nums.length == 0)
        return -1;

    int left = 0, right = nums.length - 1;
    while (left + 1 < right){
        // Prevent (left + right) overflow
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }

    // Post-processing:
    // End Condition: left + 1 == right
    if(nums[left] == target) return left;
    if(nums[right] == target) return right;
    return -1;
}
```

**Key Attributes:**

------

- An alternative way to implement Binary Search
- Search Condition needs to access element's immediate left and right neighbors
- Use element's neighbors to determine if condition is met and decide whether to go left or right
- Gurantees Search Space is at least 3 in size at each step
- Post-processing required. Loop/Recursion ends when you have 2 elements left. Need to assess if the remaining elements meet the condition.

 

**Distinguishing Syntax:**

------

- Initial Condition:` left = 0, right = length-1`
- Termination: `left + 1 == right`
- Searching Left: `right = mid`
- Searching Right: `left = mid`