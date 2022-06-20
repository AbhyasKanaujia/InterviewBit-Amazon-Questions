---
cover: >-
  https://images.unsplash.com/photo-1581451932564-cff1d8f4cacc?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHx3YXZ5fGVufDB8fHx8MTY1NTExNDgwOA&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ✅ Wavy Array



{% embed url="https://www.interviewbit.com/problems/wave-array/" %}
Given an array of integers, sort the array into a wave-like array and return it,\
In other words, arrange the elements into a sequence such that `a1 >= a2 <= a3 >= a4 <= a5.....`
{% endembed %}

### Using Sorting and Swap Alternate (Most Optimal)

```cpp
vector<int> Solution::wave(vector<int> &A) {
    sort(A.begin(), A.end());
    for(int i = 0; i + 1 < A.size(); i += 2) 
        swap(A[i], A[i + 1]);

    return A;
}
```

Time Complexity: $$O(n \log n)$$​

Space Complexity: $$O(1)$$​
