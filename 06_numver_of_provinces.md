**Number of Provinces using DFS**

### **Problem Statement**
Given an **N x N** adjacency matrix representing a graph, determine the number of **provinces** (i.e., connected components). A province is a group of directly or indirectly connected cities, where connectivity is represented by a **1** in the adjacency matrix.

#### **LeetCode Question Link**
[Number of Provinces - LeetCode](https://leetcode.com/problems/number-of-provinces/)

#### **GeeksforGeeks Question Link**
[Number of Provinces - GeeksforGeeks](https://www.geeksforgeeks.org/find-the-number-of-provinces/)

---

### **Approach**
1. **Convert Adjacency Matrix to Adjacency List:**
   - Since the input is an adjacency matrix, first convert it into an adjacency list.
   - If `adj[i][j] == 1`, then node `i` is connected to node `j`.

2. **Perform DFS to Count Connected Components:**
   - Initialize a `visited[]` array to track visited nodes.
   - For each unvisited node, increment the province count and perform DFS to mark all connected nodes as visited.

3. **Return the Number of Provinces:**
   - The count of DFS calls corresponds to the number of provinces.

---

### **Code Implementation (Java)**
```java
import java.util.*;

class Solution {
    static int numProvinces(ArrayList<ArrayList<Integer>> adj, int V) {
        ArrayList<ArrayList<Integer>> copyAdj = new ArrayList<>();
        
        // Convert adjacency matrix to adjacency list
        for (int i = 0; i < adj.size(); i++) {
            ArrayList<Integer> ls = new ArrayList<>();
            for (int j = 0; j < adj.get(0).size(); j++) {
                if (adj.get(i).get(j) != 0) {
                    ls.add(j);
                }
            }
            copyAdj.add(ls);
        }
        
        boolean visited[] = new boolean[adj.size()];
        int count = 0;
        
        // Perform DFS on unvisited nodes
        for (int i = 0; i < copyAdj.size(); i++) {
            if (!visited[i]) {
                count++;
                dfs(copyAdj, i, visited);
            }
        }
        return count;
    }
    
    static void dfs(ArrayList<ArrayList<Integer>> adj, int node, boolean[] visited) {
        visited[node] = true;
        for (int x : adj.get(node)) {
            if (!visited[x]) {
                dfs(adj, x, visited);
            }
        }
    }
}
```

---

### **Time Complexity Analysis**
- **Converting Matrix to Adjacency List:** **O(V²)** (Iterating over all `V × V` elements)
- **DFS Traversal:** **O(V + E)** (Each node and edge are visited once)
- **Total Time Complexity:** **O(V²) + O(V + E) ≈ O(V²)** (Since a dense graph has `E ≈ V²`)

### **Space Complexity Analysis**
- **Adjacency List Storage:** **O(V + E)**
- **Visited Array:** **O(V)**
- **Recursive DFS Stack (Worst Case):** **O(V)**
- **Total Space Complexity:** **O(V + E)**

---

### **Edge Cases Considered**
- A graph where all nodes are connected (only 1 province).
- A graph where each node is isolated (`V` provinces).
- A large dense graph (`V ≈ 1000`).
- A sparse graph with minimal edges.

### **Summary**
- DFS is used to count the number of connected components.
- Time complexity is **O(V²)** due to matrix conversion.
- Space complexity is **O(V + E)** for adjacency list and recursion stack.
- Efficient for moderate-sized graphs but may struggle with very large dense graphs.

Would you like additional optimizations or a BFS approach for this problem? 🚀

