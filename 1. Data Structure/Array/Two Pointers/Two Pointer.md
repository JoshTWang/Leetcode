#### Two Pointer

* Two pointer help us cover a **sub-array** or a mini array within the main array.
  * **Same direction**
  * **Opposite directions**
  * Fixed width



* One pointer starts from the **beginning** while the other pointer starts from the **end**.

```java
public static void reverse(int[] v, int N) {
    int i = 0;
    int j = N - 1;
    while (i < j) {
        swap(v, i, j);  // this is a self-defined function
        i++;
        j--;
    }
}
```

* One pointer is still used for the **iteration** while the second one always points at the position for next **addition**

```java
public int removeElement(int[] nums, int val) {
    int k = 0;
    for (int i = 0; i < nums.length; ++i) {
        if (nums[i] != val) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}
```



##### Left & Right

| Problem                                                      | Description                | Difficulty | Review rate |
| ------------------------------------------------------------ | -------------------------- | ---------- | ----------- |
| [11. Container With Most Water](https://leetcode.com/problems/container-with-most-water) | Proof by **contradiction** | ✦ ✦ ✦      | ★★★★★       |
|                                                              |                            |            |             |
| [905. Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity) | Similar to partition       | ✦          | ★★★         |
| [941. Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array) | Different left&right       | ✦          | ★           |
| [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array) | Math                       | ✦          | ★★★         |
|                                                              |                            |            |             |
|                                                              |                            |            |             |

##### Fast & Slow

| Problem                                                      | Description           | Difficulty | Review rate |
| ------------------------------------------------------------ | --------------------- | ---------- | ----------- |
| [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array) | Typical               | ✦ ✦        | ★★☆         |
| [27. Remove Element](https://leetcode.com/problems/remove-element) | Typical               | ✦          | ★★          |
| [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii) | $26$ Plus             | ✦ ✦ ✧      | ★★☆         |
|                                                              |                       |            |             |
| [163. Missing Ranges](https://leetcode.com/problems/missing-ranges) | Range                 | ✦✦         | ★☆          |
| [228. Summary Ranges](https://leetcode.com/problems/summary-ranges) | Range                 | ✦ ✦ ✧      | ★★☆         |
| [283. Move Zeroes](https://leetcode.com/problems/move-zeroes) | Read & write          | ✦          | ★           |
|                                                              |                       |            |             |
| [2216. Minimum Deletions to Make Array Beautiful](https://leetcode.com/problems/minimum-deletions-to-make-array-beautiful) | Similar to TwoPointer | ✦          | ★           |

★ ✦

☆ ✧