---
cover: >-
  https://images.unsplash.com/photo-1541580103-eb54f7a758be?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw0fHxncmlkfGVufDB8fHx8MTY1NTExNDc1MA&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ✅ Min Steps in Infinite Grid

{% embed url="https://www.interviewbit.com/problems/min-steps-in-infinite-grid/" %}

### Using Delta and recursion to actually reach point

```cpp
int getMinDist(int x1, int y1, int x2, int y2, int step = 0) {
    // reached
    if(x1 == x2 && y1 == y2)
        return step;

    int xDelta = x2 - x1;
    int yDelta = y2 - y1;

    // move leftward or rightward
    x1 += (xDelta > 0) ? 1 : (xDelta < 0) ? -1 : 0;
    // move upward or downward
    y1 += (yDelta > 0) ? 1 : (yDelta < 0) ? -1 : 0;

    // count as one step and find min distance from this point on
    return getMinDist(x1, y1, x2, y2, step + 1);
}

int Solution::coverPoints(vector<int> &A, vector<int> &B) {
    int dist = 0;
    
    for(int i = 0; i + 1 < A.size(); i++) 
        dist += getMinDist(A[i], B[i], A[i + 1], B[i + 1]);
    

    return dist;
}

```

### Properly Using Delta

```cpp
int getMinDist(int x1, int y1, int x2, int y2) {
    int xDelta = abs(x2 - x1);
    int yDelta = abs(y2 - y1);

    return max(xDelta, yDelta);
}

int Solution::coverPoints(vector<int> &A, vector<int> &B) {
    int dist = 0;
    
    for(int i = 0; i + 1 < A.size(); i++) 
        dist += getMinDist(A[i], B[i], A[i + 1], B[i + 1]);
    
    return dist;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​

If `xDelta` and `yDelta` both have some magnitude we move in the diagonal direction.&#x20;

If one of them is 0 we move only either vertically or horizontally.

Each move reduces the non zero `delta` by 1.

So the number of steps is exactly equal to one of the delta.&#x20;

And in fact, it is exactly equal to the larger delta.&#x20;

As the smaller delta becomes 0 sooner than the larger delta and remains there until the larger delta becomes 0 too.
