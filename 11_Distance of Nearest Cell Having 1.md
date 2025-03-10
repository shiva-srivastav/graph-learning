# Distance of Nearest Cell Having 1
#dsa #graphs #bfs

## 💡 Problem Statement
Given a binary matrix (grid with 0s and 1s), find the distance of the nearest 1 for each cell.

## 🔗 Problem Link
[GeeksforGeeks - Distance of nearest cell having 1](https://www.geeksforgeeks.org/problems/distance-of-nearest-cell-having-1-1587115620/1)

### Input/Output Format
- **Input**: Binary matrix with 0s and 1s
- **Output**: Matrix with distances to nearest 1 for each cell
- **Distance Formula**: Manhattan distance |x1-x2| + |y1-y2|

## 🔍 Example
```
Input Grid:     Output Grid:
0 1 0          1 0 1
0 0 0    →     2 1 1
1 0 1          0 1 0
```

## 🎯 Approach
Using BFS (Breadth-First Search) starting from all 1s simultaneously

### Key Data Structures
```java
// Custom Pair class for coordinates and distances
class Pair<T,U> {
    T x;
    U y;
    Pair(T x, U y) {
        this.x = x;
        this.y = y;
    }
}

// Queue for BFS
ArrayDeque<Pair<Pair<Integer,Integer>,Integer>> queue
```

### Direction Arrays
```java
rowDir[] = {0, -1, 0, 1}   // Left, Up, Right, Down
colDir[] = {-1, 0, 1, 0}   // Corresponding columns
```

## 📝 Algorithm Steps

### 1. Initialization
- Create visited[][] and result[][] arrays
- Find all cells with value 1
- Add them to queue (distance = 0)
- Mark as visited

```java
for(int i = 0; i < grid.length; i++) {
    for(int j = 0; j < grid[0].length; j++) {
        if(grid[i][j] == 1) {
            visited[i][j] = true;
            queue.add(new Pair<>(new Pair<>(i,j), 0));
            gridCopy[i][j] = 0;
        }
    }
}
```

### 2. BFS Process
```java
while(!queue.isEmpty()) {
    // Get current cell and distance
    Pair<Pair<Integer,Integer>,Integer> pair = queue.poll();
    int x = pair.x.x;
    int y = pair.x.y;
    int dist = pair.y;
    
    // Check all 4 directions
    for(int i = 0; i < 4; i++) {
        int xnew = x + rowDir[i];
        int ynew = y + colDir[i];
        
        // Process valid unvisited neighbors
        if(isValid(xnew, ynew) && !visited[xnew][ynew]) {
            // Add to queue with new distance
            queue.add(...);
            visited[xnew][ynew] = true;
            gridCopy[xnew][ynew] = newDistance;
        }
    }
}
```

## ⚠️ Common Pitfalls
1. Forgetting to mark cells as visited when adding to queue
2. Incorrect distance calculation
3. Not checking array bounds
4. Not initializing the result array properly

## 🔄 Complexity Analysis
- **Time**: O(N×M) - Visit each cell once
- **Space**: O(N×M) - Visited array + Queue

## 🎭 Variations
1. Using different distance formulas
2. Finding distance to nearest 0 instead of 1
3. Adding diagonal movements
4. Adding barriers/walls in the grid

## 📌 Key Insights
1. BFS ensures minimum distance
2. Starting from all 1s simultaneously is more efficient
3. Direction arrays make neighbor checking cleaner
4. Manhattan distance is optimal for this grid structure

## 🤔 Related Problems
1. Rotting Oranges
2. Walls and Gates
3. Matrix 01
4. Flood Fill

## 🎯 Practice Tips
1. Try implementing with DFS first to understand why BFS is better
2. Practice with different grid sizes
3. Add print statements to visualize the BFS process
4. Try implementing without using a Pair class
