---
cover: >-
  https://images.unsplash.com/photo-1591696205602-2f950c417cb9?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxpbmNyZWFzZSUyMGRlY3JlYXNlfGVufDB8fHx8MTY1NTEyMjAwOQ&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Find Permutation

{% embed url="https://www.interviewbit.com/problems/find-permutation/" %}

```cpp
vector<int> Solution::findPerm(const string A, int B) {
    int n = A.size();
    vector<int> res(B);

    int ascending = 1;
    int descending = B;
    for(int i = 0; i < n; i++)
        if(A[i] == 'I')
            res[i] = ascending++;
        else
            res[i] = descending--;

    res[n] = (ascending + descending) / 2;

    return res;
}

```

```
A = "IIIIDI"
n = 7
 
OUTPUT = 1 2 3 4 7 5 6

A = "DDDDIDD"
n = 8

Output = 8 7 6 5 1 4 3 2

Simple insert 1 2 3... in all the I's as `ascenings`
and n (n - 1) (n - 2).. in all the D's as `descendings`

In the end push_back the average of the ascending and descending.
```
