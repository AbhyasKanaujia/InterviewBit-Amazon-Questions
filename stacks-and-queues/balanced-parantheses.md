# ✅ Balanced Parantheses!

{% embed url="https://www.interviewbit.com/problems/balanced-parantheses/" %}

```cpp
int Solution::solve(string A) {
    stack<char> s;
    
    for(const char &ch: A) {
        if(ch == '(')
            s.push('(');
        else if(!s.empty())
            s.pop();
        else
            return false;
    }
    
    return s.empty();
}

```
