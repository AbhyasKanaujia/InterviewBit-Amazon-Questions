# 0 - 1 Knapsack Problem

{% embed url="https://practice.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1" %}

```cpp
class Solution
{
    private:
    int getMaxProfit(int capacity, int wt[], int val[], int itemCount, 
                        vector<vector<int>> &savedProfit) {
        if(capacity <= 0)
            return 0;
            
        if(itemCount <= 0)
            return 0;
            
        if(savedProfit[capacity][itemCount] != -1)
            return savedProfit[capacity][itemCount];
            
        if(capacity - wt[itemCount - 1] < 0)
            return savedProfit[capacity][itemCount] = 
                        getMaxProfit(capacity, wt, val, 
                                    itemCount - 1, savedProfit);
            
        return savedProfit[capacity][itemCount] = max(
                val[itemCount - 1] + getMaxProfit(capacity - wt[itemCount - 1], 
                                    wt, val, itemCount - 1, savedProfit),
                getMaxProfit(capacity, wt, val, itemCount - 1, savedProfit)
            );
    }
    public:
    //Function to return max value that can be put in knapsack of capacity W.
    int knapSack(int capacity, int wt[], int val[], int itemCount) 
    { 
        vector<vector<int>> savedProfit(capacity + 1, vector<int>(itemCount + 1, -1));
        
        return getMaxProfit(capacity, wt, val, itemCount, savedProfit);
    }
};
```
