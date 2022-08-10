---
cover: >-
  https://images.unsplash.com/photo-1460925895917-afdab827c52f?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxleGNlbHxlbnwwfHx8fDE2NTk0MjE2OTY&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ✅ Excel Column Number

{% embed url="https://www.interviewbit.com/problems/excel-column-number/" %}

```cpp
int Solution::titleToNumber(string A) {
    int res = 0;

    for(int i = 0; i < A.size(); i++) {
        char ch = A[A.size() - 1 - i];
        int magniute = ch - 'A' + 1;
        res += magniute * pow(26, i);
    }

    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
