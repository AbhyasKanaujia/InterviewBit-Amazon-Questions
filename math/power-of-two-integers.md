# Power Of Two Integers

{% embed url="https://www.interviewbit.com/problems/power-of-two-integers/" %}

### Using log

```cpp
inline bool isInteger(const double &x) {
    return (x - (int)x < 1e-9);
}

int Solution::isPower(int x) {
    if(x == 1)
        return true;

    int low = 2, high = sqrt(x) + 1;

    for(int A = low; A <= high; A++) {
        double P = log(x) / log(A);
        if(P > 1 && isInteger(P))
            return true;
    }

    return false;
}

```
