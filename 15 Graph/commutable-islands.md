# ⭐ Commutable Islands

{% embed url="https://www.interviewbit.com/problems/commutable-islands/" %}

## Using Prim's Brute Force

```cpp
#include <bits/stdc++.h>
int Solution::solve(int A, vector<vector<int> > &B) {
    // adj[u] = {(v1, w2) , (v2, w2)...}
    vector<pair<int, int>> adj[A + 1];
    for(vector<int> edgeAndWeight : B) {
        int u = edgeAndWeight[0];
        int v = edgeAndWeight[1];
        int w = edgeAndWeight[2];
        
        adj[u].push_back({v, w});
        adj[v].push_back({u, w});
    }
    
    vector<int> weight(A + 1, INT_MAX);
    weight[0] = weight[1] = 0;
    vector<bool> mst(A + 1);
    for(int bridgeCount = 1; bridgeCount <= A - 1; bridgeCount++
        int minWeight = INT_MAX;
        int node = -1;
        for(int i = 1; i <= A; i++)
            if(!mst[i] && weight[i] < minWeight) {
                minWeight = weight[i];
                node = i;
            }        
            
        mst[node] = true;
        
        for(pair<int, int> neighbourWithWeight: adj[node]) {
            int neighbour = neighbourWithWeight.first;
            int costToNeighbour = neighbourWithWeight.second;
            
            if(mst[neighbour] == false && costToNeighbour < weight[neighbour]) 
                weight[neighbour] = costToNeighbour;
        }
    }
    
    return accumulate(weight.begin(), weight.end(), 0);
}
```

Time Complexity:  $$O(n^2)$$​ for $$A - 1$$ edges and for finding minimum

Space Complexity: $$O(2V) + O(V) +O(V)$$ for adjacency list, weights, and MST.

## Using Optimized Prim's

```cpp
#include <bits/stdc++.h>
int Solution::solve(int A, vector<vector<int> > &B) {
    vector<pair<int, int>> adj[A + 1];
    vector<bool> mst(A + 1);
    
    for(vector<int> edge: B) {
        int u = edge[0];
        int v = edge[1];
        int w = edge[2];
        
        adj[u].push_back({v, w});
        adj[v].push_back({u, w});
    }
    
    vector<int> weight(A + 1, INT_MAX);
    weight[0] = weight[1] = 0;
    
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push({0, 1});
    
    for(int edgeCount = 1; edgeCount <= A - 1; edgeCount++) {
        int node = pq.top().second;
        pq.pop();
        
        mst[node] = true;
        
        for(pair<int, int> neighbourWithWeight: adj[node]) {
            int neighbour = neighbourWithWeight.first;
            int neighbourWeight = neighbourWithWeight.second;
            
            if(mst[neighbour] == false && neighbourWeight < weight[neighbour]) {
                weight[neighbour] = neighbourWeight;
                pq.push({weight[neighbour], neighbour});
            }
        }    
    }
    return accumulate(weight.begin(), weight.end(), 0);     
}
```

## Using Kruskal's Algorithm

```cpp
bool cmp(const vector<int> &edge1, const vector<int> &edge2) {
    return edge1[2] < edge2[2];
}

int findParent(int u, vector<int> &parent) {
    if(u == parent[u])
        return u;
        
    return parent[u] = findParent(parent[u], parent);
}

void performUnion(int u, int v, vector<int> &parent, vector<int> &rank) {
    u = findParent(u, parent);
    v = findParent(v, parent);
    
    if(rank[u] < rank[v]) 
        parent[u] = v;
    else if(rank[v] < rank[u])
        parent[v] = u;
    else {
        parent[v] = u;
        rank[u]++;
    }
}

int Solution::solve(int A, vector<vector<int> > &B) {
    sort(B.begin(), B.end(), cmp);
    
    // Initialize disjoint data structure
    vector<int> parent(A + 1);
    for(int i = 1; i < A; i++)
        parent[i] = i;
        
    vector<int> rank(A + 1);
    
    // take each edge in the order of smallest to largest weights
    int cost = 0;
    for(const vector<int> &closestNode: B) {
        // if disjoint then merge
        if(findParent(closestNode[0], parent) != findParent(closestNode[1], parent)) {
            cost += closestNode[2];
            performUnion(closestNode[0], closestNode[1], parent, rank);
        }
    }
    
    return cost;
}

```
