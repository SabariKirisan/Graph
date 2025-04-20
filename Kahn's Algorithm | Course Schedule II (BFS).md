## Kahn's Algorithm | Course Schedule II (BFS) (c++)

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

- For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

## Example
Input: numCourses = 2, prerequisites = [[1,0]]

Output: [0,1]

Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
## PROGRAM:(Main.cpp)
```
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) 
    {
        int V=numCourses;
        vector<vector<int>> adj(V);
        for(int i=0;i<prerequisites.size();i++)
        {
            int u=prerequisites[i][0];
            int v=prerequisites[i][1];
            adj[v].push_back(u);
        }
        
        vector<int> indegree(V,0);
        for(int i=0;i<V;i++)
        {
            for(auto it: adj[i])
            {
                indegree[it]++;
            }
        }
        
        queue<int> q;
        for(int i=0;i<V;i++)
        {
            if(indegree[i]==0)
            {
                q.push(i);
            }
        }

        vector<int> ans;
        while(!q.empty())
        {
            int node=q.front();
            q.pop();
            ans.push_back(node);
            for(auto it:adj[node])
            {
                indegree[it]--;
                if(indegree[it]==0)
                {
                    q.push(it);
                }
            }
        }
        if(ans.size()==V) return ans;
        return {};
    }
};
```
## Complexity
- Time complexity : O(V+E)
  
             where V = no. of nodes and E = no. of edges. This is a simple BFS algorithm.

- Space complexity : O(N) + O(N) ~ O(2N)

             O(N) for the indegree array, and O(N) for the queue data structure used in BFS(where N = no.of nodes).
