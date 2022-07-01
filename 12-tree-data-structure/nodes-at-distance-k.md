# Nodes at Distance K

{% embed url="https://interviewbit.com/problems/nodes-at-distance-k/" %}

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
 
map<TreeNode *, TreeNode *> childToParent;
TreeNode *targetNode;

void getChildToParentAndTargetNode(TreeNode *root, int target) {
    if(!root) return;
    
    if(root->val == target)
        targetNode = root;
        
    if(root->left) {
        childToParent[root->left] = root;
        getChildToParentAndTargetNode(root->left, target);
    }
    
    if(root->right) {
        childToParent[root->right] = root;
        getChildToParentAndTargetNode(root->right, target);
    }
}

vector<int> Solution::distanceK(TreeNode* A, int B, int C) {
    childToParent.clear();
    targetNode = nullptr;
    getChildToParentAndTargetNode(A, B);
    map<TreeNode *, bool> visited;
    queue<TreeNode *> q;
    
    q.push(targetNode);
    visited[targetNode] = true;
    int dist = 0;
    
    vector<int> res;
    while(!q.empty()) {
        dist++;
        int size = q.size();
        
        for(int i = 0; i < size; i++) {
            TreeNode *frontNode = q.front();
            q.pop();
            
            if(frontNode->left && !visited[frontNode->left]) {
                q.push(frontNode->left);
                visited[frontNode->left] = true;
                res.push_back(frontNode->left->val);
            }
            
            if(frontNode->right && !visited[frontNode->right]) {
                q.push(frontNode->right);
                visited[frontNode->right] = true;
                res.push_back(frontNode->right->val);
            }
            
            if(childToParent[frontNode] && !visited[childToParent[frontNode]]) {
                q.push(childToParent[frontNode]);
                visited[childToParent[frontNode]] = true;
                res.push_back(childToParent[frontNode]->val);
            }
        }
        if(dist == C) 
            return res;
        res.clear();
    }
    return res;
}

```
