### Binary Search Tree

#### Properties

* Binary Search Tree is a binary tree where the key in each node
  * is greater than any key stored in the left sub-tree
  * and less than any key stored in the right sub-tree
* **Inorder traversal** in BST will is the most frequent used traversal method of a BST.

#### Basic Operations

##### Search

###### 700 - Search in a Binary Search Tree

##### Insert

* Always insert as a node

##### Delete

* No child -- just delete
* One child -- the child will replace the deleted node
* Two child -- replace the deleted node with minimum value node from the right subtree, or maximum value node from the left subtree.

#### TreeSet / TreeMap

```java
TreeSet<Integer> set = new TreeSet<>();
// Returns the least element in this set greater than or equal to the given element, or null if there is no such element.
Integer s = set.ceiling(n);
// Returns the greatest element in this set less than or equal to the given element, or null if there is no such element.
Integer g = set.floor(n);
```

#### Height-Balanced BST

* A `height-balanced` (or `self-balancing`) binary search tree is a binary search tree that automatically keeps its height small in the face of arbitrary item insertions and deletions.

* That is, the height of a balanced BST with `N` nodes is always `logN`. 
* Also, the height of the two subtrees of every node never differs by more than 1.
