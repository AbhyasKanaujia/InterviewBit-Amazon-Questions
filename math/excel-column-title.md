---
cover: >-
  https://images.unsplash.com/photo-1592431913823-7af6b323da9b?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwzfHxhbHBoYWJldHxlbnwwfHx8fDE2NTk0MjMxMDY&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Excel Column Title

{% embed url="https://www.interviewbit.com/problems/excel-column-title/" %}

```cpp
string Solution::convertToTitle(int A) {
    string res = "";

    while(A) {
        int digit = (A - 1) % 26;
        A = (A - 1) / 26;
        res = (char)(digit + 'A') + res;
    }
    
    return res;
}
```

1. Get each digit as a number from 0 to 25
2. Move that many steps ahead from 'A'
3. Remove that much magnitude
