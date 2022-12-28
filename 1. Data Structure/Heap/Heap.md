#### Details

###### MinHeap

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

##### Heap compare the value of HashMap

```java
			// init minheap the less frequent element first
        Queue<Integer> heap = new PriorityQueue<Integer>(
            (n1, n2) -> count.get(n1) - count.get(n2));
```

###### MaxHeamp

* `Collectinos.reverseOrder()`

```java
PriorityQueue<Integer> maxPQ = new PriorityQueue<>(Collections.reverseOrder());

Queue<Integer> heap = new PriorityQueue<Integer>((n1, n2) -> n2 - n1);
```

##### Collections.reverseOrder()

* returns a **comparator** that imposes the reverse of the natural ordering on the objects.

* Sorted array in reverse order

```java
Arrays.sort(arr, Collections.reverseOrder());
```



##### add() vs. offer()

- **offer** method - tries to add an element to a queue, and returns **false** if the element can't be added (like in case when a queue is full), or **true** if the element was added, and doesn't throw any specific exception.
- **add** method - tries to add an element to a queue, returns ***true\*** if the element was added, or throws an IllegalStateException if no space is currently available.

##### poll() vs. remove()

* **Poll()** - It will give the head element of the queue and will remove the head element from queue. If queue is empty then it will return null.

* **Remove()** - It will give the head element of the queue and will remove the head element from queue. If queue is empty then it will throw an Exception.

#### Heap

