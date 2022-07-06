# Black Shapes

{% embed url="https://www.interviewbit.com/problems/black-shapes/" %}

## Using BFS

### Using `Pair<int, int>`

```cpp
// adding these deltas to i and j 
// moves them up-down and left-right respectively.
int xDelta[4] = {0, 0, -1, 1};
int yDelta[4] = {-1, 1 , 0, 0};

class Coordinate {
  public:
    int i;
    int j;
    
    Coordinate(int i, int j) {
        this->i = i;
        this->j = j;
    }
};

// checks if (i, j) is a valid index for the matrix A
bool isBounded(int i, int j, vector<string> &A) {
    if(i < 0 || j < 0 || i >= A.size() || j >= A[0].size())
        return false;
    return true;
}

int Solution::black(vector<string> &A) {
    // Step 1: untill each cell have been traversed, find an X
    // Step 2: increment the count of shapes
    // Step 3: remove all adjacent Xs
    // Step 4: go to step 1
    
    // set count initially to 0
    int count = 0;
    
    // travese each cell
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            // if the cell is  an X
            if(A[i][j] == 'X') {
                // increment the count since an unvisited bunch of X is here
                count++;
                
                // create a queue of pair of (i, j)
                queue<Coordinate> q;
                
                // insert current cell containing X
                q.push(Coordinate(i, j));
                A[i][j] = 'O';
                
                // untill all Xs have been removed
                while(!q.empty()) {
                    // current size of queue
                    int size = q.size();
                    // process all the elements currently in queue
                    for(int i = 1; i <= size; i++) {
                        // get front cell
                        Coordinate frontCell = q.front();
                        // remove it fron the queue
                        q.pop();                        
                                                
                        // use xDelta and yDelta to get all 4 neighbours
                        for(int dir = 0; dir < 4; dir++) {
                            
                            int nextI = frontCell.i + xDelta[dir];
                            int nextJ = frontCell.j + yDelta[dir];
                            
                            // check if neighbour index are in bounds
                            // and that they contain X
                            if(isBounded(nextI, nextJ, A) && A[nextI][nextJ] == 'X')  {
                                
                                // if so then push them into the queue for having its neighbours checked
                                q.push(Coordinate(nextI, nextJ));    
                                
                                // PROCESSING: 
                                // remove X and replace with O
                                A[nextI][nextJ] = 'O';
                            }
                        }
                        
                    }
                }
            }
    
    // return the count
    return count;
    
}
```

### Using Coordinate Class

```cpp
class Coordinate {
  public:
    int i;
    int j;
    
    Coordinate(int i, int j) {
        this->i = i;
        this->j = j;
    }
    
    // checks if (i, j) is a valid index for the matrix A
    bool isBounded(vector<string> &A) {
        if(i < 0 || j < 0 || i >= A.size() || j >= A[0].size())
            return false;
        return true;
    }
    
    // get neighbours of i, j
    vector<Coordinate> getNeighbours() {
        // adding these deltas to i and j 
        // moves them up-down and left-right respectively.
        int xDelta[4] = {0, 0, -1, 1};
        int yDelta[4] = {-1, 1 , 0, 0};
        
        // Resulting neighbours contains four negihbours in four directions
        vector<Coordinate> neighbours;
        
        // loop to get delta
        for(int dir = 0; dir < 4; dir++) 
            // craete a neighbour using delta and 
            // push it into result
            neighbours.push_back(Coordinate(i + xDelta[dir], j + yDelta[dir]));
        
        return neighbours;
    }
};

int Solution::black(vector<string> &A) {
    // Step 1: untill each cell have been traversed, find an X
    // Step 2: increment the count of shapes
    // Step 3: remove all adjacent Xs
    // Step 4: go to step 1
    
    // set count initially to 0
    int count = 0;
    
    // travese each cell
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            // if the cell is  an X
            if(A[i][j] == 'X') {
                // increment the count since an unvisited bunch of X is here
                count++;
                
                // create a queue of pair of (i, j)
                queue<Coordinate> q;
                
                // insert current cell containing X
                q.push(Coordinate(i, j));
                A[i][j] = 'O';
                
                // untill all Xs have been removed
                while(!q.empty()) {
                    // current size of queue
                    int size = q.size();
                    // process all the elements currently in queue
                    for(int i = 1; i <= size; i++) {
                        // get front cell
                        Coordinate frontCell = q.front();
                        // remove it fron the queue
                        q.pop();                        
                            
                        // get neighbours and process them            
                        for(Coordinate neighbour: frontCell.getNeighbours()) {
                            // check if neighbour is bounded and contain X
                            if(neighbour.isBounded(A) && A[neighbour.i][neighbour.j] == 'X') {
                                // if so then push it into the queue for having its neighbours processed
                                q.push(neighbour);
                                
                                // PROCESSING:
                                // Replace X with O
                                A[neighbour.i][neighbour.j] = 'O';                                
                            }
                        }   
                    }
                }
            }
    
    // return the count
    return count;    
}
```

<details>

<summary>Without Comments</summary>

```cpp
class Coordinate {
  public:
    int i;
    int j;
    
    Coordinate(int i, int j) {
        this->i = i;
        this->j = j;
    }
    
    bool isBounded(vector<string> &A) {
        if(i < 0 || j < 0 || i >= A.size() || j >= A[0].size())
            return false;
        return true;
    }
    
    vector<Coordinate> getNeighbours() {
        int xDelta[4] = {0, 0, -1, 1};
        int yDelta[4] = {-1, 1 , 0, 0};
        
        vector<Coordinate> neighbours;
        
        for(int dir = 0; dir < 4; dir++) 
            neighbours.push_back(
                        Coordinate(i + xDelta[dir], j + yDelta[dir])
                                );
        
        return neighbours;
    }
};

int Solution::black(vector<string> &A) {
    int count = 0;
    
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            if(A[i][j] == 'X') {
                count++;
                
                queue<Coordinate> q;
                
                q.push(Coordinate(i, j));
                A[i][j] = 'O';
                
                while(!q.empty()) {
                    int size = q.size();
                    for(int i = 1; i <= size; i++) {
                        Coordinate frontCell = q.front();
                        q.pop();                        
                            
                        for(Coordinate neighbour: frontCell.getNeighbours()) {
                            if(neighbour.isBounded(A) 
                                    && A[neighbour.i][neighbour.j] == 'X') {
                                q.push(neighbour);
                                
                                A[neighbour.i][neighbour.j] = 'O';                                
                            }
                        }   
                    }
                }
            }
    
    return count;
    
}
```

</details>
