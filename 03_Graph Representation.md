**Graph Representation**

Graphs can be represented in multiple ways depending on the requirement. The most commonly used representations are:

---

## **1. Adjacency Matrix Representation**

An **Adjacency Matrix** is a 2D array where rows and columns represent vertices, and the value at a specific cell indicates whether an edge exists between the vertices.

### **Characteristics:**
- Space Complexity: **O(V²)** (V = Number of vertices)
- Efficient for dense graphs but consumes more space for sparse graphs.
- Checking if an edge exists is **O(1)** time complexity.

### **Adjacency Matrix for an Undirected Graph:**

#### **Graph Example:**
```
  (0) --- (1)
   | \    |
   |  \   |
  (2) -- (3)
```
#### **Matrix Representation:**
```
   0  1  2  3
0 [0, 1, 1, 1]
1 [1, 0, 0, 1]
2 [1, 0, 0, 1]
3 [1, 1, 1, 0]
```

### **Adjacency Matrix for a Directed Graph:**
```
   0  1  2  3
0 [0, 1, 1, 0]
1 [0, 0, 0, 1]
2 [0, 0, 0, 1]
3 [0, 0, 0, 0]
```

---

## **2. Adjacency List Representation**

An **Adjacency List** is a more space-efficient representation that uses an array of lists. Each index represents a vertex, and the list at that index stores the neighboring vertices.

### **Characteristics:**
- Space Complexity: **O(V + E)** (V = vertices, E = edges)
- Efficient for sparse graphs.
- Checking an edge exists takes **O(V)** in the worst case.

### **Adjacency List for an Undirected Graph:**
```
0 → 1 → 2 → 3
1 → 0 → 3
2 → 0 → 3
3 → 0 → 1 → 2
```

### **Adjacency List for a Directed Graph:**
```
0 → 1 → 2
1 → 3
2 → 3
3 → ∅
```

---

## **3. Weighted Graph Representation**

Graphs can have weighted edges representing cost, distance, or capacity. They can be represented in:

### **Adjacency Matrix for a Weighted Graph:**
```
   0   1   2   3
0 [0, 10, 20,  0]
1 [10, 0,  0,  5]
2 [20, 0,  0, 15]
3 [0,  5, 15,  0]
```

### **Adjacency List for a Weighted Graph (Using Pairs)**
```
0 → (1, 10) → (2, 20)
1 → (0, 10) → (3, 5)
2 → (0, 20) → (3, 15)
3 → (1, 5) → (2, 15)
```

---

## **Graph Representation in Code (C++ & Java)**

### **Adjacency List in C++ (Using Vector of Pairs)**
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int V = 4;
    vector<pair<int, int>> adj[V];

    adj[0].push_back({1, 10});
    adj[0].push_back({2, 20});
    adj[1].push_back({0, 10});
    adj[1].push_back({3, 5});
    adj[2].push_back({0, 20});
    adj[2].push_back({3, 15});
    adj[3].push_back({1, 5});
    adj[3].push_back({2, 15});
}
```

### **Adjacency List in Java (Using HashMap and ArrayList)**
```java
import java.util.*;

class Graph {
    private int V;
    private HashMap<Integer, ArrayList<Pair>> adj;

    static class Pair {
        int vertex, weight;
        Pair(int v, int w) { vertex = v; weight = w; }
    }

    Graph(int V) {
        this.V = V;
        adj = new HashMap<>();
        for (int i = 0; i < V; i++)
            adj.put(i, new ArrayList<>());
    }

    void addEdge(int u, int v, int weight) {
        adj.get(u).add(new Pair(v, weight));
        adj.get(v).add(new Pair(u, weight));
    }
}
```

---

### **Comparison of Graph Representations**
| Representation  | Space Complexity | Edge Lookup Time | Best for |
|---------------|----------------|----------------|----------|
| Adjacency Matrix | O(V²) | O(1) | Dense Graphs |
| Adjacency List  | O(V+E) | O(V) | Sparse Graphs |

By understanding these representations, one can choose the optimal one based on the graph's characteristics and the problem's constraints.

