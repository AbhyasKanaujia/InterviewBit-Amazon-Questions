# ✅ Set Matrix Zeros

{% embed url="https://www.interviewbit.com/problems/set-matrix-zeros/" %}

{% tabs %}
{% tab title="First Tab" %}
```cpp
void Solution::setZeroes(vector<vector<int> > &A) {
    // storage to remember which rows and cols will be zeroed.
    vector<bool> zeroRow(A.size());
    vector<bool> zeroCol(A[0].size());

    // storing rows and cols that need to be zeroed without modifying the array
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            if(A[i][j] == 0) 
                zeroRow[i] = zeroCol[j] = true;

    // using zeroRow and zeroCol to actaully mark each element
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            if(zeroRow[i] || zeroCol[j])
                A[i][j] = 0;
            
}
```
{% endtab %}

{% tab title="Second Tab" %}
```javascript
module.exports = {
    /**
     * param A: list of list of integers
     * @return the same list modified
     */
    solve: function (A) {
        let row = new Array(A.length), col = new Array(A.length).fill(false)
        
        for(let i = 0; i < A.length; i++)
            for(let j = 0; j < A[0].length; j++)
                if(!A[i][j]) {
                    row[i] = true;
                    col[j] = true;
                }
                
        for(let i = 0; i < A.length; i++)
            for(let j = 0; j < A[0].length; j++)
                if(row[i] || col[j])
                    A[i][j] = 0;
                    
        return A;
    },    
};
```
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(m+n)$$
