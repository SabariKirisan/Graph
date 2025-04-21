## Shortest Path in Undirected (BFS) (c++)

You are given an adjacency list, adj of Undirected Graph having unit weight of the edges, find the shortest path from src to all the vertex and if it is unreachable to reach any vertex, then return -1 for that vertex.

## Example
Input: adj[][] = [[1, 3], [0, 2], [1, 6], [0, 4], [3, 5], [4, 6], [2, 5, 7, 8], [6, 8], [7, 6]], src=0

Output: [0, 1, 2, 1, 2, 3, 3, 4, 4]

![image](https://github.com/user-attachments/assets/57467afe-d1d4-4dbb-a6d9-59f3c49319dc)

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    vector<int> shortestPath(vector<vector<int>>& adj, int src) 
    {
        int n=adj.size();
        
        vector<int> dis(n,1e9);
        dis[src]=0;
        queue<int> q;
        q.push(src);
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            
            for(auto it:adj[node])
            {
                if(dis[node]+1 < dis[it])
                {
                    dis[it]=dis[node]+1;
                    q.push(it);
                }
            }
        }
        for(int i=0;i<n;i++)
        {
            if(dis[i]==1e9)
            {
                dis[i]=-1;
            }
        }
        return dis;
    }
};
```
## Complexity
- Time complexity : O(N+2E) + O(N) ~ O(N + E)  
  
             O(N + 2E) { for the BFS Algorithm} + O(N) { for adding the final values of the shortest path in the resultant array} ~ O(N+2E).

- Space complexity : O(N) + O(N) + O(N + E) = O(3N + E) ~ O(N + E)

             Distance array dis[n] = O(N),Queue used for BFS = O(N) in the worst case,Adjacency list = O(N + E)

