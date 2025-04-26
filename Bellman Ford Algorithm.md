## Bellman Ford Algorithm (c++)

Given an weighted graph with V vertices numbered from 0 to V-1 and E edges, represented by a 2d array edges[][], where edges[i] = [u, v, w] represents a direct edge from node u to v having w edge weight. You are also given a source vertex src.

Your task is to compute the shortest distances from the source to all other vertices. If a vertex is unreachable from the source, its distance should be marked as 108. Additionally, if the graph contains a negative weight cycle, return [-1] to indicate that shortest paths cannot be reliably computed.

## Example
Input: V = 5, edges[][] = [[1, 3, 2], [4, 3, -1], [2, 4, 1], [1, 2, 1], [0, 1, 5]], src = 0

![image](https://github.com/user-attachments/assets/dc41f586-4bc8-45ea-9dba-52e92840fcc7)

Output: [0, 5, 6, 6, 7]

Explanation: Shortest Paths:

- For 0 to 1 minimum distance will be 5. By following path 0 → 1

- For 0 to 2 minimum distance will be 6. By following path 0 → 1  → 2

- For 0 to 3 minimum distance will be 6. By following path 0 → 1  → 2 → 4 → 3 

- For 0 to 4 minimum distance will be 7. By following path 0 → 1  → 2 → 4

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    vector<int> bellmanFord(int V, vector<vector<int>>& edges, int src) 
    {
        vector<int> dis(V,1e8);
        dis[src]=0;
        for(int i=0;i<V-1;i++)
        {
            for(auto it:edges)
            {
                int u=it[0];
                int v=it[1];
                int wt=it[2];
                if(dis[u]!=1e8 && dis[u]+wt<dis[v])
                {
                    dis[v]=dis[u]+wt;
                }
            }
        }
        for(auto it:edges)
        {
            int u=it[0];
            int v=it[1];
            int wt=it[2];
            if(dis[u]!=1e8 && dis[u]+wt<dis[v])
            {
                return{-1};
            }
        }
        return dis;
    }
};
```
## Complexity
- Time complexity : 
  
         O(V*E)

   - V = no. of vertices
   - E = no. of Edges.
     
- Space complexity :

         O(V) for the distance array which stores the minimized distances.
