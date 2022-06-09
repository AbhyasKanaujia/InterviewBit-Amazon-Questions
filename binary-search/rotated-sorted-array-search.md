# ⭐ Rotated Sorted Array Search

{% embed url="https://www.interviewbit.com/problems/rotated-sorted-array-search/" %}

```cpp
int getPivot(const vector<int> &A) {
    int low = 0, high = A.size() - 1;
    int ans = A.size() - 1;

    while(low < high) {
        int mid = low + ((high - low) >> 1);
        if(A[mid] > A[0])
            low = mid + 1;
        else {
            ans = mid;
            high = mid;
        }
    }
    return ans;
}

int binarySearch(const vector<int> &A, int low, int high, int x) {
    int res = -1;
    while(low <= high) {
        int mid = low + ((high - low) >> 1);
        if(A[mid] < x) 
            low = mid + 1;
        else if(A[mid] > x) 
            high = mid - 1;
        else {
            res = mid;
            break;
        }
    }
    return res;
}

int Solution::search(const vector<int> &A, int B) {
    int pivot = getPivot(A);
    int res = -1;
    if(pivot == A.size() - 1)
        res = binarySearch(A, 0, A.size() - 1, B);
    else if(B >= A[0] && B <= A[pivot - 1])
        res = binarySearch(A, 0, pivot - 1, B);
    else if(B >= A[pivot] && B <= A[A.size() - 1])
        res = binarySearch(A, pivot, A.size() - 1, B);
    
    return res;
}
```

