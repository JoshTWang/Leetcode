#### Arrays.sort()

* `Arrays.sort(2Darray, (a, b) -> a[0] - b[0]);`
* `Arrays.sort(array, (a, b) -> a - b)`

```java
Arrays.sort(intervals, (a, b) -> a[0] - b[0]); // lambda


// or


class myComparator implements Comparator<int[]> {
    public int compare(int[] a, int[] b) {
      	return a[1] - b[1];
    }
}

public int compareSomething() {
  	Arrays.sort(nums, new myComparator);
}
```

