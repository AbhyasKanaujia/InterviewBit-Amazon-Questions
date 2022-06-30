# ZigZag Level Order Traversal BT

{% embed url="https://www.interviewbit.com/problems/zigzag-level-order-traversal-bt/" %}

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
vector<vector<int> > Solution::zigzagLevelOrder(TreeNode* A) {
    vector<vector<int>> res;
    
    queue<TreeNode *> q;
    q.push(A);
    bool leftToRight = true;
    
    while(!q.empty()) {
        int size = q.size();
        vector<int> row; 
        for(int i = 0; i < size; i++) {
            TreeNode *frontNode = q.front();
            q.pop();
            
            if(frontNode->left) 
                q.push(frontNode->left);
            if(frontNode->right)
                q.push(frontNode->right);
                
            row.push_back(frontNode->val);
        }
        
        if(!leftToRight)
            reverse(row.begin(), row.end());
        res.push_back(row);
        leftToRight = !leftToRight;  
    }
    
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​
