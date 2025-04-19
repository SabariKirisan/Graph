## Find Eventual Safe States (DFS) (c++)

- There is a directed graph of n nodes with each node labeled from 0 to n - 1. The graph is represented by a 0-indexed 2D integer array graph where graph[i] is an integer array of nodes adjacent to node i, meaning there is an edge from node i to each node in graph[i].

- A node is a terminal node if there are no outgoing edges. A node is a safe node if every possible path starting from that node leads to a terminal node (or another safe node).

- Return an array containing all the safe nodes of the graph. The answer should be sorted in ascending order.

## Example
![image](https://github.com/user-attachments/assets/ebb97662-a325-431d-9102-7dd204b194f9)

Input: graph = [[1,2],[2,3],[5],[0],[5],[],[]]

Output: [2,4,5,6]

Explanation: The given graph is shown above.

Nodes 5 and 6 are terminal nodes as there are no outgoing edges from either of them.
Every path starting at nodes 2, 4, 5, and 6 all lead to either node 5 or 6.
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
- Time complexity : O(V+E) + O(V) ~ O(V + E)
  
             where V = no. of nodes and E = no. of edges. There can be at most V components. So, another O(V) time complexity.

- Space complexity : O(3N) + O(N) ~ O(N)

             O(3N) for Three arrays and O(N) for recursive stack space.
