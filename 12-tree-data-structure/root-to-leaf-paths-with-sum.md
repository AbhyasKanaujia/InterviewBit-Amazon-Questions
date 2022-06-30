# Root to Leaf Paths With Sum

{% embed url="https://www.interviewbit.com/problems/root-to-leaf-paths-with-sum/" %}

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
 
vector<vector<int>> res;

void getRes(TreeNode *root, int sum, vector<int> &path) {
    if(!root) return;
    
    if(!root->left && !root->right) {
        if(sum == root->val) {
            path.push_back(root->val);
            res.push_back(path);
            path.pop_back();
        }
        return;
    }
    
    path.push_back(root->val);
    int subSum = sum - root->val;
    
    getRes(root->left, subSum, path);
    getRes(root->right, subSum, path);
    
    path.pop_back();
}
vector<vector<int> > Solution::pathSum(TreeNode* A, int B) {
    res.clear();
    vector<int> path;
    getRes(A, B, path);
    return res;
}

```
