# ⭐ Min Stack

{% embed url="https://www.youtube.com/watch?v=V09NfaGf2ao" %}

### Using Pair

```cpp

vector<pair<int, int>> stk;

MinStack::MinStack() {
    while(stk.size() > 0)
        stk.pop_back();
}

void MinStack::push(int x) {
    if(stk.size() == 0)
        stk.push_back(make_pair(x, x));
    else
        stk.push_back(make_pair(x, min(stk.back().second, x)));
}

void MinStack::pop() {
    if(stk.size() > 0)
        stk.pop_back();
}

int MinStack::top() {
    return ((stk.size() > 0) ? stk.back().first : -1);
}

int MinStack::getMin() {
    return ((stk.size() > 0) ? stk.back().second : -1);
}
```

Time Complexity: $$O(1)$$​

Space Complexity: $$O(2n)$$​ :point\_left: can be optimized to use $$O(n)$$​
