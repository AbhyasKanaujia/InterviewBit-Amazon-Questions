# ✅ Sorted Array To Balanced BST

{% embed url="https://www.interviewbit.com/problems/sorted-array-to-balanced-bst/" %}

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
 
TreeNode *getTree(const vector<int> &inorder, int low, int high) {
    if(low > high) 
        return nullptr;
        
    if(low == high) 
        return new TreeNode(inorder[low]);
        
        
    int mid = low + ((high - low) >> 1);
    
    TreeNode *root = new TreeNode(inorder[mid]);
    
    root->left = getTree(inorder, low, mid - 1);
    root->right = getTree(inorder, mid + 1, high);
    
    return root;
}
TreeNode* Solution::sortedArrayToBST(const vector<int> &A) {
    return getTree(A, 0, A.size() - 1);
}

```
