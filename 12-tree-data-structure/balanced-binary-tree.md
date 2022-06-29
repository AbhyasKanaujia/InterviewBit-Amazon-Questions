# Balanced Binary Tree

{% embed url="https://www.interviewbit.com/problems/balanced-binary-tree/" %}

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
class treeInfo {
  public:
    int height;
    bool isBalanced;
    
    treeInfo(int h, bool b) {
        height = h;
        isBalanced = b;
    }
};

treeInfo getInfo(TreeNode *A) {
    if(!A) 
        return treeInfo(0, true);
        
    treeInfo left = getInfo(A->left);
    treeInfo right = getInfo(A->right);
    
    bool isBalanced = abs(left.height - right.height) <= 1;
    return treeInfo(max(left.height, right.height) + 1, isBalanced && left.isBalanced && right.isBalanced);
}
int Solution::isBalanced(TreeNode* A) {
    return getInfo(A).isBalanced;
}

```
