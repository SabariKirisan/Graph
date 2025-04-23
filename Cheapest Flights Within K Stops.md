## Cheapest Flights Within K Stops (c++)

There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

## Example
![image](https://github.com/user-attachments/assets/79591dcb-405b-4152-a83a-fdbac25d1961)

Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1

Output: 700

Explanation:The graph is shown above.

The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.

Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) 
    {
        vector<vector<pair<int,int>>> adj(n);
        for(auto it:flights)
        {
            int u=it[0];
            int v=it[1];
            int w=it[2];
            adj[u].push_back({v,w});
        }     
        vector<int> dist(n,1e9);
        dist[src]=0;
        queue<tuple<int, int, int>> q;
        q.push({0,src,0});
        while(!q.empty())
        {
            auto [stops,node,cost]=q.front();
            q.pop();

            if(stops > k) continue;

            for(auto it:adj[node])
            {
                int adjnode=it.first;
                int edge_w=it.second;
                if(cost + edge_w < dist[adjnode] && stops <=k)
                {
                    dist[adjnode] =cost+edge_w;
                    q.push({stops+1,adjnode,dist[adjnode]});
                }
            }  
        }
        if(dist[dst]==1e9) return -1;
        return dist[dst];
    }
};
```
## Complexity
- Time complexity : 
  
         O((k+1) * m) 

   - Building the adjacency list takes O(m).
   - Each node may be visited up to k + 1 times (0 stops to k stops)
   - So total operations ≈ O((k+1) * m)
- Space complexity :

         O( N + M )

    - Adjacency list: O(m)
    - Queue: In worst case, holds O((k+1) * n) entries
    - Distance array: O(n)
