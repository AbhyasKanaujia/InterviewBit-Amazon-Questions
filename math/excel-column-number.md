# Excel Column Number

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
