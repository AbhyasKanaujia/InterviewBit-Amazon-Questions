# Length of Last Word

{% embed url="https://www.interviewbit.com/problems/length-of-last-word/" %}

```cpp
int Solution::lengthOfLastWord(const string A) {
    int len = 0;
    int i = A.size() - 1;
    while(i >= 0 && A[i] == ' ')
        i--;
    while(i >= 0 && A[i] != ' ')
        i--, len++;
        
    return len;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​

Edge Case: What if there are spaces the end of the string `"Hello Wolrd   "`
