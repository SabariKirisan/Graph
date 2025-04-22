## Shortest Path in Weighted undirected graph (c++)

You are given a weighted undirected graph having n vertices numbered from 1 to n and m edges along with their weights. Find the shortest weight path between the vertex 1 and the vertex n,  if there exists a path, and return a list of integers whose first element is the weight of the path, and the rest consist of the nodes on that path. If no path exists, then return a list containing a single element -1.

The input list of edges is as follows - {a, b, w}, denoting there is an edge between a and b, and w is the weight of that edge.

Note: The driver code here will first check if the weight of the path returned is equal to the sum of the weights along the nodes on that path, if equal it will output the weight of the path, else -2. In case the list contains only a single element (-1) it will simply output -1. 

## Example
Input: n = 5, m= 6, edges = [[1, 2, 2], [2, 5, 5], [2, 3, 4], [1, 4, 1], [4, 3, 3], [3, 5, 1]]

Output: 5

Explanation: Shortest path from 1 to n is by the path 1 4 3 5 whose weight is 5. 

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    vector<int> shortestPath(int n, int m, vector<vector<int>>& edges) 
    {
        vector<pair<int,int>> adj[n+1];
        for(auto it:edges)
        {
            int u=it[0];
            int v=it[1];
            int w=it[2];
            adj[u].push_back({v,w});
            adj[v].push_back({u,w});
        }
        
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
        
        vector<int> dist(n+1,1e9);
        dist[1]=0;
        vector<int> parent(n+1);
        for(int i=1;i<=n;i++) parent[i]=i;
        
        pq.push({0,1});
        
        while(!pq.empty())
        {
            auto it=pq.top();
            int dis=it.first;
            int node=it.second;
            pq.pop();
            
            for(auto it:adj[node])
            {
                int adjnode=it.first;
                int edge_w=it.second;
                if(dis + edge_w < dist[adjnode])
                {
                    dist[adjnode]=dis+ edge_w;
                    pq.push({dist[adjnode],adjnode});
                    parent[adjnode]=node;
                }
            }
        }
        if(dist[n]==1e9) return {-1};
        
        vector<int>path;
        int node=n;
        while(parent[node] != node)
        {
            path.push_back(node);
            node=parent[node];
        }
        path.push_back(1);
        reverse(path.begin(),path.end());
        
        path.insert(path.begin(), dist[n]);
        
        return path;
    }
};
```
## Complexity
- Time complexity : 
  
         O(m log n + n)

   - Building the adjacency list: O(M)

   - Dijkstra’s Algorithm using Min Heap: O((n + m) log n)

        - You push each edge into the priority queue possibly once: O(m log n)(because each push/pop is log n and you may have to do it up to m times)

        - Each node is popped from the queue once: O(n log n)
    
        - Path reconstruction: O(n)

- Space complexity :

         O(n + m)

    - adj → stores 2m pairs (undirected): O(m)

    - dist and parent arrays: O(n)

    - priority_queue: at most holds n nodes: O(n)
