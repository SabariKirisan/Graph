## Number of Islands (c++)

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

## Example
Input: grid = 

[  ["1","1","1","1","0"],

  ["1","1","0","1","0"],
  
  ["1","1","0","0","0"],
  
  ["0","0","0","0","0"] ]

Output: 1
## PROGRAM:(Main.cpp)
```
class Solution 
{
private:
void bfs(int row,int col,vector<vector<char>> &grid,vector<vector<int>> &vis)
{
    vis[row][col]=1;
    queue<pair<int,int>>q;
    q.push({row,col});
    int n=grid.size();
    int m=grid[0].size();

    int drow[] = {-1, 0, 1, 0};
    int dcol[] = {0, 1, 0, -1};
    
    while(!q.empty())
    {
        row=q.front().first;
        col=q.front().second;
        q.pop();

        for(int i=0;i<4;i++)
        {
            int nrow=row+drow[i];
            int ncol=col+dcol[i];
            if(nrow >=0 && nrow < n && ncol >=0 && ncol < m && !vis[nrow][ncol] && grid[nrow][ncol]=='1')
            {
                vis[nrow][ncol]=1;
                q.push({nrow,ncol});
            }
        }
    }
}
public:
    int numIslands(vector<vector<char>>& grid) 
    {
        int n=grid.size();
        int m=grid[0].size();

        vector<vector<int>> vis(n,vector<int>(m,0));
        int cnt=0;
        for(int row=0; row<n; row++)
        {
            for(int col=0; col<m; col++)
            {
                if(!vis[row][col] && grid[row][col]=='1')
                {
                    cnt++;
                    bfs(row,col,grid,vis);
                }
            }
        }  
        return cnt;  
    }
};
```
## Complexity
- Time complexity : O(N × M)

- Space complexity : O(N × M)
