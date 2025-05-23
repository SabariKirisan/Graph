## Is Graph Bipartite? (DFS) (c++)

There is an undirected graph with n nodes, where each node is numbered between 0 and n - 1. You are given a 2D array graph, where graph[u] is an array of nodes that node u is adjacent to. More formally, for each v in graph[u], there is an undirected edge between node u and node v. The graph has the following properties:

- There are no self-edges (graph[u] does not contain u).
- There are no parallel edges (graph[u] does not contain duplicate values).
- If v is in graph[u], then u is in graph[v] (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes u and v such that there is no path between them.
A graph is bipartite if the nodes can be partitioned into two independent sets A and B such that every edge in the graph connects a node in set A and a node in set B.

Return true if and only if it is bipartite.

## Example
![image](https://github.com/user-attachments/assets/d8267174-d042-4d54-bccc-5b7ec4a8e32b)

Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]

Output: false

Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
## PROGRAM:(Main.cpp)
```
class Solution {
private:
    bool dfs(int node,int col,vector<vector<int>>& graph,vector<int> &vis)
    {
        vis[node]=col;
        for(auto it:graph[node])
        {
            if(vis[it]==-1)
            {
                if(dfs(it,!col,graph,vis)==false) return false;
            }
            else if(vis[it]==col)
            {
                 return false;
            }
        }
        return true;
    }
public:
    bool isBipartite(vector<vector<int>>& graph) 
    {
        int n=graph.size();
        vector<int> vis(n,-1);
        for(int i=0;i<n;i++)
        {
            if(vis[i]==-1)
            {
                if(dfs(i,0,graph,vis)==false) 
                {
                    return false;
                }
            }
        }
        return true;
    }
};
```
## Complexity
- Time complexity : O(V + 2E)
  
             Where V = Vertices, 2E is for total degrees as we traverse all adjacent nodes.

- Space complexity : O(V) + O(V) ~ O(V) 

             Space for Vis Array and Recursion Stack space.
