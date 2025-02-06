# **Rotten Oranges - BFS Approach**

## **Problem Statement**
Given a **matrix** where:
- `0` represents an **empty cell**.
- `1` represents a **fresh orange**.
- `2` represents a **rotten orange**.

A rotten orange can **infect adjacent fresh oranges** in **one unit of time** (left, right, up, down).
The task is to determine the **minimum time** required to rot all oranges. If it is **impossible** to rot all fresh oranges, return `-1`.

🔗 **Problem Link:** [Rotten Oranges - GeeksforGeeks](https://www.geeksforgeeks.org/problems/rotten-oranges2536)

---

## **Approach (Breadth-First Search - BFS)**
### **1️⃣ Identify Initial Rotten Oranges & Count Fresh Oranges**
- Traverse the matrix to **find all rotten oranges** and push them into a queue.
- Count the **total number of fresh oranges**.

### **2️⃣ Perform BFS (Level-wise Traversal)**
- **Start BFS** using the queue containing all initial rotten oranges.
- Each level of BFS represents **one unit of time**.
- For each rotten orange in the queue, **infect adjacent fresh oranges** and push them into the queue.
- Keep track of the **maximum time taken**.

### **3️⃣ Check If Any Fresh Oranges Remain**
- If all fresh oranges are infected (`freshCount == 0`), return **the time taken**.
- Otherwise, return `-1` (some oranges could not be infected).

---

## **Java Implementation**
```java
import java.util.ArrayDeque;

class Solution {
    // Function to find minimum time required to rot all oranges.
    public int orangesRotting(int[][] mat) {
        return bfs(mat);
    }

    class Pair<T, U> {
        T x;
        U y;

        Pair(T x, U y) {
            this.x = x;
            this.y = y;
        }
    }

    public int bfs(int[][] mat) {
        ArrayDeque<Pair<Pair<Integer, Integer>, Integer>> queue = new ArrayDeque<>();
        int freshCount = 0;

        // Step 1: Add all initially rotten oranges to the queue and count fresh oranges
        for (int i = 0; i < mat.length; i++) {
            for (int j = 0; j < mat[0].length; j++) {
                if (mat[i][j] == 2) {
                    queue.add(new Pair<>(new Pair<>(i, j), 0));
                } else if (mat[i][j] == 1) {
                    freshCount++;
                }
            }
        }

        // Step 2: Handle edge cases
        if (freshCount == 0) return 0; // No fresh oranges
        if (queue.isEmpty()) return -1; // No rotten oranges to start infection

        int rowDirection[] = {0, -1, 1, 0};
        int colDirection[] = {-1, 0, 0, 1};
        int maxLevel = 0;

        // Step 3: BFS to rot fresh oranges
        while (!queue.isEmpty()) {
            Pair<Pair<Integer, Integer>, Integer> pair = queue.poll();
            int x = pair.x.x;
            int y = pair.x.y;
            int level = pair.y;

            for (int i = 0; i < 4; i++) {
                int row = x + rowDirection[i];
                int col = y + colDirection[i];

                if (row >= 0 && col >= 0 && row < mat.length && col < mat[0].length && mat[row][col] == 1) {
                    queue.add(new Pair<>(new Pair<>(row, col), level + 1));
                    maxLevel = Math.max(level + 1, maxLevel);
                    freshCount--;
                    mat[row][col] = 2; // Mark as rotten
                }
            }
        }

        // Step 4: If there are remaining fresh oranges, return -1
        return freshCount == 0 ? maxLevel : -1;
    }
}
```

---

## **Complexity Analysis**
- **Time Complexity**: **O(N × M)**
  - Every cell is processed at most **once**.
  - BFS traversal takes **O(N × M)** in the worst case.
- **Space Complexity**: **O(N × M)** (Queue for BFS traversal).

---

## **Edge Cases Considered**
✅ No fresh oranges → Return `0` (all already rotten or empty).
✅ Fresh oranges exist, but no rotten ones → Return `-1` (impossible to rot).
✅ All oranges are already rotten → Return `0`.
✅ Fresh oranges in isolated positions → Return `-1`.

---

## **Key Takeaways**
- **BFS is the optimal approach** since it spreads infection level-wise.
- **Tracking fresh oranges (`freshCount`) helps determine when to stop BFS.**
- **Marking oranges as rotten (`mat[row][col] = 2`) prevents redundant processing.**

This ensures an **efficient and correct solution** to the problem! 🚀

