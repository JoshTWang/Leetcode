#### A template from LC 207

```java
class Solution {
    // DFS + cycle detection
    enum Color { GRAY, BLACK }; // null is white
    Map<Integer, List<Integer>> adjList;
    Color[] states;
    
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        // step 1) build the graph
        this.adjList = new HashMap<>();
        for (int[] edge : prerequisites) {
            int src = edge[1];
            int dest = edge[0];
            adjList.putIfAbsent(src, new ArrayList<>());
            adjList.get(src).add(dest);
        }
        
        // step 2) cycle detection
        this.states = new Color[numCourses];
        for (int i = 0; i < numCourses; i++) {
            if (states[i] == null && !acycle(i)) {
                return false;
            }
        }
        return true;
    }
    
    private boolean acycle (int curr) {
        // base case
        if (states[curr] != null) {
            return states[curr] == Color.BLACK;
        }
        
        // recurrence relation
        states[curr] = Color.GRAY; // processing
        
        if (adjList.get(curr) != null) {
            for (int next : adjList.get(curr)) {
                if (!acycle(next)) {
                    return false;
                }
            }
        }
        
        states[curr] = Color.BLACK; // visited
        return true;
    }
}
```

