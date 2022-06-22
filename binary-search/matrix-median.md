# ⭐ Matrix Median

{% embed url="https://www.interviewbit.com/problems/matrix-median/" %}

### Naive Approach: Extract into Linear Array and Sort&#x20;

```cpp
int Solution::findMedian(vector<vector<int> > &A) {
    vector<int> linear;
    for(const vector<int> &row: A)
        for(const int &x: row)
            linear.push_back(x);

    sort(linear.begin(), linear.end());

    int n = linear.size();

    if(n & 1)
        return linear[n / 2];
    else 
        return (linear[n / 2 - 1] + linear[n / 2]) / 2;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

### Using Binary Search

{% embed url="https://www.youtube.com/watch?v=63fPPOdIr2c" %}

```cpp
int countSmallerThanMid(const vector<int> &row, int mid) {
    int l = 0, h = row.size() - 1;
    while(l <= h) {
        int md = (l + h) >> 1;
        if(row[md] <= mid) {
            l = md + 1;
        } else {
            h = md - 1;
        }
    }
    return l; 
}
int Solution::findMedian(vector<vector<int> > &A) {
    int low = 1;
    int high = 1e9;
    int n = A.size();
    int m = A[0].size();

    while(low <= high) {
        int mid = low + ((high - low) >> 1);
        int count = 0;
        for(int i = 0; i < n; i++) 
            count += countSmallerThanMid(A[i], mid);

        if(count <= (n * m) / 2) 
            low = mid + 1;
        else 
            high = mid - 1;
    }

    return low;
}
```

Time Complexity: $$O(\log n)$$​

Space Complexity: $$O(1)$$​
