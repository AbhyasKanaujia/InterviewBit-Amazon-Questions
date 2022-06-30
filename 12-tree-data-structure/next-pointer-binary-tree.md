# Next Pointer Binary Tree

{% embed url="https://www.interviewbit.com/problems/next-pointer-binary-tree/" %}

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
void Solution::connect(TreeLinkNode* A) {
    if(!A || !A->left) 
        return;
        
    for(TreeLinkNode *parentStart = A; parentStart && parentStart->left; parentStart = parentStart->left) {
        TreeLinkNode *parent = parentStart;
        while(parent) {
            parent->left->next = parent->right;
            if(!parent->next) break;
            parent->right->next = parent->next->left;
            parent = parent->right;
        }
    }
}

```
