# Spiral Order Matrix II

{% embed url="https://www.interviewbit.com/problems/spiral-order-matrix-ii/" %}

```cpp
vector<vector<int> > Solution::generateMatrix(int A) {
    vector<vector<int>> res(A, vector<int>(A));

    int minRow = 0, minCol = 0;
    int maxRow = A - 1, maxCol = A - 1;

    int value = 1;
    while(value <= A * A) {
        // top row
        for(int col = minCol; col <= maxCol && value <= A * A; col++) 
            res[minRow][col] = value++;

        minRow++;
        
        // right col
        for(int row = minRow; row <= maxRow && value <= A * A; row++) 
            res[row][maxCol] = value++;

        maxCol--;

        // bottom row
        for(int col = maxCol; col >= minCol && value <= A * A; col--)
            res[maxRow][col] = value++;

        maxRow--;

        // left col
        for(int row = maxRow; row >= minRow && value <= A * A; row--)
            res[row][minCol] = value++;

        minCol++;
    }
    return res;
}

```
