## Dijkstra Algorithm (c++)

Given an undirected, weighted graph with V vertices numbered from 0 to V-1 and E edges, represented by 2d array edges[][], where edges[i]=[u, v, w] represents the edge between the nodes u and v having w edge weight.

You have to find the shortest distance of all the vertices from the source vertex src, and return an array of integers where the ith element denotes the shortest distance between ith node and source vertex src.

Note: The Graph is connected and doesn't contain any negative weight edge.

## Example
Input: V = 3, edges[][] = [[0, 1, 1], [1, 2, 3], [0, 2, 6]], src = 2

Output: [4, 3, 0]

Explanation:

![image](https://github.com/user-attachments/assets/5461f3be-f044-4a50-ad5c-6d954d99e829)


Shortest Paths:

For 2 to 0 minimum distance will be 4. By following path 2 -> 1 -> 0

For 2 to 1 minimum distance will be 3. By following path 2 -> 1

For 2 to 2 minimum distance will be 0. By following path 2 -> 2

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    vector<int> dijkstra(int V, vector<vector<int>> &edges, int src) 
    {
        vector<pair<int,int>> adj[V];
        for(int i=0;i<edges.size();i++)
        {
            int u=edges[i][0];
            int v=edges[i][1];
            int w=edges[i][2];
            adj[u].push_back({v,w});
            adj[v].push_back({u,w});
        }
        
        vector<int>dist(V,1e9);
        dist[src]=0;
        set<pair<int,int>> st;
        st.insert({0,src});
        
        while(!st.empty())
        {
            auto it=*(st.begin());
            int node=it.second;
            int dis=it.first;
            st.erase(it);
            
            for(auto it:adj[node])
            {
                int edge_w=it.second;
                int adjnode=it.first;
                
                if(edge_w + dis < dist[adjnode])
                {
                    dist[adjnode]=edge_w + dis;
                    st.insert({dist[adjnode],adjnode});
                }
            }
        }
        return dist;
    }
};
```
## Complexity
- Time complexity : 
  
         O((V + E) * log V)

   - Building the adjacency list: O(E)

   - Using set<pair<int,int>> st:

        - In the worst case, we could insert up to E elements into the set (each relaxation can insert a new entry).

        - Each insert or erase in set takes O(log N) time.

- Space complexity :

         O(V + E)

    - Adjacency list: O(V + E)

    - Distance array: O(V)

    - Set → holds up to O(V) elements at a time (can insert up to E times) → O(V) average
