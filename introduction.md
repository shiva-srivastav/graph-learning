
**Introduction to Graphs**

Graphs are fundamental data structures used in computer science and mathematics to represent relationships between objects. They consist of vertices (or nodes) and edges (or links) that connect them. Graphs are widely used in various domains, including social networks, transportation systems, network topology, and more.

---

**Terminology in Graphs**

1. **Graph (G)**: A graph G is defined as an ordered pair G = (V, E), where V is a set of vertices (nodes), and E is a set of edges (connections between nodes).

   ![Graph Example](https://upload.wikimedia.org/wikipedia/commons/6/64/Graph_Bidirectional.svg)

2. **Vertex (Node, V)**: A fundamental unit of a graph that represents an entity. The number of vertices in a graph is denoted as |V|.

3. **Edge (E)**: A connection between two vertices. It represents a relationship between them. The number of edges in a graph is denoted as |E|.

4. **Degree of a Vertex**: The number of edges incident to a vertex.
   - **In-degree**: Number of incoming edges (for directed graphs).
   - **Out-degree**: Number of outgoing edges (for directed graphs).

5. **Types of Graphs**:
   - **Directed Graph (Digraph)**: A graph in which edges have a direction (represented as ordered pairs).
   - **Undirected Graph**: A graph where edges do not have a direction.
   - **Weighted Graph**: A graph where edges have weights (or costs) associated with them.
   - **Unweighted Graph**: A graph where edges do not have weights.
   - **Connected Graph**: A graph in which there is a path between every pair of vertices.
   - **Disconnected Graph**: A graph that has at least one isolated vertex or separate components.
   - **Cyclic Graph**: A graph that contains at least one cycle.
   - **Acyclic Graph**: A graph that does not contain any cycle.

   ![Graph Types](https://upload.wikimedia.org/wikipedia/commons/a/a2/Directed.svg)

6. **Path**: A sequence of vertices where each adjacent pair is connected by an edge.
   - **Simple Path**: A path that does not repeat vertices.
   - **Cycle**: A path that starts and ends at the same vertex without repeating edges.

7. **Subgraph**: A subset of a graph containing some vertices and edges of the original graph.

8. **Adjacency**:
   - **Adjacency Matrix**: A representation of a graph using a 2D matrix.
   - **Adjacency List**: A list-based representation of a graph where each vertex stores a list of connected vertices.

9. **Tree**: A special type of acyclic graph that is connected and has no cycles.

   ![Tree Example](https://upload.wikimedia.org/wikipedia/commons/f/f7/Binary_tree.svg)

10. **Bipartite Graph**: A graph whose vertices can be divided into two sets such that no two vertices within the same set are adjacent.

11. **Eulerian Path & Eulerian Circuit**:
   - **Eulerian Path**: A path that visits every edge exactly once.
   - **Eulerian Circuit**: A path that visits every edge exactly once and starts and ends at the same vertex.

12. **Hamiltonian Path & Hamiltonian Circuit**:
   - **Hamiltonian Path**: A path that visits every vertex exactly once.
   - **Hamiltonian Circuit**: A path that visits every vertex exactly once and returns to the starting vertex.

13. **Graph Representation**:
   - **Adjacency List**: Stores a list of adjacent vertices for each vertex.
   - **Adjacency Matrix**: A 2D array where an entry (i, j) represents the presence (or weight) of an edge between vertex i and vertex j.
   - **Incidence Matrix**: A matrix representation that shows the relationship between vertices and edges.

14. **Graph Traversal Algorithms**:
   - **Depth First Search (DFS)**: Explores as far as possible along a branch before backtracking.
   - **Breadth First Search (BFS)**: Explores all neighbors at the current depth before moving to the next level.

   ![DFS vs BFS](https://upload.wikimedia.org/wikipedia/commons/4/42/Graph_traversals.gif)

Graphs play a crucial role in various applications, including shortest path algorithms (like Dijkstra's and Bellman-Ford), minimum spanning tree algorithms (like Kruskal's and Prim's), and network flow problems.