* Priority Queue
  * A priority queue is an [abstract data type](https://en.wikipedia.org/wiki/Abstract_data_type) similar to a regular [queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)) or [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) data structure in which each element additionally has a "**priority**" associated with it. In a priority queue, an element with high priority is served before an element with low priority.

* Priority Queue is an **abstract data type** while a heap is a **data structure**.
* A heap is a binary tree that meets the following criteria:
  - Is a **complete binary tree**;
  - The value of each node must be **no greater than (or no less than)** the value of its child nodes.

##### properties

- Insertion of an element into the Heap has a time complexity of O(logN);
- Deletion of an element from the Heap has a time complexity of O(logN);
- The maximum/minimum value in the Heap can be obtained with O(1) time complexity.

##### Two heaps

There are two kinds of heaps: **Max Heap** and **Min Heap**.

- Max Heap: Each node in the Heap has a value **no less than** its child nodes. Therefore, the top element (root node) has the **largest** value in the Heap.
- Min Heap: Each node in the Heap has a value **no larger than** its child nodes. Therefore, the top element (root node) has the **smallest** value in the Heap.

#### Implement

* Elements in the Heap can be stored in the **array** in the form of a **binary tree**.

```java
// Implementing "Min Heap"
public class MinHeap {
    // Create a complete binary tree using an array
    // Then use the binary tree to construct a Heap
    int[] minHeap;
    // the number of elements is needed when instantiating an array
    // heapSize records the size of the array
    int heapSize;
    // realSize records the number of elements in the Heap
    int realSize = 0;

    public MinHeap(int heapSize) {
        this.heapSize = heapSize;
        minHeap = new int[heapSize + 1];
        // To better track the indices of the binary tree, 
        // we will not use the 0-th element in the array
        // You can fill it with any value
        minHeap[0] = 0;
    }

    // Function to add an element
    public void add(int element) {
        realSize++;
        // If the number of elements in the Heap exceeds the preset heapSize
        // print "Added too many elements" and return
        if (realSize > heapSize) {
            System.out.println("Added too many elements!");
            realSize--;
            return;
        }
        // Add the element into the array
        minHeap[realSize] = element;
        // Index of the newly added element
        int index = realSize;
        // Parent node of the newly added element
        // Note if we use an array to represent the complete binary tree
        // and store the root node at index 1
        // index of the parent node of any node is [index of the node / 2]
        // index of the left child node is [index of the node * 2]
        // index of the right child node is [index of the node * 2 + 1]
        int parent = index / 2;
        // If the newly added element is smaller than its parent node,
        // its value will be exchanged with that of the parent node 
        while ( minHeap[index] < minHeap[parent] && index > 1 ) {
            int temp = minHeap[index];
            minHeap[index] = minHeap[parent];
            minHeap[parent] = temp;
            index = parent;
            parent = index / 2;
        }
    }

    // Get the top element of the Heap
    public int peek() {
        return minHeap[1];
    }

    // Delete the top element of the Heap
    public int pop() {
        // If the number of elements in the current Heap is 0,
        // print "Don't have any elements" and return a default value
        if (realSize < 1) {
            System.out.println("Don't have any element!");
            return Integer.MAX_VALUE;
        } else {
            // When there are still elements in the Heap
            // realSize >= 1
            int removeElement = minHeap[1];
            // Put the last element in the Heap to the top of Heap
            minHeap[1] = minHeap[realSize];
            realSize--;
            int index = 1;
            // When the deleted element is not a leaf node
            while (index <= realSize / 2) {
                // the left child of the deleted element
                int left = index * 2;
                // the right child of the deleted element
                int right = (index * 2) + 1;
                // If the deleted element is larger than the left or right child
                // its value needs to be exchanged with the smaller value
                // of the left and right child
                if (minHeap[index] > minHeap[left] || minHeap[index] > minHeap[right]) {
                    if (minHeap[left] < minHeap[right]) {
                        int temp = minHeap[left];
                        minHeap[left] = minHeap[index];
                        minHeap[index] = temp;
                        index = left;
                    } else {
                        // maxHeap[left] >= maxHeap[right]
                        int temp = minHeap[right];
                        minHeap[right] = minHeap[index];
                        minHeap[index] = temp;
                        index = right;
                    }
                } else {
                    break;
                }
            }
            return removeElement;
        } 
    }

    // return the number of elements in the Heap
    public int size() {
        return realSize;
    }

    public String toString() {
        if (realSize == 0) {
            return "No element!";
        } else {
            StringBuilder sb = new StringBuilder();
            sb.append('[');
            for (int i = 1; i <= realSize; i++) {
                sb.append(minHeap[i]);
                sb.append(',');
            }
            sb.deleteCharAt(sb.length() - 1);
            sb.append(']');
            return sb.toString();
        }
    }

    public static void main(String[] args) {
        // Test case
        MinHeap minHeap = new MinHeap(3);
        minHeap.add(3);
        minHeap.add(1);
        minHeap.add(2);
        // [1,3,2]
        System.out.println(minHeap.toString());
        // 1
        System.out.println(minHeap.peek());
        // 1
        System.out.println(minHeap.pop());
        // [2, 3]
        System.out.println(minHeap.toString());
        minHeap.add(4);
        // Add too many elements
        minHeap.add(5);
        // [2,3,4]
        System.out.println(minHeap.toString());
    }
}

```

#### Application

##### HeapSort

* Using maxheap -- inplace

1. Heapify all elements into a Max Heap.
2. Record and delete the **top** element.
3. Put the top element into an array T that stores all sorted elements. Now, the Heap will remain a Max Heap.
4. Repeat steps 2 and 3 until the Heap is empty. The array T will contain all elements sorted in descending order.

##### The Top k problem

###### Approach 1

Solution of the Top K **largest** elements:

1. Construct a **Max** Heap.
2. Add all elements into the Max Heap.
3. Traversing and deleting the top element (using pop() or poll() for instance), and store the value into the result array T.
4. Repeat step 3 until we have removed the K largest elements.

Solution of the Top K **smallest** elements:

1. Construct a **Min** Heap.
2. Add all elements into the Min Heap.
3. Traversing and deleting the top element (using pop() or poll() for instance), and store the value into the result array T.
4. Repeat step 3 until we have removed the K smallest elements.

###### Approach 2

Solution of the Top K **largest** elements:

1. Construct a **Min** Heap with size K.
2. Add elements to the Min Heap one by one.
3. When there are K elements in the “Min Heap”, compare the current element with the top element of the Heap:
4. If the current element is no larger than the top element of the Heap, drop it and - proceed to the next element.
5. If the current element is larger than the Heap’s top element, delete the Heap’s top element, and add the current element to the Min Heap.
6. Repeat Steps 2 and 3 until all elements have been iterated.

Now the K elements in the Min Heap are the K largest elements.

Solution of the Top K **smallest** elements:

1. Construct a **Max** Heap with size K.
2. Add elements to the Max Heap one by one.
3. When there are K elements in the “Max Heap”, compare the current element with the top element of the Heap:
4. If the current element is no smaller than the top element of the Heap, drop it and proceed to the next element.
5. If the current element is smaller than the top element of the Heap, delete the top element of the Heap, and add the current element to the Max Heap.
6. Repeat Steps 2 and 3 until all elements have been iterated.

Now the K elements in the Max Heap are the K smallest elements.