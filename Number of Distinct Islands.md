## Number of Distinct Islands (DFS) (c++)

Given a boolean 2D matrix grid of size n * m. You have to find the number of distinct islands where a group of connected 1s (horizontally or vertically) forms an island. Two islands are considered to be distinct if and only if one island is not equal to another (not rotated or reflected).

## Example
Input: 

![image](https://github.com/user-attachments/assets/fbc429ea-fb71-4c4a-a134-40088270289d)

Output: 3

Explanation:

![image](https://github.com/user-attachments/assets/14ed6553-853f-45f7-bebe-ee0febfa722d)

There are 3 islands as the different components are surrounded by water (i.e. 0), and there is no land connectivity in either of the 8 directions hence separating them into 3 islands.

## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    void dfs(int row,int col,vector<vector<int>>& grid,vector<vector<int>> &vis,vector<pair<int,int>> &vec,int base_r,int base_c)
    {
        vis[row][col]=1;
        vec.push_back({row-base_r,col-base_c});
        int n=grid.size();
        int m=grid[0].size();
        
        int drow[]={-1,0,1,0};
        int dcol[]={0,-1,0,1};
        
        for(int i=0;i<4;i++)
        {
            int nrow=row+drow[i];
            int ncol=col+dcol[i];
            if(nrow>=0 && nrow<n && ncol>=0 && ncol<m && vis[nrow][ncol]==0 &&grid[nrow][ncol]==1)
            {
                dfs(nrow,ncol,grid,vis,vec,base_r,base_c);
            }
        }
    }
  public:
    int countDistinctIslands(vector<vector<int>>& grid) 
    {
        int n=grid.size();
        int m=grid[0].size();
        set<vector<pair<int,int>>> st;
        vector<vector<int>> vis(n,vector<int>(m,0));
    
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(!vis[i][j] && grid[i][j]==1)
                {
                    vector<pair<int,int>> vec;
                    dfs(i,j,grid,vis,vec,i,j);
                    st.insert(vec);
                }
            }
        }
        return st.size();
    }
};
```
## Complexity
- Time complexity : O(NxM + NxMx4)
  
            O(N x M) for the nested loops, and O(NxMx4) for the overall DFS of the matrix, that will happen throughout if all the cells are filled with 1.

- Space complexity : O(N x M) + O(N x M) ~ O(N x M)

            O(N x M) for visited array max queue space O(N x M), If all are marked as 1 then the maximum queue space will be O(N x M). 
