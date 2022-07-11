# Possibility of finishing all courses given pre-requisites

{% embed url="https://www.interviewbit.com/problems/possibility-of-finishing-all-courses-given-prerequisites/" %}
Cycle Detection
{% endembed %}

## Using DFS

```cpp
bool hasCycle(int node, vector<bool> &visited, vector<bool> &dfsVisited, 
              vector<int> adjList[]) {
    visited[node] = dfsVisited[node] = true;
    
    for(int neighbour: adjList[node]) 
        if(!visited[neighbour]) {
            if(hasCycle(neighbour, visited, dfsVisited, adjList))
                return true;
        } else if(dfsVisited[neighbour])
            return true;
            
    dfsVisited[node] = false;
    return false;
}

int Solution::solve(int A, vector<int> &B, vector<int> &C) {
    // cycle detection in a directed graph
    
    // * Create adjList
    vector<int> adjList[A + 1];
    
    for(int i = 0; i < B.size(); i++) 
        adjList[B[i]].push_back(C[i]);
        
    
    // * Data Strucutres requred for cycle detection through DFS
    vector<bool> visited(A + 1);
    vector<bool> dfsVisited(A + 1);
    
    // * for each component, call dfs
    for(int node = 1; node <= A; node++)
        if(!visited[node])
            if(hasCycle(node, visited, dfsVisited, adjList))
                return false; // if cyclic then course can't be taken
                
    return true;
    // if acyclic then coures can be taken
}
```

## Using Topological Sort BFS&#x20;

```cpp
int Solution::solve(int A, vector<int> &B, vector<int> &C) {
    // * create a directed adjList
    vector<int> adjList[A + 1];
    for(int i = 0; i < B.size(); i++)
        adjList[B[i]].push_back(C[i]);
        
    // * create a topological sort
    
    // ? data strucutre for topological sort using bfs
    vector<int> indegree(A + 1);
    queue<int> q;
    vector<int> topologicalSort;
    
    // * fill indegree of all vertices
    for(int node = 1; node <= A; node++)
        for(int neighbour : adjList[node])
            indegree[neighbour]++;
            
    // * push into queue those vertices that have 0 indegree
    for(int node = 1; node <= A; node++) 
        if(indegree[node] == 0) 
            q.push(node);
            
    while(!q.empty()) {
        int frontNode = q.front();
        q.pop();
        
        topologicalSort.push_back(frontNode);
        
        for(int neighbour : adjList[frontNode]) {
            indegree[neighbour]--;
            if(indegree[neighbour] == 0)
                q.push(neighbour);
        }
    }
    
    return topologicalSort.size() == A;
}
```
