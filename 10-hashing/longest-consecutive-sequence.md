# ⭐ Longest Consecutive Sequence

{% embed url="https://www.interviewbit.com/problems/longest-consecutive-sequence/" %}

## Using Sorting

```cpp
int Solution::longestConsecutive(const vector<int> &A) {
    set<int> s(A.begin(), A.end());
    vector<int> copy(s.begin(), s.end());
    int begin = 0;
    int res = min((int) A.size() , 1);
    for(int i = 1; i < copy.size(); i++) {
        if(copy[i] == copy[i - 1] + 1)
            res = max(res, i - begin + 1);
        else 
            begin = i;
    }
    
    return res;
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(2n)$$

## Using set

{% embed url="https://www.youtube.com/watch?v=qgizvmgeyUM" %}

```cpp
unordered_set<int> s;

int Solution::longestConsecutive(const vector<int> &A) {
    int res = INT_MIN;
    
    s.clear();
    for(const int &x: A)
        s.insert(x);
        
    for(const int &x: A) 
        if(!s.count(x - 1)) { // is it the fisrt elmement of its consecutive sereis?
            int count = 1; 
            while(s.count(x + count)) // does the next element exists?
                count++;
                
            res = max(res, count);        
        }
    
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
