# ⭐ Distribute Candy

{% embed url="https://www.interviewbit.com/problems/distribute-candy/" %}

```cpp
#include<bits/stdc++.h>
int Solution::candy(vector<int> &rating) {
    vector<int> candies(rating.size(), 1);
    
    for(int i = 1; i < rating.size(); i++) 
        if(rating[i - 1] < rating[i])
            candies[i] = max(candies[i - 1] + 1, candies[i]);
    
    for(int i = rating.size() - 2; i >= 0; i--)
        if(rating[i + 1] < rating[i])
            candies[i] = max(candies[i + 1] + 1, candies[i]);
            
    return accumulate(candies.begin(), candies.end(), 0);
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
