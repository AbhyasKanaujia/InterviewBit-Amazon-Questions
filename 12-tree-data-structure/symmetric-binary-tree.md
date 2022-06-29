# Symmetric Binary Tree

{% embed url="https://www.interviewbit.com/problems/symmetric-binary-tree/" %}

Inorder traversal should be a palindrome

number of elements should be odd

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
 
vector<int> inorder;

void getInorder(TreeNode *root) {
    if(!root) return;
    
    getInorder(root->left);
    inorder.push_back(root->val);
    getInorder(root->right);
}

bool isPalindrome() {
    int p1 = 0, p2 = inorder.size() - 1;
    while(p1 < p2)
        if(inorder[p1++] != inorder[p2--])
            return false;
            
    return true;
}

int Solution::isSymmetric(TreeNode* A) {
    inorder.clear();
    getInorder(A);
    if(inorder.size() & 1)
        return isPalindrome();
    else 
        return false;
}

```
