# Median of Array

{% embed url="https://www.interviewbit.com/problems/median-of-array/" %}

### Naive Solution

```cpp
double Solution::findMedianSortedArrays(const vector<int> &A, const vector<int> &B) {
    vector<int> merged;

    int i = 0, j = 0;
    while(i < A.size() && j < B.size())
        if(A[i] <= B[j])
            merged.push_back(A[i++]);
        else    
            merged.push_back(B[j++]);

    if( i < A.size())
        merged.push_back(A[i++]);

    if(j < B.size())
        merged.push_back(B[j++]);

    int n = merged.size();

    if(n == 1)
        return merged[0];

    if(n & 1)
        return merged[n / 2];
    else 
        return (merged[n / 2] + merged[n / 2 - 1]) / 2.0;
}

```

Time Complexity: $$O(m + n)$$​

Space Complexity: $$O(m + n)$$

### Using Binary Search

{% embed url="https://www.youtube.com/watch?v=NTop3VTjmxk" %}

```cpp
double Solution::findMedianSortedArrays(const vector<int> &A, const vector<int> &B) {
    if(B.size() < A.size()) return findMedianSortedArrays(B, A);

    int n1 = A.size();
    int n2 = B.size();
    int low = 0, high = n1;

    while(low <= high) {
        int cut1 = (low + high) >> 1;
        int cut2 = (n1 + n2 + 1) / 2 - cut1;

        int left1 = cut1 == 0 ? INT_MIN : A[cut1 - 1];
        int left2 = cut2 == 0 ? INT_MIN : B[cut2 - 1];

        int right1 = cut1 == n1 ? INT_MAX : A[cut1];
        int right2 = cut2 == n2 ? INT_MAX : B[cut2];

        if(left1 <= right2 && left2 <= right1) {
            if((n1 + n2) % 2 == 0)
                return (max(left1, left2) + min(right1, right2)) / 2.0;
            else
            return 
                max(left1, left2);
        } 
        else if(left1 > right2)
            high = cut1 - 1;
        else    
            low = cut1 + 1;
    }
    return 0.0;    
}
```

