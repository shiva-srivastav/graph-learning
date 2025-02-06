# **Number of Islands (BFS Approach)**

## **Problem Statement**
Given a 2D grid map of **'1' (land)** and **'0' (water)**, return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands **horizontally, vertically, or diagonally**. You may assume that all four edges of the grid are all surrounded by water.

---

## **Approach Used: Breadth-First Search (BFS)**
### **Concepts Used**
1. **Graph Representation:** The given grid is treated as a graph where each **'1' (land)** is a node, and adjacent land nodes are connected.
2. **BFS Traversal:** We use BFS to explore all connected components of land, marking them as visited.
3. **Connected Components Counting:** Each BFS traversal represents discovering a new island, and we increment the island count accordingly.

---

## **Algorithm**
1. Create a **visited[][]** boolean array to track visited cells.
2. Traverse the grid using a nested loop.
3. If a cell contains **'1'** (land) and hasn't been visited:
   - Perform **BFS traversal** from that cell.
   - Mark all connected land cells as visited.
   - Increment the island count.
4. BFS explores adjacent cells **(up, down, left, right, and diagonals)** until all connected land cells are marked.

---

## **Implementation (Java)**
```java
import java.util.*;

class Solution {
    public int numIslands(char[][] grid) {
        boolean[][] visited = new boolean[grid.length][grid[0].length];
        int islandCount = 0;

        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1' && !visited[i][j]) {
                    bfs(grid, visited, new Coordinate(i, j));
                    islandCount++;
                }
            }
        }
        return islandCount;
    }

    // Helper class to store x, y coordinates
    class Coordinate {
        int row, col;
        Coordinate(int row, int col) {
            this.row = row;
            this.col = col;
        }
    }

    void bfs(char[][] grid, boolean[][] visited, Coordinate start) {
        Queue<Coordinate> queue = new ArrayDeque<>();
        queue.add(start);
        visited[start.row][start.col] = true;

        for (int row = -1; row <= 1; row++) {
            for (int col = -1; col <= 1; col++) {
                if (row == 0 && col == 0) continue; // Skip the current cell

                int[] rowDirection = {-1, 0, 1, 0, -1, -1, 1, 1};
                int[] colDirection = {0, -1, 0, 1, -1, 1, -1, 1};

                while (!queue.isEmpty()) {
                    Coordinate current = queue.poll();
                    int x = current.row, y = current.col;

                    for (int d = 0; d < 8; d++) {
                        int xCh = x + rowDirection[d];
                        int yCh = y + colDirection[d];

                        if (xCh >= 0 && xCh < grid.length && 
                            yCh >= 0 && yCh < grid[0].length && 
                            grid[xCh][yCh] == '1' && !visited[xCh][yCh]) {
                            
                            visited[xCh][yCh] = true;
                            queue.add(new Coordinate(xCh, yCh));
                        }
                    }
                }
            }
        }
    }
}
```

---

## **Explanation of Code**
### **1. BFS Traversal**
- We use **a queue** to explore connected land cells.
- When a **'1' (land)** is found, BFS starts, marking all reachable land cells as visited.

### **2. Coordinate Class**
- A **helper class `Coordinate`** stores `(row, col)` for easy referencing in the BFS queue.

### **3. Traversing Adjacent Cells**
- The **nested loop** iterates over 8 directions **(up, down, left, right, and diagonals)**.

### **4. Time Complexity Analysis**
- Each cell is **visited once**, so the **time complexity is O(N×M)**, where `N` is rows and `M` is columns.
- **Space Complexity:** O(N×M) due to the **visited[][] array** and BFS queue.

---

## **Example Walkthrough**
### **Input Grid:**
```
11000
11000
00100
00011
```
### **Step-by-Step Execution:**
1. Start at `(0,0)`, run BFS → Mark connected **land cells**.
2. Find next unvisited **'1'**, run BFS → Discover new island.
3. Repeat until all **land cells are processed**.

### **Output:**
```
Number of islands: 3
```

---

## **Edge Cases Considered**
✅ Single-row or single-column grid.
✅ No islands (all water).
✅ All land (one big island).
✅ Large grid sizes to test performance.

---

### **Additional Resources**
For more insights, refer to: [GeeksforGeeks - Find the Number of Islands](https://www.geeksforgeeks.org/problems/find-the-number-of-islands/)

---

### **Final Thoughts**
- **Breadth-First Search (BFS) ensures we visit each island component once, making it optimal for this problem.**
- **Using a queue prevents recursion depth issues that might arise with DFS in large grids.**

🚀 **Now you have a fully optimized solution with detailed explanations!**

