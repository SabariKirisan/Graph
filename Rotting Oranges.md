## Rotting Oranges (c++)

You are given an m x n grid where each cell can have one of three values:

0 representing an empty cell,

1 representing a fresh orange, or

2 representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.
## Example
![image](https://github.com/user-attachments/assets/82d7289f-289a-4012-946f-e88b8387874e)

Input: grid = [[2,1,1],[1,1,0],[0,1,1]]

Output: 4

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) 
    {
        int n=grid.size();
        int m=grid[0].size();

        queue<pair<pair<int,int>,int>> q;
        vector<vector<int>> vis(n,vector<int>(m,0));
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(grid[i][j]==2)
                {
                    q.push({{i,j},0});
                    vis[i][j]=2;
                }
                else
                {
                    vis[i][j]=0;
                }
            }
        }
        int tm=0;
        int drow[]={-1,0,1,0};
        int dcol[]={0,-1,0,1};
        while(!q.empty())
        {
            int r=q.front().first.first;
            int c=q.front().first.second;
            int t=q.front().second;
            q.pop();

            tm=max(tm,t);

            for(int i=0;i<4;i++)
            {
                int nrow=r+drow[i];
                int ncol=c+dcol[i];

                if(nrow >=0 && nrow<n && ncol >=0 && ncol < m && grid[nrow][ncol]==1 && vis[nrow][ncol]==0)
                {
                    q.push({{nrow,ncol},t+1});
                    vis[nrow][ncol]=2;
                }
            }
        }
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(vis[i][j]!=2 && grid[i][j]==1)
                {
                    return -1;
                }
            }
        }
        return tm;
    }
};
```
## Complexity
- Time complexity : O ( n x m ) x 4    

  Reason: Worst-case - We will be making each fresh orange rotten in the grid and for each rotten orange will check in 4 directions

- Space complexity : O ( n x m )

  Reason: worst-case -  If all oranges are Rotten, we will end up pushing all rotten oranges into the Queue data structure
