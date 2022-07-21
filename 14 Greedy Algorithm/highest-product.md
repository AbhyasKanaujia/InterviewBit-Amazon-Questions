# ⭐ Highest Product

{% embed url="https://www.interviewbit.com/problems/highest-product/" %}

```cpp
int Solution::maxp3(vector<int> &A) {
    sort(A.begin(), A.end());
    int n = A.size();
    int choice1 = A[n - 1] * A[n - 2] * A[n - 3];
    int choice2 = A[0] * A[1] * A[n - 1];
    
    return max(choice1,choice2);
}
```

{% embed url="https://www.youtube.com/watch?v=fQF7tAmMKHE" %}
