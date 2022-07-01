# ⭐ Diagonal Traversal

{% embed url="https://www.interviewbit.com/problems/diagonal-traversal/" %}

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
 
map<int, vector<int>> levelToNodes;

void getDiagonalTraversal(TreeNode *root, int level) {
    if(!root) return;
    
    levelToNodes[level].push_back(root->val);
    getDiagonalTraversal(root->left, level + 1);
    getDiagonalTraversal(root->right, level);
}

vector<int> Solution::solve(TreeNode* A) {
    levelToNodes.clear();
    vector<int> res;
    
    int level = 0;
    getDiagonalTraversal(A, level);
    
    for(auto group: levelToNodes) 
        for(int x: group.second) 
            res.push_back(x);
    
    return res;
}
```

Time Complexity: $$O(n)$$

Space Complexity: $$O(n)$$

## Using Queue :star:

Store all the rights into ans. Store all the lefts into queue.

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
vector<int> Solution::solve(TreeNode* A) {
    queue<TreeNode *> q;
    q.push(A);
    vector<int> ans;
    
    while(!q.empty()) {
        TreeNode *frontNode = q.front();
        q.pop();
        
        TreeNode *ptr = frontNode;
        while(ptr) {
            if(ptr->left)
                q.push(ptr->left);
            ans.push_back(ptr->val);
            ptr = ptr->right;
        }
    }
    return ans;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
