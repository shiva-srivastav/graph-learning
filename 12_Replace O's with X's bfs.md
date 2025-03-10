# Replace O's with X's
#dsa #graphs #bfs #matrix

## 🔗 Problem Link
[GeeksforGeeks - Replace O's with X's](https://www.geeksforgeeks.org/problems/replace-os-with-xs0052/1)

---

## 💡 Problem Statement
Given a matrix where 'O' denotes water and 'X' denotes land. Replace all O's with X's except the O's that are not surrounded by X's from all four sides.

### Input/Output Format
- **Input**: Matrix with 'O's and 'X's
- **Output**: Matrix with certain 'O's replaced by 'X's
- **Constraint**: 'O's connected to border cannot be replaced

## 🔍 Example
```
Input Matrix:     Output Matrix:
X X X X          X X X X
X O O X    →     X X X X
X X O X          X X X X
X O X X          X O X X
```

## 🎯 Approach
Using BFS starting from border 'O's to mark unsurrounded cells

### Key Data Structures
```java
// Custom Pair class for coordinates
static class Pair {
    int x;
    int y;
    Pair(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

// Queue for BFS
ArrayDeque<Pair> queue
```

### Direction Arrays
```java
rowDir[] = {0, -1, 0, 1}   // Left, Up, Right, Down
colDir[] = {-1, 0, 1, 0}   // Corresponding columns
```

## 📝 Algorithm Steps

### 1. Border Cell Processing
```java
// Process first and last column
for(int i = 0; i < mat.length; i++) {
    // First column
    if(mat[i][0] == 'O' && !visited[i][0]) {
        visited[i][0] = true;
        queue.add(new Pair(i, 0));
    }
    // Last column
    if(mat[i][mat[0].length-1] == 'O' && !visited[i][mat[0].length-1]) {
        visited[i][mat[0].length-1] = true;
        queue.add(new Pair(i, mat[0].length-1));
    }
}

// Process first and last row
for(int i = 0; i < mat[0].length; i++) {
    // First row
    if(mat[0][i] == 'O' && !visited[0][i]) {
        visited[0][i] = true;
        queue.add(new Pair(0, i));
    }
    // Last row
    if(mat[mat.length-1][i] == 'O' && !visited[mat.length-1][i]) {
        visited[mat.length-1][i] = true;
        queue.add(new Pair(mat.length-1, i));
    }
}
```

### 2. BFS Process
```java
while(!queue.isEmpty()) {
    Pair pair = queue.poll();
    
    // Check all 4 directions
    for(int i = 0; i < 4; i++) {
        int newx = x + rowDir[i];
        int newy = y + colDir[i];
        
        // Process valid unvisited O's
        if(isValid(newx, newy) && !visited[newx][newy] && mat[newx][newy] == 'O') {
            queue.add(new Pair(newx, newy));
            visited[newx][newy] = true;
        }
    }
}
```

### 3. Final Matrix Update
```java
for(int i = 0; i < mat.length; i++) {
    for(int j = 0; j < mat[0].length; j++) {
        if(!visited[i][j]) {
            mat[i][j] = 'X';
        }
    }
}
```

## ⚠️ Common Pitfalls
1. Not checking all border cells
2. Forgetting to mark cells as visited
3. Incorrect boundary checking
4. Not handling empty matrix cases
5. Processing 'X' cells unnecessarily

## 🔄 Complexity Analysis
- **Time**: O(N×M) - Visit each cell at most once
- **Space**: O(N×M) - Visited array + Queue

## 🎭 Variations
1. Finding enclosed regions in different shapes
2. Different connectivity rules (8-directional)
3. Multiple character types
4. Counting enclosed regions

## 📌 Key Insights
1. Starting from borders helps identify unsurrounded cells
2. Only need to process 'O' cells
3. Visited cells tracking prevents cycles
4. BFS ensures all connected 'O's are found

## 🤔 Related Problems
1. Number of Islands
2. Flood Fill
3. Surrounded Regions
4. Walls and Gates

## 🎯 Practice Tips
1. Draw out the process on paper first
2. Test with different matrix sizes
3. Handle edge cases (empty matrix, single row/column)
4. Try implementing with DFS for comparison
