## Distance of Nearest Cell having 1 (or) Map of Highest Peak (BFS) (c++)

You are given an integer matrix isWater of size m x n that represents a map of land and water cells.

- If isWater[i][j] == 0, cell (i, j) is a land cell. 

- If isWater[i][j] == 1, cell (i, j) is a water cell.  

You must assign each cell a height in a way that follows these rules:

- The height of each cell must be non-negative.

- If the cell is a water cell, its height must be 0.

- Any two adjacent cells must have an absolute height difference of at most 1. A cell is adjacent to another cell if the former is directly north, east, south, or west of the latter (i.e., their sides are touching).

Find an assignment of heights such that the maximum height in the matrix is maximized.

Return an integer matrix height of size m x n where height[i][j] is cell (i, j)'s height. If there are multiple solutions, return any of them.

## Example
![image](https://github.com/user-attachments/assets/cb3359de-2341-4e2a-ba6d-f4b929cb4c9b)

Input: isWater = [[0,0,1],[1,0,0],[0,0,0]]

Output: [[1,1,0],[0,1,1],[1,2,2]]

Explanation: A height of 2 is the maximum possible height of any assignment.
Any height assignment that has a maximum height of 2 while still meeting the rules will also be accepted.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& isWater) 
    {
        int n=isWater.size();
        int m=isWater[0].size();
        vector<vector<int>>vis(n,vector<int>(m,0));
        vector<vector<int>>dis(n,vector<int>(m,0));
        queue<pair<pair<int,int>,int>> q;

        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(isWater[i][j]==1)
                {
                    vis[i][j]=1;
                    q.push({{i,j},0});
                }
                else
                {
                    vis[i][j]=0;
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
