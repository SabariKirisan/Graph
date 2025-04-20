## Kahn's Algorithm | Alien Dictionary (BFS) (c++)

A new alien language uses the English alphabet, but the order of letters is unknown. You are given a list of words[] from the alien language’s dictionary, where the words are claimed to be sorted lexicographically according to the language’s rules.

Your task is to determine the correct order of letters in this alien language based on the given words. If the order is valid, return a string containing the unique letters in lexicographically increasing order as per the new language's rules. If there are multiple valid orders, return any one of them.

However, if the given arrangement of words is inconsistent with any possible letter ordering, return an empty string ("").

A string a is lexicographically smaller than a string b if, at the first position where they differ, the character in a appears earlier in the alien language than the corresponding character in b. If all characters in the shorter word match the beginning of the longer word, the shorter word is considered smaller.

Note: Your implementation will be tested using a driver code. It will print true if your returned order correctly follows the alien language’s lexicographic rules; otherwise, it will print false.
## Example
Input: words[] = ["caa", "aaa", "aab"]

Output: true

Explanation: A possible corrct order of letters in the alien dictionary is "cab".

The pair "caa" and "aaa" suggests 'c' appears before 'a'.

The pair "aaa" and "aab" suggests 'a' appear before 'b' in the alien dictionary. 

So, 'c' → 'a' → 'b' is a valid ordering.
## PROGRAM:(Main.cpp)
```
class Solution {
  private:
    vector<int> topoSort(int V, vector<vector<int>>& adj) 
    {
        
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
        return ans;
    }
  public:
    string findOrder(vector<string> &words) 
    {
        int n=words.size();
        unordered_set<char> uniqueChars;
        for (int i = 0; i < words.size(); i++) 
        {
            for (int j = 0; j < words[i].size(); j++) 
            {
                char ch = words[i][j];
                if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z')) 
                {
                    uniqueChars.insert(ch);
                }
            }
        }
        vector<char> chars(uniqueChars.begin(), uniqueChars.end());
        unordered_map<char, int> charToIndex;
        for (int i = 0; i < chars.size(); i++) 
        {
            charToIndex[chars[i]] = i;
        }
        
        int k = chars.size();
        vector<vector<int>>adj(k);
        for(int i=0;i<n-1;i++)
        {
            string s1=words[i];
            string s2=words[i+1];
            int len=min(s1.size(),s2.size());
            bool foundDiffering = false;
            for(int ptr=0;ptr<len;ptr++)
            {
                if(s1[ptr] != s2[ptr])
                {
                    int u = charToIndex[s1[ptr]];
                    int v = charToIndex[s2[ptr]];
                    adj[u].push_back(v);
                    foundDiffering = true;
                    break;
                }
            }
            if (!foundDiffering && s1.size() > s2.size()) 
            {
                return "";
            }
        }
        vector<int> topo=topoSort(k,adj);
        if (topo.size() != k) 
        {
            return "";
        }
        
        string ans="";
        for (int idx : topo) {
            ans += chars[idx];
        }
        return ans;
    }
};
```
## Complexity
- Time complexity : O(N * L + k^2)
  
              Creating uniqueChars: O(N * L),Converting to chars: O(k),Building charToIndex: O(k),Building the adjacency list: O(N * L),Topological Sort: O(k^2),Constructing the result string: O(k)
              where:
                  - N is the number of words,
                  - L is the average length of the words,
                  - k is the number of unique characters in the words.

- Space complexity : O(N) + O(N) + O(N) + O(N) = O(4N) ~ O(N)

             uniqueChars set: O(k),chars vector: O(k),charToIndex map: O(k),adj (adjacency list): O(k + E) where E is the number of edges.,Topological sort uses additional space for the queue and result: O(k).
             where:
                  - k is the number of unique characters
                  - E is the number of edges in the graph
   
