## Number Of Islands (c++)

You are given a n,m which means the row and column of the 2D matrix and an array of  size k denoting the number of operations. Matrix elements is 0 if there is water or 1 if there is land. Originally, the 2D matrix is all 0 which means there is no land in the matrix. The array has k operator(s) and each operator has two integer A[i][0], A[i][1] means that you can change the cell matrix[A[i][0]][A[i][1]] from sea to island. Return how many island are there in the matrix after each operation.You need to return an array of size k.

Note : An island means group of 1s such that they share a common side.

## Example
Input Format: n = 4 m = 5 k = 4 A = {{1,1},{0,1},{3,3},{3,4}} 

Output: 1 1 2 2 

Explanation: The following illustration is the representation of the operation:

![image](https://github.com/user-attachments/assets/8c26a6c7-ff8f-48e7-a814-10d8c5103f47)

## PROGRAM:(Main.cpp)
```
class DisjointSet 
{
public:
    vector<int> parent, size;
    DisjointSet(int n) 
    {
        parent.resize(n + 1);
        size.resize(n + 1,0);
        for (int i = 0; i <= n; i++) 
        {
            parent[i] = i;
        }
    }

    int findUPar(int node) {
        if (node == parent[node])
            return node;
        return parent[node] = findUPar(parent[node]);
    }
    
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        }
        else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
};
class Solution {
  public:
    vector<int> numOfIslands(int n, int m, vector<vector<int>> &operators) 
    {
        DisjointSet ds(n*m);
        int vis[n][m];
        memset(vis,0,sizeof vis);
        int cnt=0;
        vector<int> ans;
        for(auto it:operators)
        {
            int row=it[0];
            int col=it[1];
            if(vis[row][col]==1)
            {
                ans.push_back(cnt);
                continue;
            }
            vis[row][col]=1;
            cnt++;
            
            int drow[]={-1,0,1,0};
            int dcol[]={0,1,0,-1};
            for(int i=0;i<4;i++)
            {
                int nrow=row+drow[i];
                int ncol=col+dcol[i];
                if(nrow >=0 && nrow <n && ncol >=0 && ncol <m)
                {
                    if(vis[nrow][ncol]==1)
                    {
                        int node=row*m+col;
                        int adjnode=nrow*m+ncol;
                        if(ds.findUPar(node) != ds.findUPar(adjnode))
                        {
                            cnt--;
                            ds.unionBySize(node,adjnode);
                        }
                    }
                }
            }
            ans.push_back(cnt);
        }
        return ans;
    }
};
```
## Complexity
- Time complexity : 
  
          O(Q*4α) ~ O(Q)
    
   - where Q = no. of queries. The term 4α is so small that it can be considered constant.
     
- Space complexity :

         O(Q) + O(N*M) + O(N*M)
  
   - where Q = no. of queries
   - N = total no. of rows
   - M = total no. of columns.
     
  The last two terms are for the parent and the size array used inside the Disjoint set data structure. The first term is to store the answer.
