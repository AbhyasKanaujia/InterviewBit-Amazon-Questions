# Spiral Order Matrix I

{% embed url="https://www.interviewbit.com/problems/spiral-order-matrix-i/" %}

{% tabs %}
{% tab title="C++" %}
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
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
 //param A : array of array of integers
 //return a array of integers
	spiralOrder : function(A){
        let m = A.length, n = A[0].length
        let minRow = 0, maxRow = m - 1
        let minCol = 0, maxCol = n - 1
        
        let count = m * n
        
        let res = []
        
        while(count) {
            for(let col = minCol; count &&  col <= maxCol; col++) {
                res.push(A[minRow][col])
                count--
            }
            minRow++
            
            
            for(let row = minRow; count &&  row <= maxRow; row++) {
                res.push(A[row][maxCol])
                count--
            }
            maxCol--
            
            
            for(let col = vector<int> Solution::spiralOrder(const vector<vector<int> > &A) {
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
}maxCol; count &&  col >= minCol; col--) {
                res.push(A[maxRow][col])
                count--
            }
            maxRow--
            
            
            for(let row = maxRow; count &&  row >= minRow; row--) {
                res.push(A[row][minCol])
                count--
            }
            minCol++
        }
        
        return res
	}
};

```
{% endtab %}
{% endtabs %}

Time Complexity: $$O(mn)$$

Space Complexity: $$O(n)$$​
