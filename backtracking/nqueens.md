# ⭐ NQueens

{% embed url="https://www.interviewbit.com/problems/nqueens/" %}

```cpp
vector<vector<string>> res;

bool check(const vector<string> &board, int row, int col, int size) {
    // check horizontally left
    for(int i = 0; i < col; i++)
        if(board[row][i] == 'Q')
            return false;
            
    // check upper left diagonal
    int i = row, j = col;
    while(i >= 0 && j >= 0)
        if(board[i--][j--] =='Q')
            return false;
    
    // check lower left diagonal
    i = row, j = col;
    while(i < size && j >= 0)
        if(board[i++][j--] == 'Q')
            return false;
            
    return true;
}

void getWays(const int &size, vector<string> &board, int col) {
    if(col == size) {
        res.push_back(board);
    }
    for(int row = 0; row < size; row++) 
        if(check(board, row, col, size)) {
            board[row][col] = 'Q';
            getWays(size, board, col + 1);
            board[row][col] = '.';
        }
}

vector<vector<string> > Solution::solveNQueens(int A) {
    res.clear();
    vector<string> board(A, string(A, '.'));
    int col = 0;    
    getWays(A, board, col);
    return res;
}

```
