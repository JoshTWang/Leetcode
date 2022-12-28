# Python

### Array

- `[0] * 26`
- `[[0] * 26 for _ in range(26)]` -- 2D array



### Set & Map

- HashSet is just set
  - `hashset = set()`

- HashMap is just dictionary
  - `hashmap = {}`



#### Queue & Stack

```py
>>> from collections import deque
>>> stack = deque()
>>> stack.append(10)
>>> stack.append(20)
>>> stack.append(30)
>>> stack
deque([10, 20, 30])
>>> stack.pop()           # LIFO
30
>>> stack.pop()
20
>>> 
>>> queue = deque()
>>> queue.append(10)
>>> queue.append(20)
>>> queue.append(30)
>>> queue
deque([10, 20, 30])
>>> queue.popleft()       # FIFO
10
>>> queue.popleft()
20
```



#### ord()

- give back unicode
