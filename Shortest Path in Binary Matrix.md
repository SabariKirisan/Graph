## Shortest Path in Binary Matrix (c++)

Given an n x n binary matrix grid, return the length of the shortest clear path in the matrix. If there is no clear path, return -1.

A clear path in a binary matrix is a path from the top-left cell (i.e., (0, 0)) to the bottom-right cell (i.e., (n - 1, n - 1)) such that:

  - All the visited cells of the path are 0.
  - All the adjacent cells of the path are 8-directionally connected (i.e., they are different and they share an edge or a corner).

The length of a clear path is the number of visited cells of this path.

## Example
![image](https://github.com/user-attachments/assets/cad72ca6-5fdf-4e5b-aef6-676ecc111747)

Input: grid = [[0,0,0],[1,1,0],[1,1,0]]

Output: 4

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) 
    {
        int n = grid.size();
        if(grid[0][0]==0 && n==1) return 1; 
        if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1) return -1;

        queue<pair<int,int>> q;
        vector<vector<int>> dist(n,vector<int>(n,1e9));
        dist[0][0]=1;
        q.push({0,0});
        while(!q.empty())
        {
            auto it=q.front();
            q.pop();
            int row=it.first;
            int col=it.second;

            for(int i=-1;i<=1;i++)
            {
                for(int j=-1;j<=1;j++)
                {
                    int nrow=row+ i;
                    int ncol=col+ j;

                    if(nrow >=0 && nrow < n && ncol >=0 && ncol < n && grid[nrow][ncol]==0 && dist[row][col] + 1 < dist[nrow][ncol])
                    {
                        dist[nrow][ncol]= 1+dist[row][col];
                        if(nrow==n-1 && ncol==n-1) return dist[nrow][ncol];
                        q.push({nrow,ncol});
                    }
                }
            }
        }
        return -1;
    }
};
```
## Complexity
- Time complexity : 
  
         O( 8*N*N )

   -  { N*N are the total cells, for each of which we also check 8 adjacent nodes for the shortest path length}, Where N = No. of rows of the binary maze

- Space complexity :

         O( N*N )

    - Where N = No. of rows of the binary maze 
