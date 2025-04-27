## Number of Provinces (c++)

Given an undirected graph with V vertices. We say two vertices u and v belong to a single province if there is a path from u to v or v to u. Your task is to find the number of provinces.

Note: A province is a group of directly or indirectly connected cities and no other cities outside of the group.

## Example
Input:[[1, 0, 1],[0, 1, 0],[1, 0, 1]]

![image](https://github.com/user-attachments/assets/f737033f-5807-42ee-994b-3d25c8a7d467)
 
Output:2

Explanation: The graph clearly has 2 Provinces [1,3] and [2]. As city 1 and city 3 has a path between them they belong to a single province. City 2 has no path to city 1 or city 3 hence it belongs to another province.

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
    int numProvinces(vector<vector<int>> adj, int V) 
    {
        DisjointSet ds(V);
        for(int i=0;i<V;i++)
        {
            for(int j=0;j<V;j++)
            {
                if(adj[i][j]==1)
                {
                    ds.unionBySize(i,j);
                }
            }
        }
        int cnt=0;
        for(int i=0;i<V;i++)
        {
            if(ds.parent[i]==i)
            cnt++;
        }
        return cnt;
    }
};
```
## Complexity
- Time complexity : 
  
         O(V) + O(V^2 × α(V)) + O(V) ~ O(V²)
    
   - parent array of size V+1 → O(V) space, size array of size V+1 → O(V) space = So this initialization takes O(V) time and space.
   - Two nested loops → O(V²) iterations.
   - For each adj[i][j] == 1, you call unionBySize(i, j).
        - Inside unionBySize(), you call two findUPar() functions.
        - Each findUPar() is O(α(V)) time (α(V) is almost constant ≈ 4).
   - Thus, each unionBySize() operation is O(α(V)) ≈ O(1).
   - ⮕ Total union operation time = O(V² × α(V)) ≈ O(V²).
   - A single loop of size V → O(V) time.
     
- Space complexity :

         O(V+V) ~ O(V)
  
   - parent[] array: O(V)
   - size[] array: O(V)
