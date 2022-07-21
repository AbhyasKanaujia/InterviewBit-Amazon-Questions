# ⭐ Valid Sudoku

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

{% embed url="https://www.youtube.com/watch?v=TjFXEUCMqI8" %}

{% tabs %}
{% tab title="C++" %}
```cpp
int Solution::isValidSudoku(const vector<string> &A) {
    map<int, set<int>> rowHas;
    map<int, set<int>> colHas;
    map<int, set<int>> blockHas;
    
    for(int i = 0; i < 9; i++)
        for(int j = 0; j < 9; j++) {
            if(A[i][j] == '.')
                continue;
            
            if(rowHas[i].count(A[i][j]))
                return false;
            else
                rowHas[i].insert(A[i][j]);
                
            if(colHas[j].count(A[i][j]))
                return false;
            else    
                colHas[j].insert(A[i][j]);
                
            int blockRow = i / 3;
            int blockCol = j / 3;
            
            if(blockHas[blockRow * 3 + blockCol].count(A[i][j]))
                return false;
            else 
                blockHas[blockRow * 3 + blockCol].insert(A[i][j]);
        }
        
    return true;
    
}
```

Accepted
{% endtab %}
{% endtabs %}
