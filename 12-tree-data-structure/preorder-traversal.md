# Preorder Traversal

{% embed url="https://www.interviewbit.com/problems/preorder-traversal/" %}

```cpp
vector<int> res;
void fillInorder(TreeNode *A) {
    if(!A) return;
    res.push_back(A->val);
    fillInorder(A->left);
    fillInorder(A->right);
}
vector<int> Solution::preorderTraversal(TreeNode* A) {
    res.clear();
    fillInorder(A);
    return res;
}
```
