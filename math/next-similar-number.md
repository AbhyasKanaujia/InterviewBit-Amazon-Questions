# Next Similar Number

{% embed url="https://www.interviewbit.com/problems/next-similar-number/" %}

### Next Permutation

```cpp
string Solution::solve(string A) {
    int breakpoint;
    for(breakpoint = A.size() - 2; breakpoint >= 0; breakpoint--) 
        if(A[breakpoint] < A[breakpoint + 1])
            break;

    if(breakpoint == -1)
        return "-1";
    // find next larger

    int nextLarger;
    for(nextLarger = A.size() - 1; nextLarger > breakpoint; nextLarger--)
        if(A[nextLarger] > A[breakpoint])
            break;

    swap(A[breakpoint], A[nextLarger]);

    reverse(A.begin() + breakpoint + 1, A.end());
    return A;
}
```
