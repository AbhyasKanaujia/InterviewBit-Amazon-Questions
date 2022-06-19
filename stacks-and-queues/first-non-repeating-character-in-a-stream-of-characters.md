# ⭐ First non-repeating character in a stream of characters

{% embed url="https://www.interviewbit.com/problems/first-non-repeating-character-in-a-stream-of-characters/" %}

```cpp
string Solution::solve(string A) {
    vector<int> visited(26, 0);
    queue<char> q;
    string res;
    
    for(int x: A) {
        // insert newly visited char in order 
        if(visited[x - 'a'] == 0)
            q.push(x);
        
        visited[x - 'a']++;
        
        while(!q.empty() && visited[q.front() - 'a'] > 1)
            q.pop();
        
        if(q.empty())
            res += '#';
        else
            res += q.front();
    }
    
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
