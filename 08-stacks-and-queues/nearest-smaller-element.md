# Nearest Smaller Element

{% embed url="https://www.interviewbit.com/problems/nearest-smaller-element/" %}

## Using Stack

```cpp
vector<int> Solution::prevSmaller(vector<int> &A) {
    stack<int> s;
    vector<int> res;
    
    for(const int &x: A) {
        while(!s.empty() && s.top() >= x) 
            s.pop();
            
        res.push_back(s.empty() ? -1 : s.top());
        s.push(x);
    }
    return res;
}
```

Time Complexity: $$O(n)$$

Space Complexity: $$O(1)$$​
