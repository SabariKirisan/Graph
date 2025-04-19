## Directed Graph Cycle (DFS) (c++)

Given a Directed Graph with V vertices (Numbered from 0 to V-1) and E edges, check whether it contains any cycle or not.

The graph is represented as a 2D vector edges[][], where each entry edges[i] = [u, v] denotes an edge from verticex u to v.

## Example
Input: V = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]

![image](https://github.com/user-attachments/assets/0da3b676-49d8-434c-8d16-759a743e2bb5)

Output: true

Explanation: The diagram clearly shows a cycle 0 → 2 → 0
## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    bool dfs(int node,vector<int> &vis,vector<int> &pathvis,vector<vector<int>> &adjList)
    {
        vis[node]=1;
        pathvis[node]=1;
        
        for(auto it: adjList[node])
        {
            if(!vis[it])
            {
                if(dfs(it,vis,pathvis,adjList)== true) return true;
            }
            else if(pathvis[it])
            {
                return true;
            }
        }
        pathvis[node]=0;
        return false;
    }
  public:
    bool isCyclic(int V, vector<vector<int>> &edges) 
    {
        vector<vector<int>> adjList(V);
        for (int i = 0; i < edges.size(); i++) 
        {
            
            int u = edges[i][0];
            int v = edges[i][1];
            adjList[u].push_back(v);
        }
        
        vector<int> vis(V,0);
        vector<int> pathvis(V,0);
        
        for(int i=0;i<V;i++)
        {
            if(vis[i]==0)
            {
                if(dfs(i,vis,pathvis,adjList)== true) return true;
            }
        }
        return false;
    }
};
```
## Complexity
- Time complexity : O(V+E) + O(V)
  
             where V = no. of nodes and E = no. of edges. There can be at most V components. So, another O(V) time complexity.

- Space complexity : O(2N) + O(N) ~ O(2N)

             O(2N) for two visited arrays and O(N) for recursive stack space.
