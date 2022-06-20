# ✅ Rotate Matrix

{% embed url="https://www.interviewbit.com/problems/rotate-matrix/" %}

```cpp
void Solution::rotate(vector<vector<int> > &A) {
    for(int i = 0; i < A.size(); i++) 
        for(int j = i + 1; j < A[0].size(); j++)
            swap(A[i][j], A[j][i]);

    int col1 = 0, col2 = A[0].size() - 1;
    while(col1 <= col2) {
        for(int i = 0; i < A.size(); i++) 
            swap(A[i][col1], A[i][col2]);
        col1++;
        col2--;
    }
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
