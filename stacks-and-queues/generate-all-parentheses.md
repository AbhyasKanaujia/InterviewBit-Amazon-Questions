# Generate all Parentheses

{% embed url="https://www.interviewbit.com/problems/generate-all-parentheses/" %}

```cpp
int Solution::isValid(string A) {
    map<char, char> openingFor = {{')', '('} , {'}', '{'}, {']', '['}};
    stack<char> brackets;
    
    for(char ch: A) {
        bool isOpen = !openingFor.count(ch);
        
        if(isOpen) 
            brackets.push(ch);
        else {
            if(brackets.empty() || brackets.top() != openingFor[ch])
                return false;
            else
                brackets.pop();
        }
        
    }
    
    return brackets.empty();
}

```
