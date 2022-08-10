---
cover: >-
  https://images.unsplash.com/photo-1536693419517-38712b94e24f?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxfHxzY3JhbWJsZWR8ZW58MHx8fHwxNjU5MzgwOTg4&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Maximum Unsorted Subarray

{% embed url="https://www.interviewbit.com/problems/maximum-unsorted-subarray/" %}



Given an array, **A** of non-negative integers of size **N**. Find the minimum sub-array **Al, Al+1 ,..., Ar** such that if we sort(in ascending order) that sub-array, then the whole array should get sorted. If **A** is already sorted, output **-1**.\
\
**Problem Constraints**

1 <= N <= 1000000\
1 <= A\[i] <= 1000000\
\
**Input Format**

The first and only argument is an array of non-negative integers of size N.\
\
**Output Format**

Return an array of length two where the first element denotes the starting index(0-based) and the second element denotes the ending index(0-based) of the sub-array. If the array is already sorted, return an array containing only one element i.e. -1.\
\
**Example Input**

Input 1:

```
A = [1, 3, 2, 4, 5]
```

Input 2:

```
A = [1, 2, 3, 4, 5]
```

**Example Output**

Output 1:

```
[1, 2]
```

Output 2:

```
[-1]
```

**Example Explanation**

Explanation 1:

```
If we sort the sub-array A1, A2, then the whole array A gets sorted.
```

Explanation 2:

```
A is already sorted.
```

### Solution

```cpp
vector<int> Solution::subUnsort(vector<int> &A) {
    int n = A.size();
    vector<int> maxLeft(n);
    vector<int> minRight(n);

    maxLeft[0] = A[0];
    minRight[n - 1] = A[n - 1];

    for(int i = 1; i < n; i++)
        maxLeft[i] = max(maxLeft[i - 1], A[i]);

    for(int i = n - 2; i >= 0; i--)
        minRight[i] = min(minRight[i + 1], A[i]);

    vector<int> res;
    int right = n;
    for(int i = 0; i < n; i++)
        if(maxLeft[i] != minRight[i]) {
            res.push_back(i);
            break;
        }

    if(res.empty()) {
        res.push_back(-1);
        return res;
    }

    for(int i = n - 1; i >= 0; i--) 
        if(maxLeft[i] != minRight[i]) {
            res.push_back(i);
            break;
        }

    return res;
}

```

```
For Array 1 3 2 4 5
minLeft = 1 1 1 1 1
maxLeft = 1 3 3 4 5
minRight= 1 2 2 4 5
maxRight= 5 5 5 5 5
```

Apparently, `maxRight` and `minLeft` is useless.&#x20;

Whatever matches between `maxLeft` and `minRight` is what is properly sorted.&#x20;

What doesn't match is what needs to be sorted.

If the array were already soretd:

```
For Array  1 2 3 4 5
maxLeft  = 1 2 3 4 5
minRight = 1 2 3 4 5  
```

This tells us that if the array is already sored, then everything in the `maxLeft` and `minRight` will match.&#x20;
