# Implement StrStr

{% embed url="https://www.interviewbit.com/problems/implement-strstr/" %}

```cpp
bool check(const string &A, const string &B, int pos) {
    int i;
    for(i = 0; i < B.size(); i++) 
        if(pos == A.size() || A[pos++] != B[i])
            return false;
            
    return true;
}

int Solution::strStr(const string A, const string B) {
    for(int i = 0; i < A.size(); i++)
        if(A[i] == B[0] && check(A, B, i))
            return i;
            
    return -1;
}

```
