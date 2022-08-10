---
cover: >-
  https://images.unsplash.com/photo-1624953856534-babd3e0377b3?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxMHx8bWluaWF0dXJlfGVufDB8fHx8MTY1OTQ0NjE5OQ&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Power Of Two Integers

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
