# ⭐ Gas Station

{% embed url="https://www.interviewbit.com/problems/gas-station/hints/" %}

```cpp
int Solution::canCompleteCircuit(const vector<int> &gas, const vector<int> &cost) {
    vector<int> contribution(gas.size());
    int totalGas = 0, totalCost = 0;
    for(int i = 0; i < gas.size(); i++) {
        totalGas += gas[i];
        totalCost += cost[i];
        
        contribution[i] = gas[i] - cost[i];
    }
    
    if(totalCost > totalGas)
        return -1;
        
    int validStartingPoint = 0;
    int total = 0;
    for(int i = 0; i < gas.size(); i++) {
        total += contribution[i];
        if(total < 0) {
            total = 0;
            validStartingPoint = i + 1;
        }
    }
    
    return validStartingPoint;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
