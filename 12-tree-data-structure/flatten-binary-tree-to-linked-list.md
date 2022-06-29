# Flatten Binary Tree to Linked List

{% embed url="https://www.interviewbit.com/problems/flatten-binary-tree-to-linked-list/" %}

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
TreeNode* Solution::flatten(TreeNode* A) {
    if(!A)
        return nullptr;
        
    TreeNode *leftSubTree = flatten(A->left);
    TreeNode *rightSubTree = flatten(A->right);
    
    TreeNode *ptr = A;
    ptr->right = nullptr;
    ptr->left = nullptr;
    if(leftSubTree)
        ptr->right = leftSubTree;
    
    while(ptr->right)
        ptr = ptr->right;
        
    if(rightSubTree)
        ptr->right = rightSubTree;
        
    return A;
}
```
