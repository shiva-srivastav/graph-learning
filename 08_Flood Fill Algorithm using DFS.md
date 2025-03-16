# Flood Fill Algorithm using DFS

### **Problem Statement**
Given a **2D grid (image)**, perform a flood fill starting from a given pixel `(sr, sc)` and change all connected pixels of the same initial color to a new color.

#### **LeetCode Question Link**
[Flood Fill - LeetCode](https://leetcode.com/problems/flood-fill/)

#### **GitHub Repository (Example Implementation)**
[GitHub - Flood Fill Algorithm](https://github.com/your-repo/flood-fill-dfs) *(Replace with actual repo if available)*

---

### **Approach**
1. **Create a Copy of the Image:**
   - Before modifying the input image, create a copy to avoid altering the original.
   
2. **Initialize DFS Traversal:**
   - Store the initial color of the starting pixel.
   - Define possible movement directions (Up, Left, Down, Right).
   - Recursively update adjacent pixels with the new color if they match the initial color.

3. **Return the Updated Image Copy:**
   - Once all valid pixels are updated, return the modified image copy.

---

### **Code Implementation (Java)**
```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        int init = image[sr][sc];
        int[][] copyImage = new int[image.length][image[0].length];
        
        for (int i = 0; i < image.length; i++) {
            for (int j = 0; j < image[0].length; j++) {
                copyImage[i][j] = image[i][j];
            }
        }
        
        dfs(image, copyImage, sr, sc, newColor, init);
        
        return copyImage;
    }
    
    public void dfs(int[][] image, int[][] copyImage, int sr, int sc, int newColor, int init) {
        copyImage[sr][sc] = newColor;
        
        int colDir[] = {-1, 0, 1, 0};
        int rowDir[] = {0, -1, 0, 1};
        
        for (int i = 0; i < 4; i++) {
            int sx = sr + rowDir[i];
            int sy = sc + colDir[i];
            
            if (sx >= 0 && sx < image.length && sy >= 0 && sy < image[0].length && copyImage[sx][sy] == init) {
                dfs(image, copyImage, sx, sy, newColor, init);
            }
        }
    }
}
```

---

### **Time Complexity Analysis**
- **DFS Traversal:** **O(N × M)** (Each pixel is visited once in the worst case, where `N` and `M` are image dimensions)
- **Copying the Image:** **O(N × M)**
- **Total Time Complexity:** **O(N × M)**

### **Space Complexity Analysis**
- **Recursive DFS Stack (Worst Case):** **O(N × M)** (For a completely filled region)
- **Copy of the Image:** **O(N × M)**
- **Total Space Complexity:** **O(N × M)**

---

### **Edge Cases Considered**
- The starting pixel is already the `newColor`.
- The entire image is a single color.
- A large sparse image with minimal connected pixels.
- A fully connected grid where all pixels change.

### **Summary**
- DFS is used to recursively traverse and update connected pixels.
- The approach ensures the original image is preserved by modifying a copy.
- The time complexity is **O(N × M)**.
- The space complexity is **O(N × M)** due to recursion and image storage.

Would you like a BFS approach or further optimizations? 🚀

