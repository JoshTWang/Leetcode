#### Question

* How could we quickly check whether two vertives are connected?
* The primary use of disjoint sets is to address the **connectivity** between the components of a network.

#### Two important function

* The **find** function
  * finds the root node of a given vertex
* The **union** function
  * Union two vertices and makes their root nodes the same

#### Implement

```java
public class UnionFind {
    // Constructor of Union-find. The size is the length of the root array.
    public UnionFind(int size) {}
    public int find(int x) {}
    public void union(int x, int y) {}
    public boolean connected(int x, int y) {}
}
```

##### Find

```java
public int find(int x) {
    if (x == root[x]) {
        return x;
    }
    return root[x] = find(root[x]);
}
```

##### Union

```java
public void union(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);
    if (rootX != rootY) {
        if (rank[rootX] > rank[rootY]) {
            root[rootY] = rootX;
        } else if (rank[rootX] < rank[rootY]) {
            root[rootX] = rootY;
        } else {
            root[rootY] = rootX;
            rank[rootX] += 1;
        }
    }
}
```



#### QuickFind

* Each call to `find` will requireO(1) time since we are just accessing an element of the array at the given index.
* Each call to `union` will require O*(*N) time because we need to **traverse** through the entire array and update the root vertices for all the vertices of the set that is going to be merged into another set.

|                     | Union-find Constructor | Find   | Union    | Connected |
| ------------------- | ---------------------- | ------ | -------- | --------- |
| **Time Complexity** | *O*(*N*)               | *O*(1) | *O*(*N*) | *O*(1)    |

```java
// UnionFind.class
class UnionFind {
    private int[] root;

    public UnionFind(int size) {
        root = new int[size];
        for (int i = 0; i < size; i++) {
            root[i] = i;
        }
    }

    public int find(int x) {
        return root[x];
    }
		
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            for (int i = 0; i < root.length; i++) {
                if (root[i] == rootY) {
                    root[i] = rootX;
                }
            }
        }
    }

    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}
```

#### QuickUnion

- For the `find` operation, in the worst-case scenario, we need to traverse every vertex to find the root for the input vertex. The maximum number of operations to get the root vertex would be no more than the tree's height, so it will take O*(*N) time.
- The `union` operation consists of two `find` operations which (**only in the worst-case**) will take O(N) time, and two constant time operations, including the equality check and updating the array value at a given index. Therefore, the `union` operation also costs O(N)*O*(*N*) in the worst-case.

|                     | Union-find Constructor | Find     | Union    | Connected |
| ------------------- | ---------------------- | -------- | -------- | --------- |
| **Time Complexity** | *O*(N)                 | *O*(*N*) | *O*(*N*) | *O*(*N*)  |

```java
class UnionFind {
    private int[] root;

    public UnionFind(int size) {
        root = new int[size];
        for (int i = 0; i < size; i++) {
            root[i] = i;
        }
    }

    public int find(int x) {
        while (x != root[x]) {
            x = root[x];
        }
        return x;
    }

    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            root[rootY] = rootX;
        }
    }

    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}
```

#### Union by rank

|                     | Union-find Constructor | Find        | Union       | Connected   |
| ------------------- | ---------------------- | ----------- | ----------- | ----------- |
| **Time Complexity** | *O*(*N*)               | *O*(log*N*) | *O*(log*N*) | *O*(log*N*) |

#### Path Compression Optimization

* After finding the root node, we can update the parent node of all traversed elements to their root node.



#### Final Version

```java
// UnionFind.class
class UnionFind {
    private int[] root;
    // Use a rank array to record the height of each vertex, i.e., the "rank" of each vertex.
    private int[] rank;

    public UnionFind(int size) {
        root = new int[size];
        rank = new int[size];
        for (int i = 0; i < size; i++) {
            root[i] = i;
            rank[i] = 1; // The initial "rank" of each vertex is 1, because each of them is
                         // a standalone vertex with no connection to other vertices.
        }
    }

	// The find function here is the same as that in the disjoint set with path compression.
    public int find(int x) {
        if (x == root[x]) {
            return x;
        }
        return root[x] = find(root[x]);
    }

	// The union function with union by rank
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] > rank[rootY]) {
                root[rootY] = rootX;
            } else if (rank[rootX] < rank[rootY]) {
                root[rootX] = rootY;
            } else {
                root[rootY] = rootX;
                rank[rootX] += 1;
            }
        }
    }

    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}

// App.java
// Test Case
public class App {
    public static void main(String[] args) throws Exception {
        UnionFind uf = new UnionFind(10);
        // 1-2-5-6-7 3-8-9 4
        uf.union(1, 2);
        uf.union(2, 5);
        uf.union(5, 6);
        uf.union(6, 7);
        uf.union(3, 8);
        uf.union(8, 9);
        System.out.println(uf.connected(1, 5)); // true
        System.out.println(uf.connected(5, 7)); // true
        System.out.println(uf.connected(4, 9)); // false
        // 1-2-5-6-7 3-8-9-4
        uf.union(9, 4);
        System.out.println(uf.connected(4, 9)); // true
    }
}
```

