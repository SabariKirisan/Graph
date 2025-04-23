## Path With Minimum Effort (c++)

You are a hiker preparing for an upcoming hike. You are given heights, a 2D array of size rows x columns, where heights[row][col] represents the height of cell (row, col). You are situated in the top-left cell, (0, 0), and you hope to travel to the bottom-right cell, (rows-1, columns-1) (i.e., 0-indexed). You can move up, down, left, or right, and you wish to find a route that requires the minimum effort.

A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the minimum effort required to travel from the top-left cell to the bottom-right cell.

## Example
![image](https://github.com/user-attachments/assets/af32b2f8-d27b-4989-adfa-ba45b145d7ea)

Input: heights = [[1,2,2],[3,8,2],[5,3,5]]

Output: 2

Explanation: The route of [1,3,5,3,5] has a maximum absolute difference of 2 in consecutive cells.
This is better than the route of [1,2,2,2,5], where the maximum absolute difference is 3.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) 
    {
        int n=heights.size();
        int m=heights[0].size();

        priority_queue<pair<int,pair<int,int>>,vector<pair<int,pair<int,int>>>,greater<pair<int,pair<int,int>>>> pq;
        
        vector<vector<int>> dist(n,vector<int>(m,1e9));
        dist[0][0]=0;
        pq.push({0,{0,0}});
        while(!pq.empty())
        {
            auto it=pq.top();
            pq.pop();
            int diff=it.first;
            int row=it.second.first;
            int col=it.second.second;

            if(row==n-1 && col==m-1) return diff;

            int drow[]={-1,0,1,0};
            int dcol[]={0,-1,0,1};

            for(int i=0;i<4;i++)
            {
                int nrow=row+drow[i];
                int ncol=col+dcol[i];

                if(nrow >=0 && nrow < n && ncol >=0 && ncol < m)
                {
                    int new_effort=max(abs(heights[row][col]-heights[nrow][ncol]),diff);
                    if(new_effort < dist[nrow][ncol])
                    {
                        dist[nrow][ncol]=new_effort;
                        pq.push({new_effort,{nrow,ncol}});
                    }
                }
            }
        }
        return 0;
    }
};
```
## Complexity
- Time complexity : 
  
         O( 4*N*M * log( N*M) ) 

   - N*M are the total cells, for each of which we also check 4 adjacent nodes for the minimum effort and additional log(N*M) for insertion-deletion operations in a priority queue 

- Space complexity :

         O( N*M )

    - N = No. of rows
    - M = No. of columns 
