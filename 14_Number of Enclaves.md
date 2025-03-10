# Number of Enclaves
#dsa #graphs #bfs #matrix

## 🔗 Problem Link
[GeeksForGeeks - Number of Enclaves](https://www.geeksforgeeks.org/problems/number-of-enclaves/1)

## 💡 Problem Statement
Given a 2D binary matrix where:
- 0 represents sea
- 1 represents land
Find the number of 1s that are not connected to any 1 on the boundary of the matrix.

### Input/Output Format
- **Input**: Binary matrix with 0s and 1s
- **Output**: Count of land cells (1s) that cannot reach the boundary
- **Note**: A land cell can move in 4 directions (up, right, down, left)

## 🔍 Example
```
Input Matrix:     After Processing:    
1 1 1 1          0 0 0 0
1 0 0 1    →     0 0 0 0     Count: 3
1 0 1 1          1 0 1 0
1 0 1 1          1 0 1 0
```

## 🎯 Approach Using BFS
1. Make a deep copy of input grid
2. Start BFS from all boundary 1s
3. Mark all reachable 1s as 0
4. Count remaining 1s

### Data Structures Used
```java
class Pair {
    int x;
    int y;
    
    Pair(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

ArrayDeque<Pair> queue;
int[][] gridCopy;  // For processing without modifying input
```

## 📝 Algorithm Steps

### 1. Deep Copy Creation
```java
int[][] gridCopy = new int[grid.length][grid[0].length];
for(int i = 0; i < grid.length; i++) {
    for(int j = 0; j < grid[0].length; j++) {
        gridCopy[i][j] = grid[i][j];
    }
}
```

### 2. Process Boundary Cells
```java
// First and last column
for(int i = 0; i < grid.length; i++) {
    if(gridCopy[i][0] == 1) {
        gridCopy[i][0] = 0;
        queue.add(new Pair(i, 0));
    }
    if(gridCopy[i][gridCopy[0].length-1] == 1) {
        gridCopy[i][gridCopy[0].length-1] = 0;
        queue.add(new Pair(i, gridCopy[0].length-1));
    }
}

// First and last row
for(int i = 0; i < grid[0].length; i++) {
    if(gridCopy[0][i] == 1) {
        gridCopy[0][i] = 0;
        queue.add(new Pair(0, i));
    }
    if(gridCopy[gridCopy.length-1][i] == 1) {
        gridCopy[gridCopy.length-1][i] = 0;
        queue.add(new Pair(gridCopy.length-1, i));
    }
}
```

### 3. BFS Process
```java
int[] rowDir = {0, -1, 0, 1};  // Left, Up, Right, Down
int[] colDir = {-1, 0, 1, 0};  // Corresponding columns

while(!queue.isEmpty()) {
    Pair pair = queue.poll();
    
    for(int i = 0; i < 4; i++) {
        int newx = pair.x + rowDir[i];
        int newy = pair.y + colDir[i];
        
        if(isValid(newx, newy, gridCopy) && gridCopy[newx][newy] == 1) {
            queue.add(new Pair(newx, newy));
            gridCopy[newx][newy] = 0;  // Mark as visited
        }
    }
}
```

### 4. Count Remaining Land Cells
```java
int count = 0;
for(int i = 0; i < gridCopy.length; i++) {
    for(int j = 0; j < gridCopy[0].length; j++) {
        if(gridCopy[i][j] == 1) count++;
    }
}
return count;
```

## ⚠️ Common Pitfalls
1. Not making a deep copy of input grid
2. Using wrong indices for boundary checks
3. Not handling corner cases (empty grid, single row/column)
4. Using wrong direction arrays
5. Forgetting to mark cells as visited

## 🔄 Complexity Analysis
- **Time**: O(N×M) - Visit each cell at most once
- **Space**: O(N×M) - For queue and gridCopy

## 🎯 Practice Tips
1. Try implementing with DFS
2. Handle different grid shapes
3. Modify to print enclave positions
4. Try without extra space (modifying input grid)
5. Add diagonal movements variation

## 🤔 Related Problems
1. Number of Islands
2. Surrounded Regions
3. Making A Large Island
4. Flood Fill

## 📌 Key Insights
1. BFS from boundary helps identify non-enclaves
2. No need for visited array as we modify grid
3. Deep copy preserves input grid
4. Processing boundaries first is crucial
5. Four-directional movement is sufficient
