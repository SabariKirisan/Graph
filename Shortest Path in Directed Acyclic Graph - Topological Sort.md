## Shortest Path in Directed Acyclic Graph - Topological Sort (DFS) (c++)

Given a Directed Acyclic Graph of V vertices from 0 to n-1 and a 2D Integer array(or vector) edges[ ][ ] of length E, where there is a directed edge from edge[i][0] to edge[i][1] with a distance of edge[i][2] for all i.

Find the shortest path from src(0) vertex to all the vertices and if it is impossible to reach any vertex, then return -1 for that vertex.

## Example
Input: V = 4, E = 2, edges = [[0,1,2], [0,2,1]]

Output: [0, 2, 1, -1]

Explanation: Shortest path from 0 to 1 is 0->1 with edge weight 2. Shortest path from 0 to 2 is 0->2 with edge weight 1. There is no way we can reach 3, so it's -1 for 3.

## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    void dfs(int node,stack<int> &st,vector<int> &vis,vector<pair<int, int>> adj[])
    {
        vis[node]=1;
        for(auto it:adj[node])
        {
            int f=it.first;
            if(!vis[f])
            {
                dfs(f,st,vis,adj);
            }
        }
        st.push(node);
    }
  public:
    vector<int> shortestPath(int V, int E, vector<vector<int>>& edges) 
    {
        vector<pair<int, int>> adj[V]; 
        for(int i=0;i<E;i++)
        {
            int u=edges[i][0];
            int v=edges[i][1];
            int wt=edges[i][2];
            adj[u].push_back({v,wt});
        }
        
        vector<int> vis(V,0);
        stack<int> st;
        for(int i=0;i<V;i++)
        {
            if(vis[i]==0)
            {
                dfs(i,st,vis,adj);
            }
        }
        
        vector<int> dis(V,1e9);
        dis[0]=0;
        while(!st.empty())
        {
            int node=st.top();
            st.pop();
            for(auto it:adj[node])
            {
                int f=it.first;
                int wt=it.second;
                
                if(dis[node]+wt < dis[f])
                {
                    dis[f]=dis[node]+wt;
                }
            }
        }
        for(int i = 0; i < V; i++) 
        {
            if(dis[i] == 1e9) dis[i] = -1;
        }
        return dis;
    }
};
```
## Complexity
- Time complexity : O(V+E) + O(V+E) + O(E) = O(2V + 3E) ~ O(V + E)  
  
             Building the Adjacency List Runs in O(E),Each node is visited once, and for each node, we explore all its outgoing edges ,DFS complexity = O(V + E),Again, we go through all nodes and for each node, all its outgoing edges,This is O(V + E)

- Space complexity : O(V+ E) + O(V) + O(V) + O(V) = O(4V + E) ~ O(V + E)

             Adjacency list Uses O(V + E),Visited array Uses O(V),Stack for topological sort Uses O(V),Distance array Uses O(V)
