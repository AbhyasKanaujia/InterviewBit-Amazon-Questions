# ⭐ Binary Tree From Inorder And Postorder

{% embed url="https://www.interviewbit.com/problems/binary-tree-from-inorder-and-postorder/" %}

{% embed url="https://www.youtube.com/watch?v=LgLRTaEMRVc" %}

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
map<int, int> inorderIndex;

TreeNode *getTree(vector<int> &inorder, int inorderLow, int inOrderHigh,
                    vector<int> &postorder, int postLow, int postHigh) {
    if(inorderLow > inOrderHigh || postLow > postHigh) 
        return nullptr;
        
    TreeNode *root = new TreeNode(postorder[postHigh]);
    
    int inorderRoot = inorderIndex[postorder[postHigh]];
    
    int leftCount = inorderRoot - inorderLow;
    
    root->left = getTree(inorder, inorderLow, inorderRoot - 1, postorder, postLow, postLow + leftCount - 1);
    root->right = getTree(inorder, inorderRoot + 1, inOrderHigh, postorder, postLow + leftCount, postHigh - 1);
    
    return root;
}

TreeNode* Solution::buildTree(vector<int> &A, vector<int> &B) {
    inorderIndex.clear();
    for(int i = 0; i < A.size(); i++)
        inorderIndex[A[i]] = i;
        
    int inorderLow = 0, inOrderHigh = A.size() - 1;
    int postLow = 0, postHigh = B.size() - 1;
    
    return getTree(A, inorderLow, inOrderHigh, B, postLow, postHigh);
}
```
