#### Iterator:

```java
Iterator<Integer> iterator;
iterator.hasNext();
iterator.next();
iterator.remove();
```

##### Property

1. We only look at **one item at a time** which means that it doesn't need to store the entire data in memory.

###### LinkedList in python

```python
class LinkedListIterator:
    def __init__(self, head):
        self._node = head

    def hasNext(self):
        return self._node is not None

    def next(self):
        result = self._node.value
        self._node = self._node.next
        return result
```

2. They can represent sequences **without** even using a data structure.

###### Range (min, max)

```python
class RangeIterator:
    def __init__(self, min, max):
        self._max = max
        self._current = min

    def hasNext(self):
        return self._current < self._max

    def next(self):
        self._current += 1
        return self._current - 1
```

3. When handling an infinite sequence we counldn't even do by copying values into an array.

###### Infinite sequence

```python
class SquaresIterator:
    def __init__(self):
        self._n = 0

    def hasNext(self):
        # It continues forever,
        # so definitely has a next!
        return True

    def next(self):
        result = self._n
        self._current += 1
        return result ** 2
```

