# Vertical Order traversal of Binary Tree

{% embed url="https://www.interviewbit.com/problems/vertical-order-traversal-of-binary-tree/" %}

## Using map of level to vector of nodes

```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class NodeWithLevel {
  public: 
    TreeNode *node;
    int horizontalDistance;
    
    NodeWithLevel(TreeNode *node, int horizontalDistance) {
        this->node = node;
        this->horizontalDistance = horizontalDistance;
    }
};

vector<vector<int> > Solution::verticalOrderTraversal(TreeNode* A) {
    vector<vector<int>> res;
    
    if(!A) return res;
    
    map<int, vector<int>> distanceToNodes;
    queue<NodeWithLevel> q;
    q.push(NodeWithLevel(A, 0));
    
    while(!q.empty()) {
        NodeWithLevel frontNode = q.front();
        q.pop();
        
        distanceToNodes[frontNode.horizontalDistance].push_back(frontNode.node->val);
        if(frontNode.node->left)
            q.push(NodeWithLevel(frontNode.node->left, frontNode.horizontalDistance - 1));
        if(frontNode.node->right)
            q.push(NodeWithLevel(frontNode.node->right, frontNode.horizontalDistance + 1));
    }    
    
    for(auto group: distanceToNodes) 
        res.push_back(group.second);
        
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$
