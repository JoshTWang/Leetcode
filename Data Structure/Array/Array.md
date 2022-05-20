> Using long
>
> `System.arraycopy()`
>
> `.clone`



#### Array

* An array is a basic data structure to store a collection of elements **sequentially**.
* Elements can be **accessed randomly** since each element in the array can be identified by and array **index**.
* Array has a **fixed capacity**. We need to specify the **size** of the array when we initialize it,

##### Operation

###### Initialize

```java
int[] a = new int[3];
int[] a = {1, 2, 3};
```

###### Iterate

```java
for (int i = 0; i < array.length; i += 1)
for (int i: array)
```

###### Sort

```java
Arrays.sort(array);
```

###### Search

* Linear Search
* **Binary Search**
  * sorted data



##### In-Place

* No need extra space
* modify the input array

---

#### Dynamic array

* **ArrayList -- Java**
* Vector -- C++

##### Operation

###### Initialize

```java
List<Integer> v = new ArrayList<>();
```

###### Cast an Array to ArrayList

```java
Integer[] a = {0, 1, 2, 3, 4};
v0 = new ArrayList<>(Arrays.asList(a));
```

###### Make a copy

* **reference copy**
* **deep copy**

```java
List<Integer> v2 = v1;                      // another reference to v1
List<Integer> v3 = new ArrayList<>(v1);     // make an actual copy of v1
```

###### Build in functions

```java
v1.set(index, value);
v1.get(index);
v1.size();
v1.add();
v1.remove(index);
```

> **add(E e)**
>
> Appends the specified element to the end of this list (optional operation).

------

> **add(int index, E element)**
>
> Inserts the specified element at the specified position in this list (optional operation).

------

> **set(int index, E element)** 
>
> Replaces the element at the specified position in this list with the specified element (optional operation).

###### sort

```java
Collections.sort(v1);
```

**Codes**

```java
// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        // 1. initialize
        List<Integer> v0 = new ArrayList<>();
        List<Integer> v1;                           // v1 == null
        // 2. cast an array to a vector
        Integer[] a = {0, 1, 2, 3, 4};
        v1 = new ArrayList<>(Arrays.asList(a));
        // 3. make a copy
        List<Integer> v2 = v1;                      // another reference to v1
        List<Integer> v3 = new ArrayList<>(v1);     // make an actual copy of v1
        // 3. get length
        System.out.println("The size of v1 is: " + v1.size());
        // 4. access element
        System.out.println("The first element in v1 is: " + v1.get(0));
        // 5. iterate the vector
        System.out.print("[Version 1] The contents of v1 are:");
        for (int i = 0; i < v1.size(); ++i) {
            System.out.print(" " + v1.get(i));
        }
        System.out.println();
        System.out.print("[Version 2] The contents of v1 are:");
        for (int item : v1) {
            System.out.print(" " + item);
        }
        System.out.println();
        // 6. modify element
        v2.set(0, 5);       // modify v2 will actually modify v1
        System.out.println("The first element in v1 is: " + v1.get(0));
        v3.set(0, -1);
        System.out.println("The first element in v1 is: " + v1.get(0));
        // 7. sort
        Collections.sort(v1);
        // 8. add new element at the end of the vector
        v1.add(-1);
        v1.add(1, 6);
        // 9. delete the last element
        v1.remove(v1.size() - 1);
    }
}
```



#### Category

###### Basic Array

###### Two Pointer

###### Matrix



#### Max && Cur

###### 53 - Maximum Subarray

* maxSubarray
* curSubarray

###### 485 - Max Consecutive-Ones

* Maxcount
* Curcount

###### 487 - Max Consecutive-Ones II

* First second
* Maxcount





### Array-related data structures

* String
* Hash table
* Linked List
* Queue
* Stack

###### Sorting

* Binary Search

###### Two Pointer -- Greedy Algorithm

###### Sliding Window