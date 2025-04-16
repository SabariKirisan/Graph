## DFS Traversal (c++)

Given an undirected and disconnected graph G(V, E), containing 'V' vertices and 'E' edges, the information about edges is given using 'GRAPH' matrix, where i-th edge is between GRAPH[i][0] and GRAPH[i][1]. print its DFS traversal.

V is the number of vertices present in graph G and vertices are numbered from 0 to V-1. 

E is the number of edges present in graph G.

Note : The Graph may not be connected i.e there may exist multiple components in a graph.
## Example

## PROGRAM:(Main.cpp)
```
#include <bits/stdc++.h>
using namespace std;

void dfs(int node, vector<vector<int>> &edges, vector<int> &vis, vector<int> &ls) 
{
    vis[node] = 1;
    ls.push_back(node);
    for (auto it : edges[node]) 
    {
        if (!vis[it]) 
        {
            dfs(it, edges, vis, ls);
        }
    }
}

vector<vector<int>> depthFirstSearch(int V, int E, vector<vector<int>> &edges) 
{
    vector<int> vis(V, 0);
    vector<vector<int>> adj(V);

    for (auto edge : edges) 
    {
        int u = edge[0];
        int v = edge[1];
        adj[u].push_back(v);
        adj[v].push_back(u); 
    }

    vector<vector<int>> result;

    for (int i = 0; i < V; i++) 
    {
        if (!vis[i]) 
        {
            vector<int> ls;
            dfs(i, adj, vis, ls);
            result.push_back(ls);
        }
    }
    return result;
}
```
## Complexity
- Time complexity : O(N) + O(E)(Directed grap)

- Space complexity : O(3N) ~ O(N)
