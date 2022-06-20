# ⭐ atoi

{% embed url="https://www.interviewbit.com/problems/atoi/" %}

```cpp
int Solution::atoi(const string A) {
    // ___A7 -> 0
    // +7 -> 7
    // -7 -> 7
    // 7 A -> 7
    
    // skip spaces
    int begin = 0;
    while(begin < A.size() && A[begin] == ' ')
        begin++;
    
    // first char is special char or alphabet  -> 0
    if(!isdigit(A[begin]) && A[begin] != '+' & A[begin] != '-'  )
        return 0;
    
    // check for sign -> remember sign
    int sign = 1;
    if(A[begin] == '+') {
        sign = 1;
        begin++;
    }
    else if(A[begin] == '-') {
        sign = -1;
        begin++;
    }
        
        
    // at this point begin points to a digit that needs to be converted 
    // until space or alphabet
    
    int res = 0;
    for(int i = begin; i < A.size() && isdigit(A[i]); i++) 
        if((INT_MAX - (A[i] - '0')) / 10 >= res)
            res = res * 10 + A[i] - '0';
        else if(sign == 1)
            return INT_MAX;
        else 
            return INT_MIN;
        
    return res * sign;
}
```
