---
cover: >-
  https://images.unsplash.com/photo-1573694279179-764ff2597b5b?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxwZXJtdXRhdGlvbnxlbnwwfHx8fDE2NTUxMTQ3OTE&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Next Permutation

{% embed url="https://www.interviewbit.com/problems/next-permutation/" %}

```cpp
vector<int> Solution::nextPermutation(vector<int> &A) {
    int breakpoint;
    int n = A.size();
    for(breakpoint = n - 2; breakpoint >= 0; breakpoint--)
        if(A[breakpoint] < A[breakpoint + 1])
            break;

    if(breakpoint == -1) {
        reverse(A.begin(), A.end());
        return A;
    }

    int justLarger;
    for(justLarger = n - 1; justLarger > breakpoint; justLarger--)
        if(A[justLarger] > A[breakpoint])
            break;

    swap(A[breakpoint], A[justLarger]);

    reverse(A.begin() + breakpoint + 1, A.end());
    return A;
}
```

### Explanation

```cpp
int breakpoint;
int n = A.size();
for(breakpoint = n - 2; breakpoint >= 0; breakpoint--)
    if(A[breakpoint] < A[breakpoint + 1])
        break;
```

$$1\, 2\, 3\, 6\, 5\, 4$$

The **Breakpoint** is used to ​find the position of the element where the digits dip down after being ascending for a while from right to left

In this example, digits from right to left keep increasing from 4 -> 5 -> 6. Then it dips down at 3.

```cpp
if(breakpoint == -1) {
    reverse(A.begin(), A.end());
    return A;
}
```

If there is no such tipping point, the number is entirely made of descending digits and there is no next permutation. So the result is the reverse of that number. Example $$987654$$.

```cpp
int justLarger;
for(justLarger = n - 1; justLarger > breakpoint; justLarger--)
    if(A[justLarger] > A[breakpoint])
        break;
```

Find the digit that is just larger than the tipping point.&#x20;

Since the digits on the right are in ascending order, we can just traverse it from right to left. As soon as we find a value that is larger that the breakpoint we can be sure that this is the digit that is just larger than the breakpoint.&#x20;

Any digit on its left is too large and on its right is too small.&#x20;

```cpp
swap(A[breakpoint], A[justLarger]);
```

Swap the breakpoint and the just larger element

```cpp
reverse(A.begin() + breakpoint + 1, A.end());
```

Make the digits after the breakpoint ascending.

Time Complexity: $$O(n)$$

Space Complexity: $$O(1)$$​
