### Single source shortest path

1. Dijkstra's Algorithm
2. Bellman Ford Algorithm
   * **negative** weights



#### Dijkstra's Algorithm

* weighted graph
* nonnegative edge weights
* **Greedy**
* PriorityQueue

##### Edge Relaxation

* add edge to the SPT only if that edge yields better distance

###### Typical Dijkstra's

```java
		private void dijkstra(Map<Integer, List<int[]>> adj, int source, int n, int source) {
      	int[] distance = new int[n];
      	for (int i = 0; i < n; i++)
            distance[i] = Integer.MAX_VALUE;
      	// [distance, nodeIndex]
        Queue<int[]> pq = new PriorityQueue<int[]>((a, b) -> a[0] - b[0]);
        pq.add(new int[]{0, source});
        
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();          
            int currNode = curr[1];
            int currDistance = curr[0];
            
            if (currDistance > distance[currNode]) {
                continue;
            }
            
            if (!adj.containsKey(currNode)) {
              	// end node
                continue;
            }
            
            for (int[] edge : adj.get(currNode)) {
                int dist = edge[0];
                int neighbor = edge[1];
                
                // Relaxation
                if (distance[neighbor] > currDistance + dist) {
                    distance[neighbor] = currDistance + dist;
                    pq.add(new int(distance[neighborNode], neighborNode));
                }
            }
        }
    }
```



#### Bellman-Ford algorithm

* directed acyclic graph (DAG)

##### Basic theory

* In a "graph with **no negative-weight cycles**" with N vertices, the shortest path between any two vertices has at most N - 1 edges.
* In a “graph with negative weight cycles”, there is no shortest path.

##### Dynamic Programming

![image-20220517180942645](/Users/morningstar/Library/Application Support/typora-user-images/image-20220517180942645.png)

> Time complexity: $O(V * E)$
>
> Space complexity: $O(V * V)$
>
> V: vertices, E edges



##### Bellman-Ford: 2 improvement

![image-20220517182434647](/Users/morningstar/Library/Application Support/typora-user-images/image-20220517182434647.png)

###### How to detect "negative weight cycles"

**Detection method**: After relaxing each edge `N-1` times, perform the `N`th relaxation. According to the “Bellman-Ford algorithm”, all distances must be the shortest after relaxing each edge `N-1` times. However, after the `N`th relaxation, if there exists `distances[u] + weight(u, v) < distances(v)` for any `edge(u, v)`, it means there is a shorter path . At this point, we can conclude that there exists a “negative weight cycle”.

> Time complexity: $O(V * E)$
>
> Space complexity: $O(V)$
>
> V: vertices, E edges

###### Limitations of the Bellman-Ford Algorithm

* The order of the edges we choose influnce the efficiency



##### SPFA algorithm

* The shortest Path Faster Algorithm(SPFA algorithm)
* Using **Queue**

> The “SPFA” Algorithm uses a “queue” to maintain the next starting vertex of the edge to be traversed. Only when the shortest distance of a vertex is relaxed and that the vertex is not in the “queue”, we **add the vertex** to the queue. We iterate the process until the queue is empty. At this point, we have calculated the minimum distance from the given vertex to any vertices.

* If $u \to v$ changed the shortest path to $v$, the vertices after $v$ may also changed, so we need to add $v$ to the queue for later operation

> Time complexity: $O(V * E)$
>
> Space complexity: $O(V)$
>
> V: vertices, E edges