# **Cycle Detection in an Undirected Graph (BFS & DFS Approach)**

## **Problem Statement**
Given an **undirected graph**, detect if there exists a **cycle**.

A **cycle** in an undirected graph occurs when a node is **revisited** while traversing the graph, without being the immediate parent of the current node.

---

## **1️⃣ Cycle Detection Using BFS**
### **Approach (Breadth-First Search - BFS)**

### **Steps:**
1. Use a **boolean visited array** to track visited nodes.
2. Traverse each unvisited node using **BFS**.
3. Maintain a **queue storing pairs** (node, parent) to track previous connections.
4. If a visited node is encountered **that is not the parent**, a cycle is detected.
5. Continue BFS until all nodes are visited.

### **Java Implementation (BFS Cycle Detection)**
```java
import java.util.*;

class Solution {
    public boolean isCycle(ArrayList<ArrayList<Integer>> adj) {
        boolean[] visited = new boolean[adj.size()];

        for (int i = 0; i < adj.size(); i++) {
            if (!visited[i]) {
                if (bfs(adj, visited, i)) {
                    return true;
                }
            }
        }
        return false;
    }

    class Pair {
        int parent;
        int current;

        Pair(int parent, int current) {
            this.parent = parent;
            this.current = current;
        }
    }

    private boolean bfs(ArrayList<ArrayList<Integer>> adj, boolean[] visited, int input) {
        ArrayDeque<Pair> queue = new ArrayDeque<>();
        queue.add(new Pair(-1, input));
        visited[input] = true;

        while (!queue.isEmpty()) {
            Pair pair = queue.poll();
            int in = pair.current;
            int parent = pair.parent;

            for (int x : adj.get(in)) {
                if (visited[x] && parent != x) {
                    return true; // Cycle detected
                } else if (!visited[x]) {
                    queue.add(new Pair(in, x));
                    visited[x] = true;
                }
            }
        }
        return false;
    }
}
```

---

## **2️⃣ Cycle Detection Using DFS**
### **Approach (Depth-First Search - DFS)**

### **Steps:**
1. Use a **boolean visited array** to track visited nodes.
2. Perform **DFS traversal** for each unvisited node.
3. Maintain a **parent reference** to track the previous node.
4. If a visited node is encountered **that is not the parent**, a cycle is detected.
5. Continue DFS traversal until all nodes are visited.

### **Java Implementation (DFS Cycle Detection)**
```java
import java.util.*;

class Solution {
    public boolean isCycle(ArrayList<ArrayList<Integer>> adj) {
        boolean[] visited = new boolean[adj.size()];

        for (int i = 0; i < adj.size(); i++) {
            if (!visited[i]) {
                if (dfs(adj, visited, i, -1)) {
                    return true;
                }
            }
        }
        return false;
    }

    private boolean dfs(ArrayList<ArrayList<Integer>> adj, boolean[] visited, int node, int parent) {
        visited[node] = true;

        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                if (dfs(adj, visited, neighbor, node)) {
                    return true;
                }
            } else if (neighbor != parent) {
                return true; // Cycle detected
            }
        }
        return false;
    }
}
```

---

## **Complexity Analysis**
### **Time Complexity**
- **BFS & DFS:** **O(V + E)** (Each vertex and edge are processed once)

### **Space Complexity**
- **BFS:** **O(V)** (Queue for BFS traversal)
- **DFS:** **O(V)** (Recursive call stack depth)

---

## **Edge Cases Considered**
✅ Graph with **no edges** → No cycle detected.  
✅ **Disconnected graph** with multiple components.  
✅ **Graph with multiple cycles** → Correctly identifies cycle presence.  
✅ **Graph with a single cycle** → Detects cycle successfully.  

---

## **Key Takeaways**
- **DFS is preferred** for cycle detection due to its stack-based traversal.
- **BFS works equally well**, but requires tracking parent nodes explicitly.
- **Handling visited nodes correctly** prevents false cycle detection.

This ensures an **efficient and correct solution** for cycle detection in an undirected graph! 🚀

