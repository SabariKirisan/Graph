## Flood Fill (c++)

You are given an image represented by an m x n grid of integers image, where image[i][j] represents the pixel value of the image. You are also given three integers sr, sc, and color. Your task is to perform a flood fill on the image starting from the pixel image[sr][sc].

To perform a flood fill:

Begin with the starting pixel and change its color to color.

Perform the same process for each pixel that is directly adjacent (pixels that share a side with the original pixel, either horizontally or vertically) and shares the same color as the starting pixel.

Keep repeating this process by checking neighboring pixels of the updated pixels and modifying their color if it matches the original color of the starting pixel.

The process stops when there are no more adjacent pixels of the original color to update.

Return the modified image after performing the flood fill.
## Example
Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, color = 2

Output: [[2,2,2],[2,2,0],[2,0,1]]

Explanation:

![image](https://github.com/user-attachments/assets/cbcae6e2-3908-45ff-9a7a-96b53d4137ed)

From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.

Note the bottom corner is not colored 2, because it is not horizontally or vertically connected to the starting pixel.

## PROGRAM:(Main.cpp)
```
class Solution {
private:
void dfs(vector<vector<int>>& image,vector<vector<int>>& ans,int initial_color,int sr,int sc,int color)
{
    ans[sr][sc]=color;
    int drow[]={-1,0,1,0};
    int dcol[]={0,-1,0,1};
    int n=image.size();
    int m=image[0].size();
    for(int i=0;i<4;i++)
    {
        int nrow=sr-drow[i];
        int ncol=sc-dcol[i];
        if(nrow >=0 && nrow < n && ncol >=0 && ncol < m && image[nrow][ncol] == initial_color && ans[nrow][ncol] != color)
        {
            dfs(image,ans,initial_color,nrow,ncol,color);
        }
    }

}
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) 
    {
        int initial_color=image[sr][sc];
        vector<vector<int>>ans =image;
        dfs(image,ans,initial_color,sr,sc,color);
        return ans;    
    }
};
```
## Complexity
- Time complexity : O(N x M + N x M x 4) ~ O(N x M) For the worst case, all of the pixels will have the same colour, so DFS function will be called for (N x M) nodes and for every node we are traversing for 4 neighbours, so it will take O(N x M x 4) time.

- Space complexity : O(N x M) + O(N x M)

O(N x M) for copied input array and recursive stack space takes up O(N x M) locations at max. 
