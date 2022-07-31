---
cover: >-
  https://images.unsplash.com/photo-1542893849-b14a2c62aacb?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxMHx8bWF4aW11bSUyMGRpc3RhbmNlfGVufDB8fHx8MTY1NTExNDg0Mw&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Max Distance

{% embed url="https://www.interviewbit.com/problems/max-distance/" %}
Given an array **A** of integers, find the maximum of **j - i** subjected to the constraint of **A\[i] <= A\[j]**.
{% endembed %}

### Bruteforce Solution

For every value `i` check every value `j = i + 1` onwards.

```cpp
int Solution::maximumGap(const vector<int> &A) {
    int res = 0;
    for(int i = 0; i < A.size(); i++) 
        for(int j = i + 1; j < A.size(); j++)
            if(A[i] <= A[j])
                res = max(res, j - i);

    return res;
}

```

Time Complexity: $$O(n^2)$$

Space Complexity: $$O(1)$$

### Using DP/Recursion/Memoization

```cpp
int getMaxDist(const vector<int> &A, int i, int j, vector<vector<int>> &dp) {
    if(i == j)
        return 0;
        
    if(A[i] <= A[j])
        return j - i;
        
    if(dp[i][j])
        return dp[i][j];
        
    return dp[i][j] = max(getMaxDist(A, i + 1, j, dp), getMaxDist(A, i, j - 1, dp));
}

int Solution::maximumGap(const vector<int> &A) {
    int i = 0, j = A.size() - 1;
    vector<vector<int>> dp(A.size(), vector<int>(A.size(), 0));
    return getMaxDist(A, i, j, dp);
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)+O(n)$$ for DP and stack

### leftMin and rightMax

```cpp
int Solution::maximumGap(const vector<int> &A) {
    vector<int> lmin(A.size()), rmax(A.size());

    lmin[0] = A[0];
    for(int i = 1; i < A.size(); i++) 
        lmin[i] = min(lmin[i - 1], A[i]);
    
    rmax[A.size() - 1] = A[A.size() - 1];
    for(int i = A.size() - 2; i >= 0; i--)
        rmax[i] = max(rmax[i + 1], A[i]);

    int i = 0, j = 0;
    int maxDist = -1;
    while(i < A.size() && j < A.size())
        if(lmin[i] <= rmax[j]) {
            maxDist = max(maxDist, j - i);
            j++;
        } else 
            i++;

    return maxDist;
}
```

Time Complexity: $$O(n)$$​

Space Complexity :$$O(n)$$​
