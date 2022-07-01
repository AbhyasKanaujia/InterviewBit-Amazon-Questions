# ⭐ 2-Sum Binary Tree

{% embed url="https://www.interviewbit.com/problems/2sum-binary-tree/" %}

## Traverse the Tree and extract Inorder

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

int Solution::t2Sum(TreeNode* A, int B) {
    inorder.clear();
    getInorder(A);
    int p1 = 0, p2 = inorder.size() - 1;
    
    while(p1 < p2) {
        if(inorder[p1] + inorder[p2] < B)
            p1++;
        else if(inorder[p1] + inorder[p2] > B)
            p2--;
        else 
            return 1;
    }
    
    return 0;
}
```

## Using Sorted Linked List from BST

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
 
void getDoubly(TreeNode *current, TreeNode *&prev) {
    if(!current) return;
    
    getDoubly(current->left, prev);
    current->left = prev;
    prev->right = current;
    prev = current;
    getDoubly(current->right, prev);
}

TreeNode *getTail(TreeNode *root) {
    if(!root) return nullptr;
    
    while(root->right) 
        root = root->right;
        
    return root;
}

int Solution::t2Sum(TreeNode* A, int B) {
    TreeNode *head = new TreeNode(-1);
    TreeNode *prev = head;
    
    getDoubly(A, prev);
    TreeNode *p1 = head->right;
    TreeNode *p2 = getTail(p1);
    
    while(p1 != p2) {
        int sum = p1->val + p2->val;
        if(sum < B)
            p1 = p1->right;
        else if(sum > B)
            p2 = p2->left;
        else
            return 1;
    }
    
    return 0;    
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
