## Find the City With the Smallest Number of Neighbors at a Threshold Distance (c++)

There are n cities numbered from 0 to n-1. Given the array edges where edges[i] = [fromi, toi, weighti] represents a bidirectional and weighted edge between cities fromi and toi, and given the integer distanceThreshold.

Return the city with the smallest number of cities that are reachable through some path and whose distance is at most distanceThreshold, If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities i and j is equal to the sum of the edges' weights along that path.

## Example
![image](https://github.com/user-attachments/assets/a165039a-9a00-4044-a8fc-19a82264a093)

Input: n = 4, edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4

Output: 3

Explanation: The figure above describes the graph. 

The neighboring cities at a distanceThreshold = 4 for each city are:
 - City 0 -> [City 1, City 2] 
 - City 1 -> [City 0, City 2, City 3] 
 - City 2 -> [City 0, City 1, City 3] 
 - City 3 -> [City 1, City 2] 

Cities 0 and 3 have 2 neighboring cities at a distanceThreshold = 4, but we have to return city 3 since it has the greatest number.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int findTheCity(int n, vector<vector<int>>& edges, int distanceThreshold) 
    {
        vector<vector<int>> dis(n,vector<int>(n,INT_MAX));
        for(auto it:edges)
        {
            dis[it[0]][it[1]]=it[2];
            dis[it[1]][it[0]]=it[2];
        }

        for(int i=0;i<n;i++) dis[i][i]=0;
        for(int k=0;k<n;k++)
        {
            for(int i=0;i<n;i++)
            {
                for(int j=0;j<n;j++)
                {
                    if(dis[i][k]==INT_MAX || dis[k][j]==INT_MAX)
                    {
                        continue;
                    }
                    dis[i][j]=min(dis[i][j],dis[i][k]+dis[k][j]);
                }
            }
        }   

        int cntcity=n;
        int cityno=-1;
        for(int city=0;city<n;city++)
        {
            int cnt=0;
            for(int adjcity=0;adjcity<n;adjcity++)
            {
                if(dis[city][adjcity]<=distanceThreshold)
                {
                    cnt++;
                }
            }
            if(cnt<=cntcity)
            {
                cntcity=cnt;
                cityno=city;
            }
        }
        return cityno;
    }
};
```
## Complexity
- Time complexity : 
  
         O(V^3), as we have three nested loops each running for V times.

   - V = no. of vertices.
     
- Space complexity :

         O(V^2), This space complexity is due to storing the adjacency matrix of the given graph.
   - V = no. of vertices. 
