## Topological sort (DFS) (c++)

Given a Directed Acyclic Graph (DAG) of V (0 to V-1) vertices and E edges represented as a 2D list of edges[][], where each entry edges[i] = [u, v] denotes a directed edge u -> v. Return the topological sort for the given graph.

Topological sorting for Directed Acyclic Graph (DAG) is a linear ordering of vertices such that for every directed edge u -> v, vertex u comes before v in the ordering.

Note: As there are multiple Topological orders possible, you may return any of them. If your returned Topological sort is correct then the output will be true else false.

## Example
Input: V = 4, E = 3, edges[][] = [[3, 0], [1, 0], [2, 0]]

![image](https://github.com/user-attachments/assets/892487ff-fec7-4427-9192-315dc289af0f)

Output: true

Explanation: The output true denotes that the order is valid. Few valid Topological orders for the given graph are:

[3, 2, 1, 0]

[1, 2, 3, 0]

[2, 3, 1, 0]
## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    void dfs(int node,stack<int> &st,vector<vector<int>>&adj,vector<int>&vis)
    {
        vis[node]=1;
        for(auto it:adj[node])
        {
            if(vis[it]==0)
            {
                dfs(it,st,adj,vis);
            }
        }
        st.push(node);
    }
  public:
    vector<int> topoSort(int V, vector<vector<int>>& edges) 
    {
        vector<vector<int>> adj(V);
        for(int i=0;i<edges.size();i++)
        {
            int u=edges[i][0];
            int v=edges[i][1];
            adj[u].push_back(v);
        }
        
        stack<int> st;
        vector<int> vis(V,0);
        for(int i=0;i<V;i++)
        {
            if(vis[i]==0)
            {
                dfs(i,st,adj,vis);
            }
        }
        
        vector<int> ans;
        while(!st.empty())
        {
            ans.push_back(st.top());
            st.pop();
        }
        return ans;
    }
};
```
## Complexity
- Time complexity : O(V+E)+O(V)
  
             where V = no. of nodes and E = no. of edges. There can be at most V components. So, another O(V) time complexity.

- Space complexity : O(2N) + O(N) ~ O(N)

             O(2N) for the visited array and the stack carried during DFS calls and O(N) for recursive stack space, where N = no. of nodes.
