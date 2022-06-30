# Min Depth of Binary Tree

{% embed url="https://www.interviewbit.com/problems/min-depth-of-binary-tree/" %}

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
int Solution::minDepth(TreeNode* A) {
    // non existent tree has height 0
    if(!A) return 0;
    
    // if one of the children is non existent 
    // then use the result of existent children
    // as non existent will always be smaller(0) 
    // and will be ignored
    if(!A->left || !A->right)
        return max(minDepth(A->right), minDepth(A->left)) + 1;    
    
    return min(minDepth(A->left), minDepth(A->right)) + 1;
}

```
