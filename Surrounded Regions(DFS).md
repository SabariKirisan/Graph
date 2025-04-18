## Surrounded Regions (DFS) (c++)

You are given an m x n matrix board containing letters 'X' and 'O', capture regions that are surrounded:

- Connect: A cell is connected to adjacent cells horizontally or vertically.

- Region: To form a region connect every 'O' cell.

- Surround: The region is surrounded with 'X' cells if you can connect the region with 'X' cells and none of the region cells are on the edge of the board.

To capture a surrounded region, replace all 'O's with 'X's in-place within the original board. You do not need to return anything.
## Example
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]

Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]

Explanation:

![image](https://github.com/user-attachments/assets/f397326a-0e7b-49f3-8b9b-b0720c375a3c)

In the above diagram, the bottom region is not captured because it is on the edge of the board and cannot be surrounded.

## PROGRAM:(Main.cpp)
```
class Solution {
private:
    void dfs(int row,int col,vector<vector<int>> &vis,vector<vector<char>>& board)
    {
        int n=board.size();
        int m=board[0].size();
        vis[row][col]=1;
        int drow[]={-1,0,1,0};
        int dcol[]={0,-1,0,1};
        for(int i=0;i<4;i++)
        {
            int nrow=row+drow[i];
            int ncol=col+dcol[i];

            if(nrow >=0 && nrow<n && ncol >=0 && ncol<m && !vis[nrow][ncol] && board[nrow][ncol]=='O')
            {
                dfs(nrow,ncol,vis,board);
            }
        }
    }
public:
    void solve(vector<vector<char>>& board) 
    {
        int n=board.size();
        int m=board[0].size();
        vector<vector<int>> vis(n,vector<int>(m,0));

        for(int i=0;i<n;i++)
        {
            if(!vis[i][0] && board[i][0]=='O')
            {
                dfs(i,0,vis,board);
            }
            if(!vis[i][m-1] && board[i][m-1]=='O')
            {
                dfs(i,m-1,vis,board);
            }
        }
        for(int j=0;j<m;j++)
        {
            if(!vis[0][j] && board[0][j]=='O')
            {
                dfs(0,j,vis,board);
            }
            if(!vis[n-1][j] && board[n-1][j]=='O')
            {
                dfs(n-1,j,vis,board);
            }
        }
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(!vis[i][j] &&  board[i][j]=='O')
                {
                    board[i][j]='X';
                }
            }
        }   
    }
};
```
## Complexity
- Time complexity : O(N) + O(M) + O(NxMx4) ~ O(N x M)
  
      For the worst case, every element will be marked as ‘O’ in the matrix, and the DFS function will be called for (N x M) nodes and for every node, we are traversing for 4 neighbors, so it will take O(N x M x 4) time. Also, we are running loops for boundary elements so it will take O(N) + O(M).
- Space complexity : O(N x M) + O(N x M) ~ O(N x M)

      for the visited array, and auxiliary stack space takes up N x M locations at max.
