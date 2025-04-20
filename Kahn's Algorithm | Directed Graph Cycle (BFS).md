## Kahn's Algorithm | Directed Graph Cycle (BFS) (c++)

Given a Directed Graph with V vertices (Numbered from 0 to V-1) and E edges, check whether it contains any cycle or not.
The graph is represented as a 2D vector edges[][], where each entry edges[i] = [u, v] denotes an edge from verticex u to v.

## Example
Input: V = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]

![image](https://github.com/user-attachments/assets/6992b413-fcbd-48ea-8092-6e540a3daf4b)

Output: true

Explanation: The diagram clearly shows a cycle 0 → 2 → 0
## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    bool isCyclic(int V, vector<vector<int>> &edges) 
    {
        vector<vector<int>> adj(V);
        for(int i=0;i<edges.size();i++)
        {
            int u=edges[i][0];
            int v=edges[i][1];
            adj[u].push_back(v);
        }
        
        vector<int> indegree(V,0);
        for(int i=0;i<V;i++)
        {
            for(auto it: adj[i])
            {
                indegree[it]++;
            }
        }
        
        queue<int> q;
        for(int i=0;i<V;i++)
        {
            if(indegree[i]==0)
            {
                q.push(i);
            }
        }

        int cnt=0;
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            cnt++;
            for(auto it:adj[node])
            {
                indegree[it]--;
                if(indegree[it]==0)
                {
                    q.push(it);
                }
            }
        }
        if(cnt==V) return false;
        return true;
    }
};
```
## Complexity
- Time complexity : O(V+E)
  
             where V = no. of nodes and E = no. of edges. This is a simple BFS algorithm.

- Space complexity : O(V) + O(V) = O(2V) ~ O(V)

             O(N) for the indegree array, and O(N) for the queue data structure used in BFS(where N = no.of nodes).
