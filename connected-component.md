**Connected Components in Graphs**

### **Definition**
A **connected component** in an undirected graph is a subset of the graph where any two vertices are connected either directly or indirectly, and no additional vertices outside this subset are connected to it.

---

## **Types of Graphs Based on Connectivity**

### **1. Connected Graph**
A graph is called **connected** if there exists a path between every pair of vertices.

#### **Example:**
```
  (A) -- (B) -- (C)
   |      |
  (D) -- (E)
```
In the above graph, all nodes are connected directly or indirectly.

### **2. Disconnected Graph**
A graph is called **disconnected** if at least one vertex is not reachable from another vertex.

#### **Example:**
```
  (A) -- (B)        (C) -- (D)
```
Here, there are two separate components (A, B) and (C, D), meaning the graph is disconnected.

### **3. Strongly Connected Graph (For Directed Graphs)**
A directed graph is **strongly connected** if there is a path from every vertex to every other vertex.

### **4. Weakly Connected Graph (For Directed Graphs)**
A directed graph is **weakly connected** if replacing all its directed edges with undirected edges results in a connected graph.

---

## **Identifying Connected Components**
### **Algorithm Approach**
To find connected components in an **undirected graph**, we can use:

1. **Depth First Search (DFS)**
2. **Breadth First Search (BFS)**

### **DFS Approach for Finding Connected Components**
```cpp
#include <iostream>
#include <vector>
using namespace std;

void DFS(int node, vector<int> adj[], vector<bool> &visited) {
    visited[node] = true;
    for (auto neighbor : adj[node]) {
        if (!visited[neighbor]) {
            DFS(neighbor, adj, visited);
        }
    }
}

int countConnectedComponents(int V, vector<int> adj[]) {
    vector<bool> visited(V, false);
    int count = 0;
    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            DFS(i, adj, visited);
            count++;
        }
    }
    return count;
}

int main() {
    int V = 5;
    vector<int> adj[V];
    adj[0] = {1, 2};
    adj[1] = {0, 2};
    adj[2] = {0, 1};
    adj[3] = {4};
    adj[4] = {3};
    
    cout << "Number of connected components: " << countConnectedComponents(V, adj);
    return 0;
}
```

### **BFS Approach for Finding Connected Components**
```java
import java.util.*;

public class ConnectedComponents {
    static void BFS(int node, Map<Integer, List<Integer>> adj, boolean[] visited) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(node);
        visited[node] = true;
        
        while (!queue.isEmpty()) {
            int current = queue.poll();
            for (int neighbor : adj.getOrDefault(current, new ArrayList<>())) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static int countConnectedComponents(int V, Map<Integer, List<Integer>> adj) {
        boolean[] visited = new boolean[V];
        int count = 0;
        
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                BFS(i, adj, visited);
                count++;
            }
        }
        return count;
    }
    
    public static void main(String[] args) {
        Map<Integer, List<Integer>> adj = new HashMap<>();
        adj.put(0, Arrays.asList(1, 2));
        adj.put(1, Arrays.asList(0, 2));
        adj.put(2, Arrays.asList(0, 1));
        adj.put(3, Arrays.asList(4));
        adj.put(4, Arrays.asList(3));
        
        System.out.println("Number of connected components: " + countConnectedComponents(5, adj));
    }
}
```

---

## **Key Takeaways**
- **Connected Graph**: A graph where all nodes are reachable from any other node.
- **Disconnected Graph**: A graph with at least one isolated component.
- **Strongly Connected Graph**: A directed graph where every node has a path to every other node.
- **Weakly Connected Graph**: A directed graph that becomes connected when edges are considered undirected.
- DFS and BFS can be used to count the number of connected components.

By mastering these concepts and algorithms, you can efficiently analyze the connectivity of graphs and solve related problems in competitive programming and real-world applications.
