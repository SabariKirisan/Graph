## Kahn's Algorithm | Find Eventual Safe States (BFS) (c++)

There is a directed graph of n nodes with each node labeled from 0 to n - 1. The graph is represented by a 0-indexed 2D integer array graph where graph[i] is an integer array of nodes adjacent to node i, meaning there is an edge from node i to each node in graph[i].

A node is a terminal node if there are no outgoing edges. A node is a safe node if every possible path starting from that node leads to a terminal node (or another safe node).

Return an array containing all the safe nodes of the graph. The answer should be sorted in ascending order.

## Example
![image](https://github.com/user-attachments/assets/86fe2715-6b89-4c65-9848-6d2fb417b1b4)

Input: graph = [[1,2],[2,3],[5],[0],[5],[],[]]

Output: [2,4,5,6]

Explanation: The given graph is shown above.
Nodes 5 and 6 are terminal nodes as there are no outgoing edges from either of them.
Every path starting at nodes 2, 4, 5, and 6 all lead to either node 5 or 6.
## PROGRAM:(Main.cpp)
```
class Solution {
public:
    vector<int> eventualSafeNodes(vector<vector<int>>& graph) 
    {
        int V=graph.size();
        vector<vector<int>> adj(V);
        for(int u = 0; u < V; u++) 
        {
            for(int j=0; j<graph[u].size();j++) 
            {
                int v=graph[u][j];
                adj[v].push_back(u);  
            }
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
        sort(ans.begin(),ans.end());
        return ans;
    }
};
```
## Complexity
- Time complexity : O(V+E)+O(N*logN)
  
              where V = no. of nodes and E = no. of edges. This is a simple BFS algorithm. Extra O(N*logN) for sorting the safeNodes array, where N is the number of safe nodes.

- Space complexity : O(N) + O(N) + O(N) + O(N) = O(4N) ~ O(N)

             O(N) for the ans ,O(N) for the indegree array, O(N) for the queue data structure used in BFS(where N = no.of nodes), and extra O(N) for the adjacency list to store the graph in a reversed order.
