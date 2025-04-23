## Number of Ways to Arrive at Destination (c++)

You are in a city that consists of n intersections numbered from 0 to n - 1 with bi-directional roads between some intersections. The inputs are generated such that you can reach any intersection from any other intersection and that there is at most one road between any two intersections.

You are given an integer n and a 2D integer array roads where roads[i] = [ui, vi, timei] means that there is a road between intersections ui and vi that takes timei minutes to travel. You want to know in how many ways you can travel from intersection 0 to intersection n - 1 in the shortest amount of time.

Return the number of ways you can arrive at your destination in the shortest amount of time. Since the answer may be large, return it modulo 109 + 7.

## Example
![image](https://github.com/user-attachments/assets/621bf35e-87de-4be1-aa3c-e88d2c1fc5b4)

Input: n = 7, roads = [[0,6,7],[0,1,2],[1,2,3],[1,3,3],[6,3,3],[3,5,1],[6,5,1],[2,5,1],[0,4,5],[4,6,2]]

Output: 4

Explanation: The shortest amount of time it takes to go from intersection 0 to intersection 6 is 7 minutes.
The four ways to get there in 7 minutes are:

  - 0 ➝ 6
  - 0 ➝ 4 ➝ 6
  - 0 ➝ 1 ➝ 2 ➝ 5 ➝ 6
  - 0 ➝ 1 ➝ 3 ➝ 5 ➝ 6

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int countPaths(int n, vector<vector<int>>& roads) 
    {
        vector<vector<pair<int,int>>> adj(n);
        for(auto it:roads)
        {
            adj[it[0]].push_back({it[1],it[2]});
            adj[it[1]].push_back({it[0],it[2]});
        }
        priority_queue<pair<long long,int>,vector<pair<long long,int>>,greater<pair<long long,int>>> pq;
        pq.push({0,0});
        vector<long long> dist(n,1e18),ways(n,0);
        dist[0]=0;
        ways[0]=1;
        int mod= 1e9+7;
        while(!pq.empty())
        {
            long long dis=pq.top().first;
            int node=pq.top().second;
            pq.pop();

            for(auto it: adj[node])
            {
                int adjnode=it.first;
                long long edge_w=it.second;

                if(dis+edge_w < dist[adjnode])
                {
                    dist[adjnode]=dis+edge_w;
                    pq.push({dist[adjnode],adjnode});
                    ways[adjnode]=ways[node];
                }
                else if(dis+edge_w == dist[adjnode])
                {
                    ways[adjnode]=(ways[adjnode]+ways[node])%mod;
                }
            }
        }
        return ways[n-1]%mod;
    }
};
```
## Complexity
- Time complexity : 
  
         O((n + m) * log n)

     - Build the Adjacency List O(m)
     - Dijkstra’s Algorithm O((n + m) * log n)
    
- Space complexity :

         O(n + m)

     - adj (adjacency list)	O(n + m)
     - dist array	O(n)
     - ways array	O(n)
     - priority_queue	O(n)

