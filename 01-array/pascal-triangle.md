---
cover: >-
  https://images.unsplash.com/photo-1523457506542-088cbc0b4540?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw0fHxwYXNjYWwlMjB0cmlhbmdsZXxlbnwwfHx8fDE2NTUxMTQ5Mjc&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Pascal Triangle

{% embed url="https://www.interviewbit.com/problems/pascal-triangle/" %}

### Using ^nC\_r

<details>

<summary>Code</summary>

```cpp
int nCr(int n, int r) {
    if(n == 0 || r == 0 || n == r)
        return 1;

    r = min(r, n - r);

    int res = 1;
    for(int i = 1; i <= r; i++) 
        res = res * (n - i + 1) / i;
    
    return res;
}
vector<vector<int> > Solution::solve(int A) {
    vector<vector<int>> res;
    for(int i = 0; i < A; i++) {
        res.push_back(vector<int>(i + 1));
        for(int j = 0; j <= i; j++)
            res[i][j] = nCr(i, j);
    }

    return res;
}
```

</details>

Time Complexity: $$O(n^3)$$​

Space Complexity: $$O(n^2)$$​ for the result

{% embed url="https://theconversation.com/the-12-days-of-pascals-triangular-christmas-21479" %}
Very interesting article on pascal's trignale
{% endembed %}
