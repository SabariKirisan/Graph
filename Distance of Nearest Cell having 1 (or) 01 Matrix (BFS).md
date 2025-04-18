## Distance of Nearest Cell having 1 (or) 01 Matrix (BFS) (c++)

Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.

The distance between two cells sharing a common edge is 1.

## Example
![image](https://github.com/user-attachments/assets/7f6371a2-2554-4b87-b1a3-1e7f6e4248a7)

Input: mat = [[0,0,0],[0,1,0],[0,0,0]]

Output: [[0,0,0],[0,1,0],[0,0,0]]

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) 
    {
        int n=mat.size();
        int m=mat[0].size();
        vector<vector<int>>vis(n,vector<int>(m,0));
        vector<vector<int>>dis(n,vector<int>(m,0));
        queue<pair<pair<int,int>,int>> q;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(mat[i][j]==0)
                {
                    vis[i][j]=1;
                    q.push({{i,j},0});
                }
            }
        }
        int drow[]={-1,0,1,0};
        int dcol[]={0,-1,0,1};
        while(!q.empty())
        {
            int row=q.front().first.first;
            int col=q.front().first.second;
            int steps=q.front().second;
            q.pop();
            dis[row][col]=steps;

            for(int i=0;i<4;i++)
            {
                int nrow=row+drow[i];
                int ncol=col+dcol[i];

                if(nrow >=0 && nrow<n && ncol >=0 && ncol<m && vis[nrow][ncol]==0)
                {
                    vis[nrow][ncol]=1;
                    q.push({{nrow,ncol},steps+1});
                }
            }
        }
        return dis;
    }
};
```
## Complexity
- Time complexity : O(NxM + NxMx4) ~ O(N x M)
  
                    For the worst case, the BFS function will be called for (N x M) nodes, and for every node, we are traversing for 4 neighbors, so it will take O(N x M x 4) time.

- Space complexity : O(N x M) + O(N x M) + O(N x M) ~ O(N x M)

             O(N x M) for the visited array, distance matrix, and queue space takes up N x M locations at max. 
