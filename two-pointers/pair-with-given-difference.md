# Pair With Given Difference

{% embed url="https://www.interviewbit.com/problems/pair-with-given-difference/" %}

### Using set/map

Same as two sum.&#x20;

```
x - y = 7 => y = x - 7
y - x = 7 => y = x + 7

For each x in A 
    see if we have y using both the equations.
```

```cpp
int Solution::solve(vector<int> &A, int B) {
    unordered_set<int> s;
    for(int x: A) 
        if(s.count(B + x) || s.count(x - B))
            return true;
        else 
            s.insert(x);
    
    return false;
}
```
