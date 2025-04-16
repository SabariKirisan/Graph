## BFS in Graph (c++)

Given an adjacency list representation of a directed graph with ‘n’ vertices and ‘m’ edges. Your task is to return a list consisting of Breadth-First Traversal (BFS) starting from vertex 0.

In this traversal, one can move from vertex 'u' to vertex 'v' only if there is an edge from 'u' to 'v'. The BFS traversal should include all nodes directly or indirectly connected to vertex 0.

## Example
![image](https://github.com/user-attachments/assets/661012a9-f443-434c-b831-087e41296cad)

Adjacency list: { {1,2,3},{4}, {5}, {},{},{}}

Output: 0 1 2 3 4 5
## PROGRAM:(Main.cpp)
```
#include<bits/stdc++.h>
using namespace std;
vector<int> bfsTraversal(int n, vector<vector<int>> &adj)
{
    int vis[n]={0};
    vis[0]=1;
    queue<int>q;
    q.push(0);
    vector<int>bfs;
    while(!q.empty())
    {
        int node=q.front();
        q.pop();
        bfs.push_back(node);
        for(auto it : adj[node])
        {
            if(!vis[it])
            {
                vis[it]=1;
                q.push(it);
            }
        }
    }
    return bfs;
}
```
## Complexity
- Time complexity : O(N) + O(E)(Directed grap)

- Space complexity : O(3N)
