## Number of Operations to Make Network Connected (c++)

There are n computers numbered from 0 to n - 1 connected by ethernet cables connections forming a network where connections[i] = [ai, bi] represents a connection between computers ai and bi. Any computer can reach any other computer directly or indirectly through the network.

You are given an initial computer network connections. You can extract certain cables between two directly connected computers, and place them between any pair of disconnected computers to make them directly connected.

Return the minimum number of times you need to do this in order to make all the computers connected. If it is not possible, return -1.

## Example
![image](https://github.com/user-attachments/assets/3a2ad6ef-5986-40e0-b6ec-a88975ea5416)

Input: n = 4, connections = [[0,1],[0,2],[1,2]]

Output: 1

Explanation: Remove cable between computer 1 and 2 and place between computers 1 and 3.
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
    int makeConnected(int n, vector<vector<int>>& connections) 
    {
        DisjointSet ds(n);
        int cnt_extra=0;
        for(auto it: connections)
        {
            int u=it[0];
            int v=it[1];
            if(ds.findUPar(u)==ds.findUPar(v))
            {
                cnt_extra++;
            }
            else
            {
                ds.unionBySize(u,v);
            }
        } 
        int cnt_comp=0;
        for(int i=0;i<n;i++)
        {
            if(ds.parent[i]==i) cnt_comp++;
        }
        int ans=cnt_comp-1;
        for(int i=0;i<n;i++)
        {
            if(cnt_extra>=ans) return ans;
        }
        return -1;
    }
};
```
## Complexity
- Time complexity : 
  
         O(n) + O(E) + O(n) ~ O(E + n)
    
   - parent array of size n+1 → O(n) space, size array of size n+1 → O(n) space = So this initialization takes O(n) time and space.
   - For each connection:
        - 2 findUPar() calls → O(α(n)) each
        - Possibly 1 unionBySize() → O(α(n))
   - Since α(n) is almost constant (~4),
   - Each iteration takes O(α(n)) ≈ O(1)
   - Thus total for all edges = O(E × α(n)) ≈ O(E)
   - Counting Components : Simple loop over all n nodes → O(n) time.
     
- Space complexity :

         O(n+n) ~ O(n)
  
   - parent[] array: O(n)
   - size[] array: O(n)
