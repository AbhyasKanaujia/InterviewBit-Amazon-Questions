# Grid Unique Paths

{% embed url="https://www.interviewbit.com/problems/grid-unique-paths/" %}

### Using DFS (very bad time complexity)

```cpp
int res = 0;

void getWays(int i, int j, int m, int n) {
    if(i == m && j == n) {
        res++;
        return;
    }

    // right
    if(m > i)
        getWays(i, j + 1, m, n);

    // down
    if(n > j)
        getWays(i + 1, j, m, n);
}

int Solution::uniquePaths(int A, int B) {
    getWays(0, 0, A, B);
    return res;
}

```

### Using Combination (Optimal)

```cpp
int nCr(int n, int r) {
    r = min(r, n - r);
    if(r == 0)
        return 1;

    int res = 1;
    for(int i = 0; i < r; i++) 
        res = res * (n - i) / (i + 1);

    return res;
}

int Solution::uniquePaths(int A, int B) {
    int m = A + B - 2;
    return nCr(m, A - 1);
}
```

For a grid of size $$4 \times 5$$.

The robot needs to move $$4$$ right and $$3$$ down.

The robot needs to make a total of $$4\times3 = 12$$ moves

So we need to make a string of size 12 that contains $$4$$ `R` s and $$3$$ `D`s

```
____________
Could contain RRRRDDD
```

This could be present in any combination.

Here we can place `R` and `D` fall in the remaining positions.&#x20;

So we need to choose $$4$$​ places out of $$12$$​.

This can be done in $$^{12}C_4$$​ ways.
