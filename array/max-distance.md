# Max Distance

{% embed url="https://www.interviewbit.com/problems/max-distance/" %}

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
