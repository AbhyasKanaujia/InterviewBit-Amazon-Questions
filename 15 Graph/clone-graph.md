# Clone Graph

{% embed url="https://www.interviewbit.com/problems/clone-graph/" %}

## Using BFS

The main idea is to traverse each node using BFS and build its list of neighbours. The catch is to avoid rebuilding any node when it reappears as some other node's child while it has already been processed. If not avoided, this will result in an infinite loop.&#x20;

```cpp
/**
 * Definition for undirected graph.
 * struct UndirectedGraphNode {
 *     int label;
 *     vector<UndirectedGraphNode *> neighbors;
 *     UndirectedGraphNode(int x) : label(x) {};
 * };
 */
UndirectedGraphNode *Solution::cloneGraph(UndirectedGraphNode *node) {
    // if node is null then return
    if(!node) return nullptr;
    // Variaabl tot store the result. Initially stores the root's value.
    UndirectedGraphNode *g = new UndirectedGraphNode(node->label);
    // if same old node is repeated, we use the same corresponding new node
    // this can be used as a visited array too
    unordered_map<UndirectedGraphNode *, UndirectedGraphNode *> oldToNewMap;
    // map old root to new root
    oldToNewMap[node] = g;
    // queue to perfrorm BFS. This will store the olds nodes
    // I will construct new nodes from this
    queue<UndirectedGraphNode *> q;
    q.push(node);
    
    // untill all the elements have been copied
    while(!q.empty()) {
        // take the first node. This is going to be an old node.
        UndirectedGraphNode *frontNode = q.front();
        // remove it from the queue
        q.pop();
        
        // the frontNode has its corresponding new node created. 
        // we need to fill the new node's neighbors based on the old node
        // get all the neighbors of the old node
        for(UndirectedGraphNode *neighbor: frontNode->neighbors) {
            // check if a corresponding new node have already been created for this neighbor
            if(!oldToNewMap[neighbor]) {
                // if this is the first encounter with this neighbor, then first create it. 
                oldToNewMap[neighbor] = new UndirectedGraphNode(neighbor->label);
                // push this new neighbor into the queue for further duplication
                q.push(neighbor);
            }
            
            // either this neighbour preexisted or was just created in the previous if statement
            // in both cases push it into the list of neighbours for the corresponding new frontNode
            oldToNewMap[frontNode]->neighbors.push_back(oldToNewMap[neighbor]);
        }
        // all the neighbor for this frontNode have been pushed into the neighbors list.
        // newly created ones are also in the queue while preexisting ones are excluded        
    }
    // eventually there will be no new nodes to be pushed into the queue and the while loop will exit
    // `g` is the new root node and can be safely returned
    return g;
}
```

<details>

<summary>Without Comments</summary>

```cpp
UndirectedGraphNode *Solution::cloneGraph(UndirectedGraphNode *node) {
    if(!node) return nullptr;
    
    UndirectedGraphNode *g = new UndirectedGraphNode(node->label);
    unordered_map<UndirectedGraphNode *, UndirectedGraphNode *> oldToNewMap;
    oldToNewMap[node] = g;
    
    queue<UndirectedGraphNode *> q;
    q.push(node);
    
    while(!q.empty()) {
        UndirectedGraphNode *frontNode = q.front();
        q.pop();
        
        for(UndirectedGraphNode *neighbor: frontNode->neighbors) {
            if(!oldToNewMap[neighbor]) {
                oldToNewMap[neighbor] = new UndirectedGraphNode(neighbor->label);
                q.push(neighbor);
            }
            
            oldToNewMap[frontNode]->neighbors.push_back(oldToNewMap[neighbor]);
        }
    }
    
    return g;
}
```

</details>

Time Complexity: $$O(N + E)$$​

Space Complexity: $$O(N + E) + O(N) + O(N)$$​ for BFS, queue and `oldToNew` mapping
