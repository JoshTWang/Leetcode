##### Integer vs Int in list

* In List<Integer>
  * `remove(5) will remove the index of 5`
  * `remove((Integer) 5) will remove the val of 5 in the list`

#### Initialize a list with value

Immutable

* ```java
  List<String> places = Arrays.asList("Buenos Aires", "Córdoba", "La Plata");
  ```

mutable

```java
ArrayList<String> places = new ArrayList<>(Arrays.asList("Buenos Aires", "Córdoba", "La Plata"));
```



### Linked List

* Linked list is a **linear** data structure which **link all the separated elements together** by the **reference field**

![image-20220210160042232](/Users/morningstar/Library/Application Support/typora-user-images/image-20220210160042232.png)

* Two type
  * Singly linked list
  * Doubly linked list
* Technique
  * Two pointer
    * fast
    * Slow




### Singly linked list

```java
// Definition for singly-linked list.
public class SinglyListNode {
    int val;
    SinglyListNode next;
    SinglyListNode(int x) { val = x; }
}
```

#### Operation

##### Bad performance

* `get`
  * It takes `O(N)` time on average to `visit an element by index`

##### Good performance

* `add` operation
  * Appends the specified element to the **end** of this list (optional operation).

* `delete` operation

#### Some interesting topic

* Two pointer technique
* reverse linked list

#### Takeaways

* Going through some test cases
* Feel free to use **several pointers**
* You may need to track the **previous** node of the current node

### Doubly Linked List

```java
// Definition for doubly-linked list.
class DoublyListNode {
    int val;
    DoublyListNode next, prev;
    DoublyListNode(int x) {val = x;}
}
```

* Add operation
  * Linked curr with prev and next
  * relink the prev and next with cur
* Delete operatino
  * Linked the prev and next

#### Summary

![img](https://assets.leetcode.com/uploads/2020/10/02/comparison_of_time_complexity.png)

* If you need to add or delete a node frequently, a **linked list** could be a good choice.

* If you need to access an element by index often, **an array** might be a better choice than a linked list.



### Techniques

#### Basic

###### 707 - Design Linked List -- CS61B

#### Iteration

###### 2 - Add Two Numbers

* Carry

###### 61 - Rotate List

###### 83 - Remove Duplicates

###### 138 - Copy List with Random Pointer

###### 203 - Remove Linked List Elements

###### 328 - Odd Even Linked List

###### 708 - Insert into a Sorted Circular



#### Two Pointer -- fast & slow

###### 19 - Remove Nth Node From End of List

###### 24 - Swap nodes in pairs

###### 141 - Linked List Cycle

###### 142 - Linked List Cycle II

* Floyd's Tortoise and Hare

###### 160 - Intersection of two Linked Lists

* how to make the two pointer in the same pattern



#### Recursion

###### 21 - Merge Two Sorted Lists



#### Reverse

###### 206 - Reverse Linked List

###### 234 - Palindrome Linked List



#### DFS

###### 430 - Flatten a Multilevel Doubly Linked List
