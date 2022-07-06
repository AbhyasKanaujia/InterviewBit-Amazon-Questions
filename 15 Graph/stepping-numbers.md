# ⭐ Stepping Numbers

{% embed url="https://www.interviewbit.com/problems/stepping-numbers/" %}

```cpp
void exploreAllPath(int value, int &A, int &B, vector<int> &res) {
    // if upper limit crossed then return
    if(value > B) return;
    
    // if within range then store result.
    // Note: no need to check upper limit. 
    // because if it were crossing upper limit the previous 
    // if would have returned
    if(value >= A)
       res.push_back(value);
    
    // get the last digit so that we can append one 
    // more and one less than this to build a valid skipping number
    int lastDigit = value % 10;
    
    // if last digit is not zero 
    // then append one less than last digit
    if(lastDigit != 0)
        exploreAllPath(value * 10 + (lastDigit - 1), A, B, res);
        
    // if last digit is not nine
    // then append one more than the last digit
    if(lastDigit != 9)
        exploreAllPath(value * 10 + (lastDigit + 1), A, B, res);
        
}
vector<int> Solution::stepnum(int A, int B) {
    vector<int> res;
    
    // low is 0 the simply push it into the result 
    // as we are no going to do a 01 02 etc.
    // the main loop starts from minimum 1
    if(A == 0) res.push_back(0);
    
    // Run a loop to choose a first digit from 1 to 9
    // and call exploreAllPath() for that first digit
    for(int i = 1; i <= 9; i++)  
        exploreAllPath(i, A, B, res);
        
    
    // sort the result and return
    sort(res.begin(), res.end());
    return res;
}
```

<details>

<summary>Without Comments</summary>

```cpp
void exploreAllPath(int value, int &A, int &B, vector<int> &res) {
    if(value > B) return;
    
    if(value >= A)
       res.push_back(value);
   
    int lastDigit = value % 10;
    
    if(lastDigit != 0)
        exploreAllPath(value * 10 + (lastDigit - 1), A, B, res);
        
    if(lastDigit != 9)
        exploreAllPath(value * 10 + (lastDigit + 1), A, B, res);
        
}
vector<int> Solution::stepnum(int A, int B) {
    vector<int> res;
    
    if(A == 0) res.push_back(0);
    
    for(int i = 1; i <= 9; i++)  
        exploreAllPath(i, A, B, res);
        
    sort(res.begin(), res.end());
    return res;   
}
```

</details>

Time Complexity: $$O(n)$$​

Space Complexity $$O(n)$$​ for the stack
