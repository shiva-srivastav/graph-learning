## **Depth First Search (DFS) - Complete Theory & Code Example in Java**

### **What is DFS?**
Depth First Search (DFS) is a fundamental graph traversal algorithm used to explore all vertices of a graph. It starts from a given source node and explores as deep as possible along each branch before backtracking.

### **Types of Graph Representation**
DFS can be implemented using:
1. **Adjacency Matrix** (2D array representation)  
2. **Adjacency List** (Array of Lists) – More efficient for sparse graphs.

### **DFS Algorithm Steps**
1. Start from the given node (source).
2. Mark it as visited.
3. Explore its adjacent (neighboring) nodes recursively.
4. Backtrack if there are no unvisited adjacent nodes.

### **DFS Implementation Approaches**
- **Recursive Approach** (Uses function call stack)
- **Iterative Approach** (Uses an explicit stack)

---

## **1. DFS Recursive Implementation (Adjacency List)**
```java
import java.util.*;

class Graph {
    private int V; // Number of vertices
    private List<List<Integer>> adjList;

    public Graph(int V) {
        this.V = V;
        adjList = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
    }

    // Add an edge to the graph
    public void addEdge(int u, int v) {
        adjList.get(u).add(v);
        adjList.get(v).add(u); // For undirected graph
    }

    // DFS recursive function
    private void dfsHelper(int node, boolean[] visited) {
        visited[node] = true;
        System.out.print(node + " ");

        for (int neighbor : adjList.get(node)) {
            if (!visited[neighbor]) {
                dfsHelper(neighbor, visited);
            }
        }
    }

    // DFS traversal
    public void dfs(int startNode) {
        boolean[] visited = new boolean[V];
        System.out.println("DFS Traversal:");
        dfsHelper(startNode, visited);
    }

    public static void main(String[] args) {
        Graph g = new Graph(6);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(1, 4);
        g.addEdge(2, 5);

        g.dfs(0);
    }
}
```
**Output:**
```
DFS Traversal:
0 1 3 4 2 5 
```

---

## **2. DFS Iterative Implementation (Using Stack)**
```java
import java.util.*;

class Graph {
    private int V;
    private List<List<Integer>> adjList;

    public Graph(int V) {
        this.V = V;
        adjList = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }
    }

    public void addEdge(int u, int v) {
        adjList.get(u).add(v);
        adjList.get(v).add(u); // For undirected graph
    }

    public void dfsIterative(int startNode) {
        boolean[] visited = new boolean[V];
        Stack<Integer> stack = new Stack<>();
        stack.push(startNode);

        System.out.println("DFS Traversal:");
        while (!stack.isEmpty()) {
            int node = stack.pop();
            if (!visited[node]) {
                System.out.print(node + " ");
                visited[node] = true;

                // Push neighbors in reverse order for correct DFS order
                List<Integer> neighbors = adjList.get(node);
                Collections.reverse(neighbors);
                for (int neighbor : neighbors) {
                    if (!visited[neighbor]) {
                        stack.push(neighbor);
                    }
                }
            }
        }
    }

    public static void main(String[] args) {
        Graph g = new Graph(6);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(1, 4);
        g.addEdge(2, 5);

        g.dfsIterative(0);
    }
}
```
**Output:**
```
DFS Traversal:
0 2 5 1 4 3 
```

---

## **Applications of DFS**
- **Finding Connected Components**
- **Detecting Cycles in a Graph**
- **Topological Sorting (DAG)**
- **Path Finding (Maze solving, Navigation)**
- **Solving Puzzles (Sudoku, N-Queens)**

---

## **DFS Problems on LeetCode & GeeksforGeeks**
### **LeetCode:**
1. [Number of Islands](https://leetcode.com/problems/number-of-islands/)
2. [Course Schedule](https://leetcode.com/problems/course-schedule/)
3. [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/)

### **GeeksforGeeks:**
1. [Depth First Search (DFS) for a Graph](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)
2. [Connected Components in an Undirected Graph](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)
3. [Detect Cycle in a Directed Graph](https://www.geeksforgeeks.org/detect-cycle-in-a-directed-graph-using-dfs/)

Let me know if you need further explanations! 🚀
