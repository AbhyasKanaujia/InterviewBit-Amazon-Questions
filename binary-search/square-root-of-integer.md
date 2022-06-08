# ⭐ Square Root of Integer

{% embed url="https://www.interviewbit.com/search/?q=Amazon" %}

```cpp
int Solution::sqrt(int A) {
    if(A == 0) return 0;

    int low = 1, high = A, res;

    while(low <= high) {
        int mid = low + ((high - low) >> 1);
        if(mid <= A / mid) {
            low = mid + 1;
            res = mid;
        } else 
            high = mid - 1;
    }
    return res;
}
```

Time Complexity: $$O(\log n)$$​

Space Complexity: $$O(1)$$​

Edge case: $$A = 0$$​
