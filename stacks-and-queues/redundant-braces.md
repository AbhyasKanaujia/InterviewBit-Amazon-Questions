# Redundant Braces

{% embed url="https://www.interviewbit.com/problems/redundant-braces/" %}

{% embed url="https://youtu.be/azYOlJh9z8U" %}

```cpp
int Solution::braces(string A) {
    stack<char> s;
    
    
    for(char ch: A) {
        if(ch == '(' || ch == '+' || ch == '-' || ch == '*' || ch == '/')
            s.push(ch);
        else if(ch == ')' && !s.empty() && s.top() == '(') 
            return true;
        else if(ch == ')') {
            while(!s.empty() && s.top() != '(')
                s.pop();
            s.pop();
        }
    }
    return false;
}

```
