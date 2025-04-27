## Minimum Spanning Tree - Kruskal's Algorithm (c++)

Given a weighted, undirected, and connected graph with V vertices and E edges, the task is to find the sum of the weights of the edges in the Minimum Spanning Tree (MST) of the graph using Kruskal's Algorithm. The graph is represented as an edge list edges[][], where edges[i] = [u, v, w] denotes an undirected edge between u and v with weight w.

## Example
Input: V = 3, E = 3, edges[][] = [[0, 1, 5], [1, 2, 3], [0, 2, 1]]

![image](https://github.com/user-attachments/assets/c617d9df-3b97-410c-8441-c943df64c540)

Output: 4

Explanation:

![image](https://github.com/user-attachments/assets/fc77408b-e4bd-40f8-8d9b-0cc69db000a5)

The Spanning Tree resulting in a weight of 4 is shown above.

## PROGRAM:(Main.cpp)
```
class DisjointSet 
{
    vector<int> parent, size;
public:
    DisjointSet(int n) 
    {
        parent.resize(n + 1);
        size.resize(n + 1,0);
        for (int i = 0; i <= n; i++) 
        {
            parent[i] = i;
        }
    }

    int findUPar(int node) {
        if (node == parent[node])
            return node;
        return parent[node] = findUPar(parent[node]);
    }
    
    void unionBySize(int u, int v) {
        int ulp_u = findUPar(u);
        int ulp_v = findUPar(v);
        if (ulp_u == ulp_v) return;
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        }
        else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
};
    
class Solution {
  public:
    int kruskalsMST(int V, vector<vector<int>> &edges) 
    {
        DisjointSet ds(V);
        sort(edges.begin(), edges.end(), [](vector<int> &a, vector<int> &b) 
        {
            return a[2] < b[2];
        });
        int mstWt = 0;
        for (auto it : edges) {
            int u = it[0];
            int v = it[1];
            int wt = it[2];

            if (ds.findUPar(u) != ds.findUPar(v)) {
                mstWt += wt;
                ds.unionBySize(u, v);
            }
        }

        return mstWt;
    }
};
```
## Complexity
- Time complexity : 
  
         O(ElogE)+O(E×α(N)) ~ O(ElogE)
    
   - O(N+E) — for extracting edge information from the adjacency list (Correct if the graph was given as adjacency list).
   - O(E logE) — for sorting edges (Correct).
   - O(E × α(N)) — for disjoint set operations inside loop.
     
- Space complexity :

         O(N+E)
  
   - O(N) + O(N) → one for the parent[] array and one for the size[] array used in Disjoint Set.
   - O(E) → for storing the list of edges
