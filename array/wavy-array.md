# Wavy Array

{% embed url="https://www.interviewbit.com/problems/wave-array/" %}

### Using Sorting (Most Optimal)

```cpp
vector<int> Solution::wave(vector<int> &A) {
    sort(A.begin(), A.end());
    for(int i = 0; i + 1 < A.size(); i += 2) 
        swap(A[i], A[i + 1]);

    return A;
}
```

Time Complexity: $$O(n \log n)$$​

Space Complexity: $$O(1)$$​
