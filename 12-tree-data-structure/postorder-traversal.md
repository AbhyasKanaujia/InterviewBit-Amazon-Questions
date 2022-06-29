# Postorder Traversal

{% embed url="https://www.interviewbit.com/problems/postorder-traversal/" %}

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
 
vector<int> res;

void getPost(TreeNode *root) {
    if(!root) return;
    
    getPost(root->left);
    getPost(root->right);
    res.push_back(root->val);
}
vector<int> Solution::postorderTraversal(TreeNode* A) {
    res.clear();
    getPost(A);
    return res;
}

```
