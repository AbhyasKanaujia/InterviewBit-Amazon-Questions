# Assign Mice to Holes

{% embed url="https://www.interviewbit.com/problems/assign-mice-to-holes/" %}

```cpp
int Solution::mice(vector<int> &A, vector<int> &B) {
    sort(A.begin(), A.end());
    sort(B.begin(), B.end());
    
    int maxDifference = INT_MIN;
    
    for(int i = 0; i < A.size(); i++)
        maxDifference = max(maxDifference, abs(A[i] - B[i]));
        
    return maxDifference;
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(1)$$​
