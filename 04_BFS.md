# **Breadth First Search (BFS) - Complete Theory & Code Example in Java**

## **What is BFS?**
Breadth First Search (BFS) is a fundamental graph traversal algorithm used to explore all vertices of a graph level by level. It starts from a given source node and visits all its neighbors before moving to the next level.

## **Types of Graph Representation**
BFS can be implemented using:
1. **Adjacency Matrix** (2D array representation)
2. **Adjacency List** (Array of Lists) – More efficient for sparse graphs.

## **BFS Algorithm Steps**
1. Start from the given node (source).
2. Mark it as visited and add it to the queue.
3. Dequeue a node and explore its adjacent (neighboring) nodes.
4. Add all unvisited adjacent nodes to the queue and mark them as visited.
5. Repeat steps 3-4 until the queue is empty.

## **BFS Implementation Approaches**
- **Iterative Approach** (Uses a Queue)

---

## **1. BFS Iterative Implementation (Adjacency List)**
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

    // BFS traversal
    public void bfs(int startNode) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();
        
        visited[startNode] = true;
        queue.add(startNode);

        System.out.println("BFS Traversal:");
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            
            for (int neighbor : adjList.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
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

        g.bfs(0);
    }
}
```

**Output:**
```
BFS Traversal:
0 1 2 3 4 5
```

---

## **Applications of BFS**
- **Finding Shortest Path (Unweighted Graphs)**
- **Connected Components in a Graph**
- **Network Broadcasting**
- **Solving Puzzles (Rubik’s Cube, Word Ladder, etc.)**
- **Web Crawling Algorithms**

---

## **BFS Problems on LeetCode & GeeksforGeeks**
### **LeetCode:**
1. [Number of Islands](https://leetcode.com/problems/number-of-islands/)
2. [Word Ladder](https://leetcode.com/problems/word-ladder/)
3. [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/)

### **GeeksforGeeks:**
1. [Breadth First Search (BFS) for a Graph](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)
2. [Level Order Traversal of a Tree](https://www.geeksforgeeks.org/level-order-tree-traversal/)
3. [Snake and Ladder Problem](https://www.geeksforgeeks.org/snake-ladder-problem-2/)

Let me know if you need further explanations! 🚀

