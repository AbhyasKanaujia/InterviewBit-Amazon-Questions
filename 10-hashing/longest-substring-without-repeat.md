# Longest Substring Without Repeat

{% embed url="https://www.interviewbit.com/problems/longest-substring-without-repeat/" %}

{% tabs %}
{% tab title="C++" %}
```cpp
int Solution::lengthOfLongestSubstring(string A) {
    unordered_set<char> s;
    int begin = -1;
    int end = -1;
    int maxLength = 0;
    for(const char &ch: A) {
        while(s.find(ch) != s.end()) {
            begin++;
            s.erase(A[begin]);
        } 
        
        end++;
        s.insert(A[end]);
        maxLength = max(maxLength, end - begin);
    }
    
    return maxLength;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
