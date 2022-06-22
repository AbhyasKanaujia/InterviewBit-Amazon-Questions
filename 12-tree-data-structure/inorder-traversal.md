# ✅ Inorder Traversal

{% embed url="https://www.interviewbit.com/problems/inorder-traversal/" %}

{% tabs %}
{% tab title="C++" %}
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

void getRes(TreeNode *A) {
    if(!A)
        return;
        
    getRes(A->left);
    res.push_back(A->val);
    getRes(A->right);
}
vector<int> Solution::inorderTraversal(TreeNode* A) {
    res.clear();
    getRes(A);
    return res;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(2^h)$$​ where $$h$$​ is the height of the tree.

Space Complexity: $$O(2^h)$$​ for the result, where $$h$$​ is the heigh of the binary tree.
