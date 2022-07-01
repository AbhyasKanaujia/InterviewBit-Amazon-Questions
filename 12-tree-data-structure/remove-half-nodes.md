# Remove Half Nodes

{% embed url="https://www.interviewbit.com/problems/remove-half-nodes/" %}

Recursively return the single child if the node is a parent of a single child.

Update left and right pointer of each node recursively.

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
 
bool isHalf(TreeNode *root) {
    if(!root) return true;
    
    return ((bool)root->left + (bool)root->right) == 1;
}

TreeNode *getSingleChild(TreeNode *root) {
    if(!root) return root;
    
    return root->left ? root->left : root->right;
}

TreeNode* Solution::solve(TreeNode* A) {
    if(!A) return A;
    
    if(A->left)
        A->left = solve(A->left);
        
    if(A->right)
        A->right = solve(A->right);
    
    if(isHalf(A))
        return getSingleChild(A);
    else 
        return A;
}
```
