In LinkedList or ArrayList, add() will add in the end. -- add() = addLast()

#### Abstract

* `Stack<Integer> s = new Stack<>();`
* `stack.push()`
* `stack.pop()`
* `stack.peek()`
* `stack.size()`



#### Stack

* In a LIFO data structure, `the newest element added to the queue will be processed first`.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/03/screen-shot-2018-06-02-at-203523.png)

#### Reinvent the wheel

```java
// "static void main" must be defined in a public class.
class MyStack {
    private List<Integer> data;               // store elements
    public MyStack() {
        data = new ArrayList<>();
    }
    /** Insert an element into the stack. */
    public void push(int x) {
        data.add(x);
    }
    /** Checks whether the queue is empty or not. */
    public boolean isEmpty() {
        return data.isEmpty();
    }
    /** Get the top item from the queue. */
    public int top() {
        return data.get(data.size() - 1);
    }
    /** Delete an element from the queue. Return true if the operation is successful. */
    public boolean pop() {
        if (isEmpty()) {
            return false;
        }
        data.remove(data.size() - 1);
        return true;
    }
};

public class Main {
    public static void main(String[] args) {
        MyStack s = new MyStack();
        s.push(1);
        s.push(2);
        s.push(3);
        for (int i = 0; i < 4; ++i) {
            if (!s.isEmpty()) {
                System.out.println(s.top());
            }
            System.out.println(s.pop());
        }
    }
}
```

#### Implement

```java
// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        // 1. Initialize a stack.
        Stack<Integer> s = new Stack<>();
        // 2. Push new element.
        s.push(5);
        s.push(13);
        s.push(8);
        s.push(6);
        // 3. Check if stack is empty.
        if (s.empty() == true) {
            System.out.println("Stack is empty!");
            return;
        }
        // 4. Pop an element.
        s.pop();
        // 5. Get the top element.
        System.out.println("The top element is: " + s.peek());
        // 6. Get the size of the stack.
        System.out.println("The size is: " + s.size());
    }
}
```

#### DFS

###### Recursive

* we are using the implicit stack provided by the system, also known as the [Call Stack](https://en.wikipedia.org/wiki/Call_stack).

```java
/*
 * Return true if there is a path from cur to target.
 */
boolean DFS(Node cur, Node target, Set<Node> visited) {
    return true if cur is target;
    for (next : each neighbor of cur) {
        if (next is not in visited) {
            add next to visted;
            return true if DFS(next, target, visited) == true;
        }
    }
    return false;
}
```

###### Iteration with stack

```java
/*
 * Return true if there is a path from cur to target.
 */
boolean DFS(int root, int target) {
    Set<Node> visited;
    Stack<Node> stack;
    add root to stack;
    while (stack is not empty) {
        Node cur = the top element in stack;
        remove the cur from the stack;
        return true if cur is target;
        for (Node next : the neighbors of cur) {
            if (next is not in visited) {
                add next to visited;
                add next to stack;
            }
        }
    }
    return false;
}
```



### Conclusion

In previous chapters, we have introduced two data structures: Queue and Stack.

#### 1. Queue

`Queue` is a `FIFO` data structure: the first element will be processed first. There are two important operations: enqueue and dequeue. We can use a dynamic array with two pointers to implement a queue.

We can use a queue to implement `Breadth-first Search` (BFS).

There are also some important extensions of the queue. For example,

- Dequeue
- Priority Queue

We will introduce these structures in later cards.

#### 2. Stack

`Stack` is a `LIFO` data structure: the last element will be processed first. There are two important operations: push and pop. The implementation of stack is quite simple. A dynamic array will be enough to implement a stack.

We use stack when `LIFO` principle is satisfied. `Depth-first Search` (DFS) is an important applications of stack.

#### 3. Summary

To summarize, you should be able to understand and compare the following concepts:

- FIFO and LIFO;
- Queue and Stack;
- BFS and DFS.