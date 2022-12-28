#### Basic BFS

```java
class Solution {
    // Basic BFS problem
    private final int[][] dirs = new int[][]{{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
    public int orangesRotting(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int fresh = 0; // how many fresh orrage remained -- no need to iterate again after BFS
        Queue<int[]> queue = new LinkedList<>();
        for (int i = 0; i < m; i += 1) {
            for (int j = 0; j < n; j += 1) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    fresh += 1;
                }
            }
        }
        // BFS
        int minutes = 0;
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i += 1) {
                int[] curr = queue.poll();
                int row = curr[0];
                int col = curr[1];
                for (int[] dir: dirs) {
                    int newRow = row + dir[0];
                    int newCol = col + dir[1];
                    if (0 <= newRow && newRow < m && 0 <= newCol && newCol < n 
                        && grid[newRow][newCol] == 1) {
                        grid[newRow][newCol] = 2;
                        fresh -= 1;
                        queue.offer(new int[]{newRow, newCol});
                    }
                }
            }
            minutes += 1;
        }
        
        if (fresh != 0) {
            return -1;
        } else {
            return Math.max(0, minutes - 1); // corner case [[0]] -> 0    [[2]] -> 0
        }
    }
}
```

