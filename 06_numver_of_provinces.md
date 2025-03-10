# **Number of Provinces (Graph) - Striver's Approach in Java**

## **Problem Statement**
Given an **n x n** matrix `isConnected` representing a graph, where `isConnected[i][j] = 1` indicates a direct connection between city `i` and city `j`, find the **number of provinces** (connected components in the graph).

### **Understanding the Problem**
- Each city is a node.
- A direct connection represents an edge.
- A **province** is a connected component in the graph.
- Our goal is to count how many such connected components exist.

---

## **Approach to Solve the Problem**
This is a **graph traversal problem** where we need to find **connected components**. 
We can solve this using:
1. **DFS (Depth First Search)**
2. **BFS (Breadth First Search)**
3. **Disjoint Set Union (Union-Find)**

---

## **1. DFS Approach (Recursive)**
### **Algorithm:**
1. Create an adjacency list from the `isConnected` matrix.
2. Maintain a `visited` array to track visited nodes.
3. For each unvisited node, perform a **DFS** traversal to mark all connected nodes.
4. Count the number of DFS calls, which represents the number of connected components (provinces).

```java
import java.util.*;

class NumberOfProvincesDFS {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(isConnected, visited, i);
                provinces++;
            }
        }
        return provinces;
    }

    private void dfs(int[][] isConnected, boolean[] visited, int node) {
        visited[node] = true;
        for (int neighbor = 0; neighbor < isConnected.length; neighbor++) {
            if (isConnected[node][neighbor] == 1 && !visited[neighbor]) {
                dfs(isConnected, visited, neighbor);
            }
        }
    }
}
```

---

## **2. BFS Approach (Using Queue)**
### **Algorithm:**
1. Use a queue to implement **BFS traversal**.
2. For each unvisited node, explore all connected nodes using BFS.
3. Count the number of BFS calls, which represents the number of provinces.

```java
import java.util.*;

class NumberOfProvincesBFS {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                bfs(isConnected, visited, i);
                provinces++;
            }
        }
        return provinces;
    }
}
```

---

## **3. Disjoint Set (Union-Find) Approach**
### **Algorithm:**
1. Implement **Disjoint Set Union (DSU)** (also called Union-Find).
2. Use **path compression** for efficient `find` operations.
3. Use **union by rank** to merge connected components.
4. The number of unique roots in DSU represents the number of provinces.

```java
class DisjointSet {
    private int[] parent;
    private int[] rank;
}
```

---

## **Time Complexity Analysis**
- **DFS & BFS:** O(N²) in worst case (for dense graphs)
- **Union-Find:** O(N²) in worst case, but with path compression, it performs almost O(N).

---

## **Problem Links (Practice Questions)**
### **LeetCode:**
- [Number of Provinces](https://leetcode.com/problems/number-of-provinces/)

### **GeeksforGeeks:**
- [Find the number of Provinces](https://www.geeksforgeeks.org/number-of-provinces-disjoint-set/)

Let me know if you need any modifications or further explanations! 🚀

