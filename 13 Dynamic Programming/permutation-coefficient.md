# Permutation Coefficient

{% embed url="https://www.codingninjas.com/codestudio/problems/permutationcoefficient_1214975" %}

```cpp
int nPr(int n, int r, vector<vector<int>> &savedResult) {
    if(r == 0)
        return 1;
    
    if(n == 0)
        return 0;
    
    if(savedResult[n][r])
        return savedResult[n][r];
    
    return savedResult[n][r] = 
        nPr(n - 1, r, savedResult) 
        + r * nPr(n - 1, r - 1, savedResult);
}

int P(int n, int r) {
    vector<vector<int>> savedResult(n + 1, vector<int>(r + 1));
    return nPr(n, r, savedResult);
}
```

```cpp
int P(int n, int r) {
    long long nPr[n + 1][r + 1];
    
    for(int i = 1; i <= r; i++)
        nPr[0][i] = 0;
    
    for(int i = 0; i <= n; i++)
        nPr[i][0] = 1;
    
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= r; j++)
            nPr[i][j] = (nPr[i - 1][j] + (j * nPr[i - 1][j - 1])) % 1000000007;
    
    return nPr[n][r];
}
```
