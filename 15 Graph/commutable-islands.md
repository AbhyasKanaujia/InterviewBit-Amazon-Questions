# Commutable Islands

{% embed url="https://www.interviewbit.com/problems/commutable-islands/" %}

```cpp
#include<bits/stdc++.h>
int getMinIndex(const vector<int> &cost, const vector<bool> &included) {
    int minIndex;
    int minCost = INT_MAX;
    for(int i = 0; i < cost.size(); i++)
        if(!included[i] && cost[i] < minCost) {
            minIndex = i;
            minCost = cost[i];
        }
        
    return minIndex;
}

int Solution::solve(int A, vector<vector<int> > &B) {
    vector<vector<vector<int>>> adj(A);
    
    for(vector<int> edge: B) {
        adj[edge[0] - 1].push_back({edge[1] - 1, edge[2]});
        adj[edge[1] - 1].push_back({edge[0] - 1, edge[2]});
    }
    
    vector<int> cost(A, INT_MAX);
    vector<bool> included(A);
    
    cost[0] = 0;
    
    for(int i = 1; i < A; i++) {
        int minIndex = getMinIndex(cost, included);
        included[minIndex] = true;
        
        for(vector<int> neighbour: adj[minIndex]) 
            if(!included[neighbour[0]] && neighbour[1] < cost[neighbour[0]])
                cost[neighbour[0]] = neighbour[1];
    }
    
    return accumulate(cost.begin(), cost.end(), 0);
}

```
