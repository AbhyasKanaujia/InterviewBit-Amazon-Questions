# Spiral Order Matrix I

{% embed url="https://www.interviewbit.com/problems/spiral-order-matrix-i/" %}

```cpp
vector<int> Solution::spiralOrder(const vector<vector<int> > &A) {
    int minRow = 0, minCol = 0;
    int maxRow = A.size() - 1, maxCol = A[0].size() - 1;

    vector<int> res;

    int total = A.size() * A[0].size();

    while(total) {
        // top row
        for(int col = minCol; col <= maxCol && total; col++) {
            res.push_back(A[minRow][col]);
            total--;
        }
        minRow++;

        // right col
        for(int row = minRow; row <= maxRow && total; row++) {
            res.push_back(A[row][maxCol]);
            total--;
        }
        maxCol--;

        // bottom row
        for(int col = maxCol; col >= minCol && total; col--) {
            res.push_back(A[maxRow][col]);
            total--;
        }
        maxRow--;

        // left col
        for(int row = maxRow; row >= minRow && total; row--) {
            res.push_back(A[row][minCol]);
            total--;
        }
        minCol++;
    }
    return res;
}
```
