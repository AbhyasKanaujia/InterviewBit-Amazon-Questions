# Vertical Sum of a Binary Tree

{% embed url="https://www.interviewbit.com/problems/vertical-sum-of-a-binary-tree/" %}

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
map<int, int> distanceToSum;

void getResult(TreeNode *root, int dist) {
    if(!root) return;
    
    distanceToSum[dist] += root->val;
    
    if(root->left) 
        getResult(root->left, dist - 1);
    
    if(root->right) 
        getResult(root->right, dist + 1);
}

vector<int> Solution::verticalSum(TreeNode* A) {
    distanceToSum.clear();
    getResult(A, 0);
    vector<int> res;
    for(auto p: distanceToSum)
        res.push_back(p.second);
    return res;
}

```
