# Coin Change

{% embed url="https://practice.geeksforgeeks.org/problems/coin-change2448/1" %}

```cpp
public:
    long long int getWays(int S[], int m, int n,
                            vector<vector<long long int>> &savedWays) {
                      
        // using no coins, no way to make any amount.       
        if(m <= 0)
            return 0;
            
        // to make 0 amount, 1 way, use no coins.
        if(n == 0)
            return 1;
        // to make -ve amount, no way.
        if(n < 0)
            return 0;
            
        // if saved result then return.
        if(savedWays[m][n])
            return savedWays[m][n];
        
        // try making amount with every coin.
        long long int ways = 0;    
        for(int i = m - 1; i >= 0; i--)
            ways += getWays(S, i + 1, n - S[i], savedWays);
            
        return savedWays[m][n] = ways;
        
    }

    long long int count(int S[], int m, int n) {
        vector<vector<long long int>> savedWays(m + 1, 
                                        vector<long long int>(n + 1));
        return getWays(S, m, n, savedWays);
        // code here.
    }
};
```
