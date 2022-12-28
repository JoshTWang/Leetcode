#### DFS in graph theory

1. Traverse **all vertices** in a “graph”;
2. Traverse **all paths between any two vertices** in a “graph”.

#### Traversing all Vertices

- Time Complexity: **O(V + E)**. Here, V represents the number of vertices, and E represents the number of edges. We need to check every vertex and traverse through every edge in the graph.
- Space Complexity: **O(V)**. Either the manually created stack or the recursive call stack can store up to V vertices.

####  Traversing all paths between two vertices 

- Time Complexity: **O((V - 1)!)** The above example is for an undirected graph. The worst-case scenario, when trying to find all paths, is a complete graph. A complete graph is a graph where every vertex is connected to every other vertex.

* Space Complexity: O(V^3)