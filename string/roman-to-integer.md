# ⭐ Roman to Integer

{% embed url="https://www.interviewbit.com/problems/roman-to-integer/" %}

```cpp
int Solution::romanToInt(string A) {
    unordered_map<char, int> value = { 
        {'I', 1}, {'V', 5}, {'X', 10}, {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
    };
    
    int res = 0;
    
    for(int i = 0; i + 1 < A.size(); i++)
        if(value[A[i]] < value[A[i + 1]])
            res -= value[A[i]];
        else
            res += value[A[i]];
            
    res += value[A[A.size() - 1]];
    
    return res;
}
```
