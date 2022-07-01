# Cousins in Binary Tree

{% embed url="https://www.interviewbit.com/problems/cousins-in-binary-tree/" %}

## Using level order traversal

Keep pushing all the children of current level to `res`.

If parent of target, then mark `found` flag as true, but don't push its children.

At the end of every level, there is a `nullptr`

When level ends, check if found.

If found then return `res`

Else reset `res` and add another null for further level searches.&#x20;

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
vector<int> Solution::solve(TreeNode* A, int B) {
    vector<int> res;
    if(!A || A->val == B) 
        return res;
        
    bool found = false;
    queue<TreeNode *> q;
    q.push(A);
    q.push(nullptr);
    
    while(!q.empty()) {
        TreeNode *frontNode = q.front();
        q.pop();
        
        if(frontNode) { // front node not null
            if(frontNode->left) // has left then push to queue
                q.push(frontNode->left);
            if(frontNode->right) // has right then push to queue
                q.push(frontNode->right);
                
            if((frontNode->left && frontNode->left->val == B)
                || (frontNode->right && frontNode->right->val == B)) // is a parent of target
                found = true; 
            else { // not a parent of target then push to res
                if(frontNode->left)
                    res.push_back(frontNode->left->val);
                if(frontNode->right)
                    res.push_back(frontNode->right->val);
            }
        } else { // front node in null
            if(found)
                return res;
            else {
                res.clear();
                if(!q.empty())
                    q.push(nullptr);
            }
        }
    }
    
    return res;
    
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(2^k)$$​ where k is the level where target exists.&#x20;

<details>

<summary>If 'no self and sibling' condition was not given</summary>

This solution returns a vector of all the nodes that are cousins of each, including the node in question and the node's sibling

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
vector<int> Solution::solve(TreeNode* A, int B) {
    queue<TreeNode *> q;
    q.push(A);
    q.push(nullptr);
    vector<int> cousins;
    bool found = false;
    
    while(!q.empty()) {
        TreeNode *frontNode = q.front();
        q.pop();
        
        if(frontNode) {
            cousins.push_back(frontNode->val);
            if(frontNode->val == B)
                found = true;
                
            if(frontNode->left)
                q.push(frontNode->left);
            if(frontNode->right) 
                q.push(frontNode->right);
        } else {
            if(found)
                return cousins;
            else {
                cousins.clear();
                if(!q.empty())
                    q.push(nullptr);
            }
        }
    }
    return cousins;
}
```

</details>
