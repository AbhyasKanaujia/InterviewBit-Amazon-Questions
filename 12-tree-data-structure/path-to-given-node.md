# Path to Given Node

{% embed url="https://www.interviewbit.com/problems/path-to-given-node/" %}

## Using Recursive Preorder Traversal

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

void getPath(TreeNode *root, int target, vector<int> &path) {
    if(!root) return;
    
    path.push_back(root->val);
    if(root->val == target) {
        res = path;
        return;
    }
    getPath(root->left, target, path);
    getPath(root->right, target, path);
    path.pop_back();
}

vector<int> Solution::solve(TreeNode* A, int B) {
    res.clear();
    vector<int> path;
    getPath(A, B, path);
    return res;
}

```
