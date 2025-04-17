## Number of Provinces (c++)

There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A province is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.

## Example
![image](https://github.com/user-attachments/assets/90a35ea2-950a-4f76-950d-b29ccdf39d09)

Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]

Output: 2
## PROGRAM:(Main.cpp)
```
class Solution 
{
private:
void dfs(int node,vector<int> &vis,vector<int> adj[])
{
    vis[node]=1;
    for(auto it:adj[node])
    {
        if(!vis[it])
        {
            dfs(it,vis,adj);
        }
    }
}
public:
    int findCircleNum(vector<vector<int>>& isConnected) 
    {
        int v=isConnected.size();
        vector<int>adj[v];

        for(int i=0;i<v;i++)
        {
            for(int j=0;j<v;j++)
            {
                if(isConnected[i][j]==1 && i!=j)
                {
                    adj[i].push_back(j);
                    adj[j].push_back(i);
                }
            }
        }  

        int cnt=0;
        vector<int> vis(v, 0);
        for(int i=0;i<v;i++)
        {
            if(!vis[i])
            {
                cnt++;
                dfs(i,vis,adj);
            }
        } 
        return cnt;
    }
};
```
## Complexity
- Time complexity : O(N) + O(V+2E), Where O(N) is for outer loop and inner loop runs in total a single DFS over entire graph, and we know DFS takes a time of O(V+2E). 

- Space complexity : O(N) + O(N),Space for recursion stack space and visited array.
