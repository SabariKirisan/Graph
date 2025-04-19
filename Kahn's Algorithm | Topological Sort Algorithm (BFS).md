## Kahn's Algorithm | Topological Sort Algorithm (BFS) (c++)

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

        vector<int> ans;
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            ans.push_back(node);
            for(auto it:adj[node])
            {
                indegree[it]--;
                if(indegree[it]==0)
                {
                    q.push(it);
                }
            }
        }
        return ans;
    }
};
```
## Complexity
- Time complexity : O(V+E)
  
             where V = no. of nodes and E = no. of edges. This is a simple BFS algorithm.

- Space complexity : O(N) + O(N) ~ O(2N)

             O(N) for the indegree array, and O(N) for the queue data structure used in BFS(where N = no.of nodes).
