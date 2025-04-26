## Floyd Warshall (c++)

You are given an weighted directed graph, represented by an adjacency matrix, dist[][] of size n x n, where dist[i][j] represents the weight of the edge from node i to node j. If there is no direct edge, dist[i][j] is set to a large value (i.e., 108) to represent infinity.

The graph may contain negative edge weights, but it does not contain any negative weight cycles.

Your task is to find the shortest distance between every pair of nodes i and j in the graph.

Note: Modify the distances for every pair in place.

## Example
Input: dist[][] = [[0, 4, 108, 5, 108], [108, 0, 1, 108, 6], [2, 108, 0, 3, 108], [108, 108, 1, 0, 2], [1, 108, 108, 4, 0]]

![image](https://github.com/user-attachments/assets/8daeb3f2-29fe-42ff-98a2-1d295a20d3ac)

Output: [[0, 4, 5, 5, 7], [3, 0, 1, 4, 6], [2, 6, 0, 3, 5], [3, 7, 1, 0, 2], [1, 5, 5, 4, 0]]

![image](https://github.com/user-attachments/assets/b0b0e312-a088-43ce-822d-56cc86d51435)

Explanation: Each cell dist[i][j] in the output shows the shortest distance from node i to node j, computed by considering all possible intermediate nodes.

## PROGRAM:(Main.cpp)
```
class Solution {
  public:
    void floydWarshall(vector<vector<int>> &dist) 
    {
        int n = dist.size();
        
        for(int k = 0; k < n; k++)
        {
            for(int i = 0; i < n; i++)
            {
                for(int j = 0; j < n; j++)
                {
                    if(dist[i][k] < 1e8 && dist[k][j] < 1e8)
                    {
                        dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                    } 
                }
            }
        }
    }
};
```
## Complexity
- Time complexity : 
  
         O(n³)
     
- Space complexity :

         O(n²)
