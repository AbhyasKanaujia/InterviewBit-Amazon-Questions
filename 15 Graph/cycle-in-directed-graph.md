# Cycle in Directed Graph

{% embed url="https://www.interviewbit.com/problems/cycle-in-directed-graph/" %}

```cpp
bool dfs(int node, vector<bool> &visited, vector<bool> &dfsVisited, vector<int> adj[]) {
    visited[node] = dfsVisited[node] = true;
    
    for(int neighbour : adj[node]) 
        if(!visited[neighbour]) {
            if(dfs(neighbour, visited, dfsVisited, adj))
                return true;
        } else if(dfsVisited[neighbour]) 
            return true;
            
    dfsVisited[node] = false;            
    return false;
}

int Solution::solve(int A, vector<vector<int> > &B) {
    vector<int> adj[A + 1];
    vector<bool> visited(A + 1);
    vector<bool> dfsVisited(A + 1);
    
    for(vector<int> edge: B) 
        adj[edge[0]].push_back(edge[1]);
        
    for(int node = 1; node <= A; node++)
        if(!visited[node])
            if(dfs(node, visited, dfsVisited, adj))
                return true;
                
                
    return false;
}
```
