## Minimum Spanning Tree (c++)

Given a weighted, undirected, and connected graph with V vertices and E edges, your task is to find the sum of the weights of the edges in the Minimum Spanning Tree (MST) of the graph. The graph is represented by an adjacency list, where each element adj[i] is a vector containing vector of integers. Each vector represents an edge, with the first integer denoting the endpoint of the edge and the second integer denoting the weight of the edge.

## Example
Input: 

![image](https://github.com/user-attachments/assets/391d0c65-cb91-488a-96e3-028b3b724ddb)

Output: 4

Explanation:  

![image](https://github.com/user-attachments/assets/73aa3a36-9d4c-4a77-a02f-a01ce8d2f33f)

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    int spanningTree(int V, vector<vector<int>> adj[]) 
    {
        priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
        vector<int>vis (V,0);
        
        pq.push({0,0});
        int sum=0;
        while(!pq.empty())
        {
            auto it=pq.top();
            int node=it.second;
            int wt=it.first;
            pq.pop();
            if(vis[node]==1) continue;
            vis[node]=1;
            sum=sum+wt;
            for(auto it:adj[node])
            {
                int adjnode=it[0];
                int edge_wt=it[1];
                if(vis[adjnode]==0)
                {
                    pq.push({edge_wt,adjnode});
                }
            }
        }
         return sum;
    }
};
```
## Complexity
- Time complexity : 
  
         O(E log V)

   - In the worst case, you might push all edges into the priority queue.

   - Each push or pop from the priority queue takes O(log V) time.

   - For a graph with E edges and V vertices:

       - Each edge can be pushed into the queue at most once.

       - Total heap operations = O(E)

       - Each heap operation takes O(log V) time.

   - Also, you visit each vertex once, but that’s negligible compared to edge operations.
     
- Space complexity :

         O(V)

   - Priority Queue will store at most O(V) elements at any time → O(V)

   - Visited array → O(V)
