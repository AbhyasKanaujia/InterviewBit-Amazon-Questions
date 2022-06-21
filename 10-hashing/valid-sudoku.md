# Valid Sudoku

{% embed url="https://www.interviewbit.com/problems/valid-sudoku/" %}

{% tabs %}
{% tab title="C++" %}
```cpp
int Solution::isValidSudoku(const vector<string> &A) {
    
    // check each row and col;
    for(int i = 0; i < 9; i++) {
        map<int, int> rowFreq, colFreq;
        for(int j = 0; j < 9; j++) {
            if(A[i][j] != '.' && ++rowFreq[A[i][j]] > 1) 
                return false;
            if(A[j][i] != '.' && ++colFreq[A[j][i]] > 1)
                return false;
        }
    }
    
    for(int blockRow = 0; blockRow < 9; blockRow += 3) 
        for(int blockCol = 0; blockCol < 9; blockCol += 3) {
            map<int, int> blockFreq;
            for(int i = 0; i < 3 ; i++)
                for(int j = 0; j < 3; j++)
                    if(A[blockRow + i][blockCol + j] != '.' && ++blockFreq[A[blockRow + i][blockCol + j]] > 1)
                        return false;
        }
        
    return true;
}
```

Accepted
{% endtab %}
{% endtabs %}
