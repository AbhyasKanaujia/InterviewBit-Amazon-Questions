# Distinct Numbers in Window

{% embed url="https://www.interviewbit.com/problems/distinct-numbers-in-window/" %}

```cpp
vector<int> Solution::dNums(vector<int> &A, int B) {
    unordered_map<int, int> freq;
    
    for(int i = 0; i < B; i++)
        freq[A[i]]++;
        
    vector<int> res;
    res.push_back(freq.size());
    
    for(int i = B; i < A.size(); i++) {
        int remove = A[i - B];
        int include = A[i];
        
        if(freq[remove] == 1)
            freq.erase(remove);
        else 
            freq[remove]--;
            
        freq[include]++;
        
        res.push_back((int)freq.size());
    }
    
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(window)$$​
