#### Concepts

* A **spanning tree** is a connected subgraph in an undirected graph where **all vertices** are connected with the **minimum number** of edges.

* A **minimum spanning tree** is a spanning tree with the minimum possible total **edge weight** in a “weighted undirected graph”.

![img](https://leetcode.com/explore/learn/card/Figures/Graph_Explore/Minimum_Spanning_Tree.png)

#### Cut Property

* A “**cut**” is a partition of vertices in a “graph” into two disjoint subsets
* A **crossing edge** is an edge that connects a vertex in one set with a vertex in the other set. In Figure 11

* **Cut property**
  * For any cut `C` of the graph, if the weight of an edge `E` in the cut-set of `C` is strictly smaller than the weights of all other edges of the cut-set of `C`, then this edge belongs to all MSTs of the graph.



#### Kruskal's Algorithm

1. Ascending **Sort** all edges by their weight
2. Add edges in that order into the Minimum Spanning Tree. **Skip the edges that would produce cycles** in the MST
3. Repeat step 2 until **N - 1** edges are added.

###### Why greedy algorithm works?



**Sorting** edges + **UnionFind** to avoid cycle

```java
class Solution {
    // Kruskal's Algorithm
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        
        // sort edges
        List<int[]> edges = new ArrayList<>();
        for (int i = 0; i < n; i += 1) {
            for (int j = i + 1; j < n; j += 1) {
                int len = Math.abs(points[i][0] - points[j][0]) 
                    + Math.abs(points[i][1] - points[j][1]);
                edges.add(new int[]{len, i, j});
            }
        }
        Collections.sort(edges, (a, b) -> a[0] - b[0]);
        
        // UnionFind
        int minCost = 0;
        int remainEdges = n - 1;
        UnionFind uf = new UnionFind(n);
        for (int[] edge : edges) {
            int len = edge[0];
            int x = edge[1];
            int y = edge[2];
            if (uf.union(x, y)) {
                minCost += len;
                remainEdges -= 1;
            }
            
            if (remainEdges == 0) {
                break;
            }
        }
        return minCost;
    }
    
    class UnionFind {
        private int[] root;
        private int[] rank;
        
        UnionFind(int size) {
            root = new int[size];
            rank = new int[size];
            for (int i = 0; i < size ; i += 1) {
                root[i] = i;
                rank[i] = 1;
            }
        }
        
        public int find(int x) {
            if (root[x] == x) {
                return x;
            }
            return root[x] = find(root[x]);
        }
        
        public boolean union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if (rootX == rootY) {
                return false;
            }
            if (rank[rootX] > rank[rootY]) {
                root[rootY] = rootX;
            } else if(rank[rootX] < rank[rootY]) {
                root[rootX] = rootY;
            } else {
                root[rootY] = rootX;
                rank[rootX] += 1;
            }
            return true;
        }
    }
}
```

#### Prim's Algorithm

1. Start from some arbitrary **start node**
2. Repeatedly add **shortest edge** that has **one node inside the MST** under construction
3. Repeat until **N - 1** edges



Using **PriorityQueue** -- n ^ 2 log(n)

Using **minDist**[] -- n ^ 2



```java
class Solution {
    public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        int mstCost = 0;
        int edgesUsed = 0;
        
        // Track nodes which are visited.
        boolean[] inMST = new boolean[n];
        
      	// update min distance to the MST each iteration
        int[] minDist = new int[n];
        minDist[0] = 0;
        
        for (int i = 1; i < n; ++i) {
            minDist[i] = Integer.MAX_VALUE;
        }
        
        while (edgesUsed < n) {
            int currMinEdge = Integer.MAX_VALUE;
            int currNode = -1;
            
            // Pick least weight node which is not in MST.
            for (int node = 0; node < n; ++node) {
                if (!inMST[node] && currMinEdge > minDist[node]) {
                    currMinEdge = minDist[node];
                    currNode = node;
                }
            }
            
            mstCost += currMinEdge;
            edgesUsed++;
            inMST[currNode] = true;
            
            // Update adjacent nodes of current node.
            for (int nextNode = 0; nextNode < n; ++nextNode) {
                int weight = Math.abs(points[currNode][0] - points[nextNode][0]) + 
                             Math.abs(points[currNode][1] - points[nextNode][1]);
                
                if (!inMST[nextNode] && minDist[nextNode] > weight) {
                    minDist[nextNode] = weight;
                }
            }
        }
        
        return mstCost;
    }
}
```





#### The difference between the “Kruskal’s algorithm” and the “Prim’s algorithm”

* “Kruskal’s algorithm” expands the “minimum spanning tree” by adding edges. 

* Whereas “Prim’s algorithm” expands the “minimum spanning tree” by adding vertices.