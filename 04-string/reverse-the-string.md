# Reverse the String

<details>

<summary>Thoughts</summary>

* 00:00 This seems to be a super easy question. Just use two-pointers. I'll try to solve this in under 2 minutes.&#x20;
* 6:30 So, it wasn't the simple `reverse a string`. It was `reverse a string word by word`&#x20;
* Took me a while and I did the bad solution where I **used a vector** to store each word.&#x20;
* There's an optimal solution using the reversal of the whole string and then reversing each word, but I don't know how I'll handle the leading and trailing space.&#x20;
* Let me give this approach a try.&#x20;
* 18:00 Ok it wasn't that hard to implement.&#x20;
* The next solution doesn't use a vector to store each word.&#x20;
* 20:00 Done

</details>

### Using vector to store each word

```cpp
string Solution::solve(string A) {
    vector<string> words;
    A += ' ';
    
    int begin = 0, end = 0; 
    while(end < A.size()) 
        if(A[begin] == ' ')     // not a word yet
            begin++, end++;
        else if(end < A.size() && A[end] != ' ')  // is a word. not ended yet. 
            end++;
        else {                  // word ended
            words.push_back(A.substr(begin, end - begin));
            begin = end;      // DON'T FORGET. INFINTE LOOP.  
        }
        
    string res = "";
    for(int i = words.size() - 1; i >= 0; i--)
        res += words[i] + " ";
        
    res.pop_back();
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​ for storing each word

### Reverse the whole string

```cpp
string Solution::solve(string A) {
    reverse(A.begin(), A.end());
    A += ' ';
    int begin = 0, end = 0;
    string res = "";
    while(end < A.size()) 
        if(A[begin] == ' ') 
            begin++, end++;
        else if(end < A.size() && A[end] != ' ')
            end++;
        else {
            string word = A.substr(begin, end - begin);
            reverse(word.begin(), word.end());
            res += word + " ";
            begin = end;
        }
    
    res.pop_back();
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​ for the result.
