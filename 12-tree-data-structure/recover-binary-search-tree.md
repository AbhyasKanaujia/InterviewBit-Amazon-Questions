# Recover Binary Search Tree

{% embed url="https://www.interviewbit.com/problems/recover-binary-search-tree/" %}

{% embed url="https://www.youtube.com/watch?v=ZWGW7FminDM" %}

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
TreeNode *first;
TreeNode *middle;
TreeNode *last;
TreeNode *prevNode;

void inorder(TreeNode *root) {
    if(root == NULL) return;
    
    inorder(root->left);
    
    if(prevNode != NULL && root->val < prevNode->val) {
        if(first == NULL) {
            first = prevNode;
            middle = root;
        } else 
            last = root;
    }
            
    prevNode = root;
    inorder(root->right);
}
vector<int> Solution::recoverTree(TreeNode* A) {
    first = middle = last = NULL;
    prevNode = new TreeNode(INT_MIN);
    inorder(A);  
    vector<int> res = {first->val};
    if(last)
        res.push_back(last->val);
    else
        res.push_back(middle->val);
    
    sort(res.begin(), res.end());
    return res;
}
```
{% endtab %}
{% endtabs %}
