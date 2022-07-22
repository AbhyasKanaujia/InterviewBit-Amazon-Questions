# ⭐ Inversions

{% embed url="https://www.interviewbit.com/problems/inversions/" %}

## Brute Force

```cpp
int Solution::countInversions(vector<int> &A) {
    int count = 0;
    for(int i = 0; i < A.size(); i++)
        for(int j = i + 1; j < A.size(); j++)
            count += A[i] > A[j];
            
    return count;
}
```

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(1)$$

## Using Merge Sort

```cpp
int res = 0;

void merge(vector<int> &A, int low, int mid, int high) {
    vector<int> left, right;
    
    for(int i = low; i <= mid; i++)
        left.push_back(A[i]);
    for(int j = mid + 1; j <= high; j++)
        right.push_back(A[j]);
        
    int i = 0, j = 0;
    
    int k = low;
    while(i < left.size() && j < right.size()) {
        if(left[i] <= right[j]) 
            A[k++] = left[i++];
        else {
            res += left.size() - i;
            A[k++] = right[j++];
        }
    }
    
    while(i < left.size()) 
        A[k++] = left[i++];
        
    while(j < right.size())
        A[k++] = right[j++];
}

void mergeSort(vector<int> &A, int low, int high) {
    if(low < high) {
        int mid = low + ((high - low) >> 1);
        
        mergeSort(A, low, mid);
        mergeSort(A, mid + 1, high);
        
        merge(A, low, mid, high);
    }
}
int Solution::countInversions(vector<int> &A) {
    res = 0;
    mergeSort(A, 0, A.size() - 1);
    return res;
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(n)$$​
