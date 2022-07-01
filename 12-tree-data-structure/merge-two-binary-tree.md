# Merge two Binary Tree

{% embed url="https://www.interviewbit.com/problems/merge-two-binary-tree/" %}

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
TreeNode* Solution::solve(TreeNode* A, TreeNode* B) {
    if(!A && !B) return nullptr;
    
    int val = A ? A->val : 0;
    val += B ? B->val : 0;
    
    TreeNode *node = new TreeNode(val);
    
    node->left = solve(A ? A->left : nullptr , B ? B->left : nullptr);
    node->right = solve(A ? A->right : nullptr , B ? B->right : nullptr);
    
    return node;
}

```
