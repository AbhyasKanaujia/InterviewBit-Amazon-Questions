---
cover: >-
  https://images.unsplash.com/photo-1565095747113-c462f5fbf6d6?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxkaWZmZXJlbmNlfGVufDB8fHx8MTY1OTM3OTcwOQ&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Maximum Absolute Difference

{% embed url="https://www.interviewbit.com/problems/maximum-absolute-difference/" %}
Return maximum value of `f(i, j)` for all 1 ≤ _i, j_ ≤ N.\
`f(i, j)` is defined as `|A[i] - A[j]| + |i - j|`
{% endembed %}

### Brute Force Solution

```cpp
int Solution::maxArr(vector<int> &A) {
    int n = A.size();
    int maximum = INT_MIN;
    for(int i = 0; i < n; i++)
        for(int j = i + 1; j < n; j++)
            maximum = max(maximum, abs(A[i] - A[j]) + j - i);

    return maximum;
}
```

### Optimal ?

```cpp
int Solution::maxArr(vector<int> &A) {
    int ans = 0, n = A.size();

    int max1 = INT_MIN, max2 = INT_MIN;
    int min1 = INT_MAX, min2 = INT_MAX;

    for(int i = 0; i < n; i++) {
        max1 = max(max1, A[i] + i);
        max2 = max(max2, A[i] - i);
        min1 = min(min1, A[i] + i);
        min2 = min(min2, A[i] - i);
    }

    ans = max(ans, max2 - min2);
    ans = max(ans, max1 - min1);

    return ans;
}
```
