# Replace O's with X's - DFS Approach
#dsa #graphs #dfs #matrix

## 🔗 Problem Link
[GeeksforGeeks - Replace O's with X's](https://www.geeksforgeeks.org/problems/replace-os-with-xs0052/1)

## 💡 Problem Understanding (DFS Perspective)
- We need to identify 'O's that are not surrounded by 'X's
- Key insight: Any 'O' connected to a border 'O' cannot be surrounded
- DFS will help us explore all connected 'O's from the border

## 🎯 DFS Solution

### Core DFS Function
```java
static void dfs(char[][] mat, boolean[][] visited, int row, int col) {
    // 1. Mark current cell as visited
    visited[row][col] = true;
    
    // 2. Direction arrays for 4-directional movement
    int[] rowDir = {-1, 0, 1, 0};  // Up, Right, Down, Left
    int[] colDir = {0, 1, 0, -1};  
    
    // 3. Explore all 4 directions
    for(int i = 0; i < 4; i++) {
        int newRow = row + rowDir[i];
        int newCol = col + colDir[i];
        
        // 4. Check validity and process unvisited 'O's
        if(isValid(newRow, newCol, mat) && 
           !visited[newRow][newCol] && 
           mat[newRow][newCol] == 'O') {
            dfs(mat, visited, newRow, newCol);
        }
    }
}
```

### Main Process Function
```java
static char[][] fill(char mat[][]) {
    if(mat == null || mat.length == 0) return mat;
    
    boolean[][] visited = new boolean[mat.length][mat[0].length];
    
    // 1. Process first and last columns
    for(int i = 0; i < mat.length; i++) {
        // First column
        if(mat[i][0] == 'O' && !visited[i][0]) {
            dfs(mat, visited, i, 0);
        }
        // Last column
        if(mat[i][mat[0].length-1] == 'O' && !visited[i][mat[0].length-1]) {
            dfs(mat, visited, i, mat[0].length-1);
        }
    }
    
    // 2. Process first and last rows
    for(int i = 0; i < mat[0].length; i++) {
        // First row
        if(mat[0][i] == 'O' && !visited[0][i]) {
            dfs(mat, visited, 0, i);
        }
        // Last row
        if(mat[mat.length-1][i] == 'O' && !visited[mat.length-1][i]) {
            dfs(mat, visited, mat.length-1, i);
        }
    }
    
    // 3. Replace unvisited 'O's with 'X's
    for(int i = 0; i < mat.length; i++) {
        for(int j = 0; j < mat[0].length; j++) {
            if(!visited[i][j] && mat[i][j] == 'O') {
                mat[i][j] = 'X';
            }
        }
    }
    
    return mat;
}
```

## 📝 Step-by-Step DFS Process
1. **Border Processing**
   - Start DFS from each 'O' on the matrix borders
   - These 'O's cannot be surrounded by definition

2. **DFS Exploration**
   - For each border 'O', explore connected 'O's in all directions
   - Mark visited cells to avoid cycles
   - Recursively process all valid neighbors

3. **Final Update**
   - Any 'O' not visited during DFS must be surrounded
   - Convert these unvisited 'O's to 'X's

## ⚠️ DFS-Specific Pitfalls
1. Stack overflow for large matrices
2. Not handling base cases in recursion
3. Forgetting to check array bounds before recursive calls
4. Not marking cells as visited before recursive call

## 🔄 Complexity Analysis
- **Time**: O(N×M) 
  - Each cell visited at most once
- **Space**: O(N×M)
  - Visited array: O(N×M)
  - Recursion stack: O(N×M) worst case

## 📌 DFS Implementation Tips
1. Always validate coordinates before recursive calls
2. Mark cells as visited before DFS, not after
3. Use direction arrays for cleaner code
4. Handle base cases first
5. Consider stack size for large inputs

## 🎯 DFS Practice Extensions
1. Implement with different direction patterns
2. Try solving without visited array
3. Add path tracking functionality
4. Count regions during DFS
5. Modify to find largest connected component
