# **Number of Islands using BFS**

### **Problem Statement**
Given a **2D grid** consisting of `'1'` (land) and `'0'` (water), find the number of **islands**. An island is formed by connecting adjacent lands **horizontally or vertically**, and it is completely surrounded by water.

#### **LeetCode Question Link**
[Number of Islands - LeetCode](https://leetcode.com/problems/number-of-islands/)

#### **GitHub Repository (Example Implementation)**
[GitHub - Number of Islands BFS](https://github.com/your-repo/num-islands-bfs) *(Replace with actual repo if available)*

---

### **Approach**
1. **Initialize a Visited Matrix:**
   - Use a boolean `visited[][]` array to track visited land cells.

2. **Iterate Through Each Cell:**
   - If a cell contains `'1'` (land) and is **not visited**, it is part of a new island.
   - Increment the **island count** and perform **BFS** to mark all connected land cells as visited.

3. **Breadth-First Search (BFS) Traversal:**
   - Use a **queue** to process adjacent land cells.
   - Move in all **4 possible directions** (up, down, left, right).
   - If a neighboring cell is `'1'` and unvisited, mark it visited and add it to the queue.

4. **Return the Total Island Count.**

---

### **Code Implementation (Java)**
```java
import java.util.*;

class Solution {
    class Pair {
        int x;
        int y;
        Pair(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    
    public int numIslands(char[][] grid) {
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int count = 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (!visited[i][j] && grid[i][j] == '1') {
                    count++;
                    bfs(i, j, visited, grid);
                }
            }
        }
        return count;
    }
    
    public void bfs(int startX, int startY, boolean[][] visited, char[][] grid) {
        Queue<Pair> queue = new ArrayDeque<>();
        queue.add(new Pair(startX, startY));
        visited[startX][startY] = true;
        
        int[] rowDir = {-1, 1, 0, 0};
        int[] colDir = {0, 0, -1, 1};
        
        while (!queue.isEmpty()) {
            Pair myPair = queue.poll();
            int sr = myPair.x;
            int sc = myPair.y;
            
            for (int i = 0; i < 4; i++) {
                int x = sr + rowDir[i];
                int y = sc + colDir[i];
                
                if (x >= 0 && x < grid.length && y >= 0 && y < grid[0].length && !visited[x][y] && grid[x][y] == '1') {
                    queue.add(new Pair(x, y));
                    visited[x][y] = true;
                }
            }
        }
    }
}
```

---

### **Time Complexity Analysis**
- **Iterating through the grid:** **O(N × M)** (where `N` is rows and `M` is columns)
- **BFS Traversal:** **O(N × M)** (Each cell is visited once in the worst case)
- **Total Time Complexity:** **O(N × M)**

### **Space Complexity Analysis**
- **Visited array:** **O(N × M)**
- **Queue (Worst Case - Entire Grid is an Island):** **O(N × M)**
- **Total Space Complexity:** **O(N × M)**

---

### **Edge Cases Considered**
- A grid with **no land** (all `'0'`).
- A grid where **each cell is an island** (every `'1'` is separate).
- A **large single island** covering the entire grid.
- A **sparse island grid** with isolated clusters.

### **Summary**
- BFS is used to explore all connected land cells efficiently.
- Time complexity is **O(N × M)**.
- Space complexity is **O(N × M)** due to the queue and visited array.
- Works well for moderate grid sizes but may require optimizations for very large inputs.

Would you like an optimized **DFS** version as well? 🚀

