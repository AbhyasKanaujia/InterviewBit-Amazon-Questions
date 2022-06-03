# ▶ Repeat and Missing Number Array

{% embed url="https://www.interviewbit.com/problems/repeat-and-missing-number-array/" %}

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    long long n = A.size();
    
    long long sumN = n * (n + 1) / 2;
    long long sumN2 = n * (n + 1) * (2 * n + 1) / 6;
    
    long long sumA = 0;
    long long sumA2 = 0;

    for(const int &x: A) {
        sumA2 += x * x;
        sumA += x;
    }

    long long MissingMinusRepeating = sumN - sumA;
    long long Missing2MinusRepeating2 = sumN2 - sumA2;

    long long MissingPlusRepeating = Missing2MinusRepeating2 / MissingMinusRepeating;

    long long twiceMissing = MissingPlusRepeating + MissingMinusRepeating;
    long long twiceRepeating = MissingPlusRepeating - MissingMinusRepeating;

    vector<int> res = {twiceRepeating / 2, twiceMissing / 2};
    return res;
}
```
