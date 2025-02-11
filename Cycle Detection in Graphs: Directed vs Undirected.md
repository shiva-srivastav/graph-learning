# Cycle Detection in Graphs: Directed vs Undirected

## Understanding Graph Cycles

### What is a Cycle?
- **Directed Graph**: A cycle exists when you can start from a vertex and follow directed edges to return to the same vertex while respecting edge directions.
- **Undirected Graph**: A cycle exists when you can start from a vertex and return to it using three or more vertices without reusing any edges.

### Key Differences

1. **Edge Traversal**
   - **Directed**: Must follow arrow direction (one-way)
   - **Undirected**: Can traverse edges in either direction (two-way)

2. **Cycle Definition**
   - **Directed**: Path like 1→2→1 is a cycle
   - **Undirected**: Path like 1--2--1 is NOT a cycle (same edge reuse)

3. **Detection Method**
   - **Directed**: Needs both visited[] and pathVisited[] arrays
   - **Undirected**: Only needs visited[] array and parent tracking

## Directed Graph Cycle Detection

### Algorithm
1. Use DFS traversal
2. Maintain two arrays:
   - visited[]: Track all visited nodes
   - pathVisited[]: Track nodes in current DFS path
3. If we find a node that's already in pathVisited[], we found a cycle

### Code Implementation
```java
class Solution {
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        boolean[] visited = new boolean[V];
        boolean[] pathVisited = new boolean[V];
        
        // Check each vertex as there might be disconnected components
        for(int i = 0; i < V; i++) {
            if(!visited[i]) {
                if(dfs(adj, visited, pathVisited, i)) return true;
            }
        }
        return false;
    }
    
    private boolean dfs(ArrayList<ArrayList<Integer>> adj, boolean[] visited, 
                       boolean[] pathVisited, int curr) {
        // Mark current node as visited and add to path
        visited[curr] = true;
        pathVisited[curr] = true;
        
        // Check all neighbors
        for(int next : adj.get(curr)) {
            if(!visited[next]) {
                // If unvisited neighbor leads to cycle
                if(dfs(adj, visited, pathVisited, next)) return true;
            }
            // If neighbor is in current path, cycle found
            else if(pathVisited[next]) return true;
        }
        
        // Remove from path when backtracking
        pathVisited[curr] = false;
        return false;
    }
}
```

### Examples
```
// Cycle exists
1 → 2 → 3
    ↑   ↓
    5 ← 4

// No cycle
1 → 2 → 3
    ↓   
    4 → 5
```

## Undirected Graph Cycle Detection

### Algorithm
1. Use DFS traversal
2. Maintain:
   - visited[]: Track visited nodes
   - parent: Track previous node to avoid false cycles
3. If we find an already visited node that's not the parent, we found a cycle

### Code Implementation
```java
class Solution {
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj) {
        boolean[] visited = new boolean[V];
        
        // Check each vertex for disconnected components
        for(int i = 0; i < V; i++) {
            if(!visited[i]) {
                if(dfs(adj, visited, i, -1)) return true;
            }
        }
        return false;
    }
    
    private boolean dfs(ArrayList<ArrayList<Integer>> adj, boolean[] visited, 
                       int curr, int parent) {
        // Mark current node as visited
        visited[curr] = true;
        
        // Check all neighbors
        for(int next : adj.get(curr)) {
            if(!visited[next]) {
                // If unvisited neighbor leads to cycle
                if(dfs(adj, visited, next, curr)) return true;
            }
            // If visited neighbor isn't parent, cycle found
            else if(next != parent) return true;
        }
        return false;
    }
}
```

### Examples
```
// Cycle exists
1 -- 2 -- 3
     |     |
     5 --- 4

// No cycle
1 -- 2 -- 3
     |   
     4 -- 5
```

## Common Mistakes to Avoid

1. **Directed Graphs**
   - Forgetting to maintain pathVisited[]
   - Not removing nodes from pathVisited[] during backtracking
   - Confusing visited[] with pathVisited[]

2. **Undirected Graphs**
   - Not tracking parent node
   - Counting same edge traversal as cycle
   - Over-complicating with unnecessary pathVisited[]

## Time and Space Complexity

### For Both Implementations
- **Time Complexity**: O(V + E)
  - V = number of vertices
  - E = number of edges
  - We visit each vertex and edge once

- **Space Complexity**: 
  - Directed: O(V) for visited[] and pathVisited[]
  - Undirected: O(V) for visited[]
  - Additional O(V) stack space for recursion

## Learning Resources

### Practice Problems
1. [Detect cycle in a directed graph (GFG)](https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1)
2. [Detect cycle in an undirected graph (GFG)](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

### Additional Learning Materials
1. [Introduction to DFS in Graphs](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)
2. [Strongly Connected Components (Kosaraju's Algorithm)](https://www.geeksforgeeks.org/strongly-connected-components/)
3. [Topological Sort](https://www.geeksforgeeks.org/topological-sorting/) - Important concept related to DAGs (Directed Acyclic Graphs)
4. [Detect Cycle in Directed Graph using Colors](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)
5. [DFS vs BFS](https://www.geeksforgeeks.org/difference-between-bfs-and-dfs/)

### Video Tutorials
1. [Striver's Graph Series](https://www.youtube.com/watch?v=uTWZrjuqPkI)
2. [Abdul Bari's Graph Theory](https://www.youtube.com/watch?v=pcKY4hjDrxk)

### LeetCode Similar Problems
1. [Course Schedule (LC-207)](https://leetcode.com/problems/course-schedule/)
2. [Course Schedule II (LC-210)](https://leetcode.com/problems/course-schedule-ii/)
3. [Graph Valid Tree (LC-261)](https://leetcode.com/problems/graph-valid-tree/)
4. [Redundant Connection (LC-684)](https://leetcode.com/problems/redundant-connection/)
