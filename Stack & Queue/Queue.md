

#### Introduction

* We may access a random element by index in **Array**
* What if we want to **restrict the processing order**

* two DS
  * Queue: **FIFO**
  * Stack: LIFO

#### Abstract

* `Queue<Integer> q = new LinkedList();`
* `queue.offer()` or `queue.add()`
* `queue.poll` or `queue.remove()`
* `queue.peek()`
* `queue.size()`



#### Queue

* Insert -- enqueue -- added at the end of the queue
* Delete -- dequeue -- remove the first element

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/05/03/screen-shot-2018-05-03-at-151021.png)

##### Reinvent the wheel -- Array

```java
// "static void main" must be defined in a public class.

class MyQueue {
    // store elements
    private List<Integer> data;         
    // a pointer to indicate the start position
    private int p_start;            
    public MyQueue() {
        data = new ArrayList<Integer>();
        p_start = 0;
    }
    /** Insert an element into the queue. Return true if the operation is successful. */
    public boolean enQueue(int x) {
        data.add(x);
        return true;
    };    
    /** Delete an element from the queue. Return true if the operation is successful. */
    public boolean deQueue() {
        if (isEmpty() == true) {
            return false;
        }
        p_start++;
        return true;
    }
    /** Get the front item from the queue. */
    public int Front() {
        return data.get(p_start);
    }
    /** Checks whether the queue is empty or not. */
    public boolean isEmpty() {
        return p_start >= data.size();
    }     
};

public class Main {
    public static void main(String[] args) {
        MyQueue q = new MyQueue();
        q.enQueue(5);
        q.enQueue(3);
        if (q.isEmpty() == false) {
            System.out.println(q.Front());
        }
        q.deQueue();
        if (q.isEmpty() == false) {
            System.out.println(q.Front());
        }
        q.deQueue();
        if (q.isEmpty() == false) {
            System.out.println(q.Front());
        }
    }
}
```

##### Reinvent the wheel -- List

```java
class MyCircularQueue {    
    Node sentinel;
    Node last;
    int size;
    int capacity;
    
    private class Node{
        int value;
        Node next;
        
        public Node(int value) {
            this.value = value;
            this.next = null;
        }
        public Node(int value, Node next) {
            this.value = value;
            this.next = next;
        }
    }
    
    public MyCircularQueue(int k) {
        capacity = k;
        sentinel = new Node(61);
        size = 0;
        last = sentinel;
    }
    
    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }
        last.next = new Node(value);
        last = last.next;
        size += 1;
        return true;
    }
    
    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }
        sentinel.next = sentinel.next.next;
        size -= 1;
        // if we delete the last element, we will lose the last pointer
        if (size == 0) {
            last = sentinel;
        }
        return true;
    }
    
    public int Front() {
        if (isEmpty()) {
            return -1;
        }    
        return sentinel.next.value; 
    }
    
    public int Rear() {
        if (isEmpty()) {
            return -1;
        }
        return last.value;
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public boolean isFull() {
        return size == capacity;
    }
}
```

#### Implement

* LinkedList
* ArrayDeque

```java
public class Main {
    public static void main(String[] args) {
        // 1. Initialize a queue.
        Queue<Integer> q = new LinkedList();
        // 2. Get the first element - return null if queue is empty.
        System.out.println("The first element is: " + q.peek());
        // 3. Push new element.
        q.offer(5);
        q.offer(13);
        q.offer(8);
        q.offer(6);
        // 4. Pop an element.
        q.poll();
        // 5. Get the first element.
        System.out.println("The first element is: " + q.peek());
        // 7. Get the size of the queue.
        System.out.println("The size is: " + q.size());
    }
}
```



#### BFS

* Find the shortest path from the root node
* Traversal
* It will be important to determine the nodes and the edges before doing BFS in a specific question. Typically, the node will be an actual node or a status while the edge will be an actual edge or a possible transition.

###### shortest path

```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    // BFS
    while (queue is not empty) {
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                add next to queue;
            }
            remove the first node from queue;
        }
        step = step + 1;
    }
    return -1;          // there is no path from root to target
}
```

#### Template -- never visit a node twice

```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    Set<Node> visited;  // store all the nodes that we've visited
    int step = 0;       // number of steps neeeded from root to current node
    // initialize
    add root to queue;
    add root to visited;
    // BFS
    while (queue is not empty) {
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                if (next is not in visited) {
                    add next to queue;
                    add next to visited;
                }
            }
            remove the first node from queue;
        }
        step = step + 1;
    }
    return -1;          // there is no path from root to target
}
```

