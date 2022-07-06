# Word Search Board

{% embed url="https://www.interviewbit.com/problems/word-search-board/" %}

```cpp
// in a 2D matrix where i signifies row and j signifies column
// xDelta moves i up and down
// yDelta moves j left and right
int xDelta[] = {0, 0, -1, 1};
int yDelta[] = {-1, 1, 0, 0};

/**
* @brief checks if i and j is bounded within row count and col count when
* moving in the dir direction using xDelta and yDelta
*
* @return true bounded
* @return fale out of bounds
*/
bool isBounded(int i, int j, int dir, int rowCount, int colCount) {
    i += xDelta[dir];
    j += yDelta[dir];
    
    if(i < 0 || j < 0 || i >= rowCount || j >= colCount)
        return false;
    return true;
}

/**
* @brief each iteration checks if the character at index \p index in the string \p B
* is present at (\p i, \p j) or not. 
* If not return false
* If present search the next index in all four directions.
* If all chars searched then return true
* 
* @return false not present starting at (i, j)
* @return true if the word was found string from (i, j). 
*
*/
bool search(vector<string> &A, int i, int j, string &B, int index) {
    // Since string is 0 indexed, an attempt to search the nth character 
    // means that all the previous characters were found.
    // i.e. the word search has successfully completed. return true.
    if(index == B.size())
        return true;
        
    // if(i, j) th character is not B[index] then there is no match. return false
    if(A[i][j] != B[index])
        return false;        
    
    // flag that assumes that search will fail
    bool found = false;
    // combine xDelta and yDelta to current i, j and attempt to move in 4 directions
    for(int dir = 0; dir < 4; dir++) 
        // make sure the search is being done in bound
        if(isBounded(i, j, dir, A.size(), A[0].size()))
            if(search(A, i + xDelta[dir], j + yDelta[dir], B, index + 1)) 
                // if found then change flag and don't search further
                return true;
            
    return false;
}

int Solution::exist(vector<string> &A, string B) {
    // points at the character that is being matched
    int index = 0;
    // find this in matrix to look for the starting point of search
    int firstLetter = B[index];
    // check each character of the given grid to find a potential starting point i.e. char == first letter
    // search for the word from this point on. If found return true.
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            if(A[i][j] == firstLetter && search(A, i, j, B, index))
                return true;
                
    // if after trying out every possible starting point and attempting to find the word
    // it was still not found then it is not there. Return false.
    return false;
}

```

<details>

<summary>Without Comments</summary>

```cpp
int xDelta[] = {0, 0, -1, 1};
int yDelta[] = {-1, 1, 0, 0};

bool isBounded(int i, int j, int dir, int rowCount, int colCount) {
    i += xDelta[dir];
    j += yDelta[dir];
    
    if(i < 0 || j < 0 || i >= rowCount || j >= colCount)
        return false;
    return true;
}

bool search(vector<string> &A, int i, int j, string &B, int index) {
    if(index == B.size())
        return true;
        
    if(A[i][j] != B[index])
        return false;        
    
    bool found = false;
    for(int dir = 0; dir < 4; dir++) 
        if(isBounded(i, j, dir, A.size(), A[0].size()))
            if(search(A, i + xDelta[dir], j + yDelta[dir], B, index + 1)) 
                return true;
            
    return false;
}

int Solution::exist(vector<string> &A, string B) {
    int index = 0;
    int firstLetter = B[index];
    for(int i = 0; i < A.size(); i++)
        for(int j = 0; j < A[0].size(); j++)
            if(A[i][j] == firstLetter && search(A, i, j, B, index))
                return true;
                
    return false;
}
```

</details>
