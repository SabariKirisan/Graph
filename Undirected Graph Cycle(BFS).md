## Undirected Graph Cycle (c++)

Given an undirected graph with V vertices and E edges, represented as a 2D vector edges[][], where each entry edges[i] = [u, v] denotes an edge between vertices u and v, determine whether the graph contains a cycle or not.

## Example
Input: V = 4, E = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 3]]

Output: true

Explanation: 

![image](https://github.com/user-attachments/assets/73a05aed-308b-4abe-b387-5031c4261db1)

1 -> 2 -> 0 -> 1 is a cycle.

## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    bool detect(int src,vector<int> &vis,vector<vector<int>>&adj)
    {
        vis[src]=1;
        queue<pair<int,int>> q;
        q.push({src,-1});
        while(!q.empty())
        {
            int node=q.front().first;
            int parent=q.front().second;
            q.pop();
            
            for(auto adjnode:adj[node])
            {
                if(!vis[adjnode])
                {
                    vis[adjnode]=1;
                    q.push({adjnode,node});
                }
                else if(parent != adjnode)
                {
                    return true;
                }
            }
        }
        return false;
    }
    
  public:
    bool isCycle(int V, vector<vector<int>>& edges) 
    {
        vector<vector<int>>adj(V);
        for(int i=0;i<edges.size();i++)
        {
            int u=edges[i][0];
            int v=edges[i][1];
            
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
        vector<int> vis(V,0);
        for(int i=0;i<V;i++)
        {
            if(!vis[i])
            {
                if(detect(i,vis,adj)) return true;
            }
        }
        return false;
    }
};
```
## Complexity
- Time complexity : O(N + 2E) + O(N), Where N = Nodes, 2E is for total degrees as we traverse all adjacent nodes. In the case of connected components of a graph, it will take another O(N) time.

- Space complexity : O(N) + O(N) ~ O(N), Space for queue data structure and visited array.
