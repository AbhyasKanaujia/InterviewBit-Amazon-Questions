# Knight On Chess Board

{% embed url="https://www.interviewbit.com/problems/knight-on-chess-board/" %}

## Using BFS

{% hint style="success" %}
Whener you need to find **the shortest path** always use **BFS**. Never DFS.
{% endhint %}

```cpp
// USING 1 INDEXING ALLTOGETHER

// a class knight that stores its position and the number of steps it have moved
// to reach this position. It can generate new knight
// that have moved a valid knight move which might be outside the board 
class Knight {
  public:
    int row;
    int col;
    int moveCount;
    
    // adding these delta to row and col
    // moves them up-down and left-right respectivesly
    int rowDelta[8] = {-2, -2, -1, -1, 1, 1, 2, 2};
    int colDelta[8] = {1, -1, 2, -2, 2, -2, 1, -1};
    
    Knight(int row, int col, int moveCount) {
        this->row = row;
        this->col = col;
        this->moveCount = moveCount;
    }
    
    vector<Knight> getMoves() const{
        vector<Knight> moves;
        
        for(int dir = 0; dir < 8; dir++)
            moves.push_back(
                    Knight(row + rowDelta[dir], 
                            col + colDelta[dir], 
                            this->moveCount + 1
                            ));
            
        return moves;
    }    
    
    bool operator==(const Knight &otherKnight) {
        return this->row == otherKnight.row && this->col == otherKnight.col;
    }
};

// a class board that stores the dimension of the board and can check
// if a knight is inside the board or not. It can also remember what 
// cells of the board have been visited
class Board {
  public:
    int rowCount;
    int colCount;
    
    vector<vector<bool>> placed;
    
    Board(int rowCount, int colCount) {
        this->rowCount = rowCount;
        this->colCount = colCount;
        
        this->placed = 
            vector<vector<bool>>(rowCount + 1, vector<bool>(colCount + 1));
    }
    
    bool isBounded(const Knight &knight) const {
        if(knight.row < 1 || knight.col < 1 || 
                knight.row > rowCount || knight.col > colCount)
            return false;
        return true;
    }  
    
    void markPlaced(const Knight &knight) {
        this->placed[knight.row][knight.col] = true;
    }
    
    void unmarkPlaced(const Knight &knight) {
        this->placed[knight.row][knight.col] = false;
    }
    
    bool isPlaced(const Knight &knight) const {
        return this->placed[knight.row][knight.col];
    }
};

// WHENVER YOU NEED SHORTEST PATH. ALWAYS USE BFS. 
// NEVER DFS

int Solution::knight(int A, int B, int C, int D, int E, int F) {
    Board board(A, B);
    Knight knight(C, D, 0);
    Knight target(E, F, -1);
    
    // a queue for the current knight
    queue<Knight> q;
    // push the initial knight with 0 moves
    q.push(knight);
    // mark as visited
    board.markPlaced(knight);
    
    // until all possible moves have been made
    while(!q.empty()) {
        Knight currentKnight = q.front();
        q.pop();
        
        if(currentKnight == target)
            return currentKnight.moveCount;
            
        for(Knight nextKnight: currentKnight.getMoves()) 
            if(board.isBounded(nextKnight) && !board.isPlaced(nextKnight)) {
                board.markPlaced(nextKnight);
                q.push(nextKnight);
            }
    }
    
    return -1;
}

```
