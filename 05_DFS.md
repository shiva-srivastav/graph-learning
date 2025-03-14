**Graph DFS Traversal**

### **Problem Statement**
Given an undirected graph represented as an adjacency list, perform a Depth-First Search (DFS) traversal starting from node `0` and return the order of visited nodes.

#### **GFG Question Link**
[DFS of Graph - GeeksforGeeks](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

---

### **Approach**
1. **Initialize Data Structures:**
   - Create a boolean array `visited[]` to keep track of visited nodes.
   - Create a list `ls` to store the DFS traversal order.

2. **Perform DFS Recursively:**
   - Mark the current node as visited.
   - Add the current node to the traversal list.
   - Recur for all adjacent nodes that have not been visited.

3. **Return the Traversal Order:**
   - Once all nodes have been visited, return the `ls` list.

---

### **Code Implementation (Java)**
```java
import java.util.*;

class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> ls = new ArrayList<>();
        boolean[] visited = new boolean[adj.size()];
        
        // Start DFS from node 0
        dfs(ls, visited, adj, 0);
        
        return ls;
    }
    
    private void dfs(ArrayList<Integer> ls, boolean[] visited, ArrayList<ArrayList<Integer>> adj, int node) {
        visited[node] = true; // Mark node as visited
        ls.add(node); // Add node to traversal list
        
        for (int x : adj.get(node)) {
            if (!visited[x]) {
                dfs(ls, visited, adj, x); // Recursive DFS call
            }
        }
    }
}
```

---

### **Time Complexity Analysis**
- Each node is visited once: **O(V)**
- Each edge is traversed once in an undirected graph: **O(E)**
- **Total Time Complexity:** **O(V + E)**

### **Space Complexity Analysis**
- `visited[]` array takes **O(V)** space.
- Recursive call stack takes **O(V)** space in the worst case (if the graph is a single long path).
- **Total Space Complexity:** **O(V)** (excluding input storage)

---

### **Edge Cases Considered**
- A graph with no edges.
- A graph with disconnected components (though the function assumes connectivity from node `0`).
- A complete graph where each node is connected to every other node.

### **Summary**
- DFS is implemented recursively.
- The time complexity is **O(V + E)**.
- The space complexity is **O(V)** due to the recursion stack.
- Works efficiently for sparse and dense graphs with proper memory management.

