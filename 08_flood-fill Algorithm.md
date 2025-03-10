# **Flood Fill Algorithm (BFS Approach)**

## **Problem Statement**
Given a **2D image represented as a grid** of integers, implement the **Flood Fill Algorithm**. The algorithm starts from a given pixel `(sr, sc)` and changes the color of that pixel and all its connected neighboring pixels **(4-directionally connected)** with the same original color to a new color.

---

## **Approach Used: Breadth-First Search (BFS)**
### **Concepts Used**
1. **Graph Representation:** The given grid is treated as a **graph**, where each pixel is a node and adjacent pixels are edges.
2. **BFS Traversal:** We use BFS to explore all **connected** pixels having the same original color.
3. **Queue-Based Processing:** The BFS queue ensures that we process each valid pixel once, preventing infinite loops.

---

## **Algorithm**
1. Store the **original color** of the starting pixel `(sr, sc)`.
2. If `newColor == originalColor`, **return immediately** (to prevent redundant processing).
3. Initialize a **queue** with the starting pixel and set its color to `newColor`.
4. Use **BFS traversal** to explore **4-directionally** adjacent pixels:
   - If a neighboring pixel has the **same original color**, change its color and push it into the queue.
5. Continue the process until all reachable pixels have been updated.

---

## **Implementation (Java)**
```java
import java.util.*;

class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        bfs(image, sr, sc, newColor);
        return image;
    }
    
    // Helper class to store (x, y) coordinates
    class Pair {
        int x, y;
        Pair(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }
    
    private void bfs(int[][] image, int sr, int sc, int newColor) {
        int originalColor = image[sr][sc];
        if (originalColor == newColor) return; // Edge case: No need to fill
        
        Queue<Pair> queue = new ArrayDeque<>();
        queue.add(new Pair(sr, sc));
        image[sr][sc] = newColor; // Change the color immediately
        
        // Define 4 possible directions (Up, Left, Right, Down)
        int[] rowDirection = {-1, 0, 0, 1};
        int[] colDirection = {0, -1, 1, 0};
        
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            int x = pair.x;
            int y = pair.y;
            
            for (int i = 0; i < 4; i++) {
                int newX = x + rowDirection[i];
                int newY = y + colDirection[i];
                
                // Check if the new position is valid
                if (newX >= 0 && newY >= 0 && newX < image.length && newY < image[0].length && 
                    image[newX][newY] == originalColor) {
                    queue.add(new Pair(newX, newY));
                    image[newX][newY] = newColor; // Change color after adding to queue
                }
            }
        }
    }
}
```

---

## **Explanation of Code**
### **1. BFS Traversal**
- **Queue-Based Processing:** Ensures that each valid pixel is visited exactly once.
- **Prevents Infinite Loops:** We only visit pixels with the **original color** and mark them immediately upon adding to the queue.

### **2. Coordinate Class**
- A **helper class `Pair`** stores `(x, y)` coordinates for easy BFS traversal.

### **3. Using BFS for Optimal Traversal**
- **Ensures all connected pixels are processed level by level.**
- **Avoids recursion depth issues compared to DFS.**

### **4. Time Complexity Analysis**
- Each pixel is **visited once**, so the **time complexity is O(N×M)**, where `N` is the number of rows and `M` is the number of columns.
- **Space Complexity:** O(N×M) due to the **visited pixels queue**.

---

## **Example Walkthrough**
### **Input Grid Before Flood Fill:**
```
1 1 0
1 1 0
0 0 1
```
### **Flood Fill Operation:**
- Start from `(0,0)` with `newColor = 2`.
- All **4-connected** `1`s are filled.

### **Output Grid After Flood Fill:**
```
2 2 0
2 2 0
0 0 1
```

---

## **Edge Cases Considered**
✅ **No color change required (newColor == originalColor)**
✅ **Single-pixel grid**
✅ **Grid already filled with `newColor`**
✅ **Large grid size to test performance**

---

### **Additional Resources**
For more insights, refer to: [GeeksforGeeks - Flood Fill Algorithm](https://www.geeksforgeeks.org/problems/flood-fill-algorithm1856)

---

### **Final Thoughts**
- **Breadth-First Search (BFS) ensures an optimal way to visit all connected pixels efficiently.**
- **Using a queue prevents stack overflow issues that arise with DFS.**

🚀 **Now you have a fully optimized flood fill solution with BFS!**

