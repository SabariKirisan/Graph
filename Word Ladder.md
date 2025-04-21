## Word Ladder (c++)

A transformation sequence from word beginWord to word endWord using a dictionary wordList is a sequence of words beginWord -> s1 -> s2 -> ... -> sk such that:

Every adjacent pair of words differs by a single letter.

Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.

sk == endWord

Given two words, beginWord and endWord, and a dictionary wordList, return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.

## Example
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) 
    {
        unordered_set<string> st(wordList.begin(),wordList.end());
        queue<pair<string,int>> q;
        q.push({beginWord,1});
        st.erase(beginWord);

        while(!q.empty())
        {
            string word=q.front().first;
            int step =q.front().second;
            q.pop();
            if(word==endWord) return step;
            for(int i=0;i<word.size();i++)
            {
                char orginal=word[i];
                for(char ch='a';ch<='z';ch++)
                {
                    word[i]=ch;
                    if(st.find(word) != st.end())
                    {
                        st.erase(word);
                        q.push({word,step+1});
                    }
                }
                word[i]=orginal;
            }
        }
        return 0;
    }
};
```
## Complexity
- Time complexity : O(N * M * 26) 
  
            Where N = size of wordList Array and M = word length of words present in the wordList.

Note that, hashing operations in an unordered set takes O(1) time, but if you want to use set here, then the time complexity would increase by a factor of log(N) as hashing operations in a set take O(log(N)) time.

- Space complexity : O(N)

            unordered_set st stores all N words → O(N). queue stores words along with steps (at most N words) → O(N).

