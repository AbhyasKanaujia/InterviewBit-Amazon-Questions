# Excel Column Title

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
