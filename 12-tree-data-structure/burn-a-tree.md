# ⭐ Burn a Tree

{% embed url="https://www.interviewbit.com/problems/burn-a-tree/" %}

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
TreeNode *fireStart;

void getChildToParentMappingAndFireStart(TreeNode *root, int target) {
    if(!root) return;
    
    if(root->val == target) fireStart = root;
    
    if(root->left) {
        childToParent[root->left] = root;
        getChildToParentMappingAndFireStart(root->left, target);
    }
    
    if(root->right) {
        childToParent[root->right] = root;
        getChildToParentMappingAndFireStart(root->right, target);
    }
}

int Solution::solve(TreeNode* A, int B) {
    fireStart = nullptr;
    childToParent.clear();
    childToParent[A] = nullptr;
    map<TreeNode *, bool> burnt;
    int time = -1;
    
    getChildToParentMappingAndFireStart(A, B);
    
    queue<TreeNode *> q;
    q.push(fireStart);
    
    while(!q.empty()) {
        time++;
        int size = q.size();
        for(int i = 0; i < size; i++) {
            TreeNode *frontNode = q.front();
            q.pop();
            burnt[frontNode] = true;
            if(frontNode->left && !burnt[frontNode->left]) 
                q.push(frontNode->left);
            if(frontNode->right && !burnt[frontNode->right]) 
                q.push(frontNode->right);
            if(childToParent[frontNode] && !burnt[childToParent[frontNode]]) 
                q.push(childToParent[frontNode]);
        }
    }
    
    return time;    
}

```
