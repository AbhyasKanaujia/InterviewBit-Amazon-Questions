# Path Sum

{% embed url="https://www.interviewbit.com/problems/path-sum/hints/" %}

## Using Recursion

1. Recursively add the left and right child until you reach the leaf.&#x20;
2. Once you reach the leaf, check if you have attained the sum
   1. If Yes then true
   2. else false

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
 

bool possible;

void checkPossibility(TreeNode *root, int sum) {
    if(!root) 
        return;
    
    if(!root->left && !root->right && root->val == sum) {
        possible = true;
        return;
    }
    
    checkPossibility(root->left, sum - root->val);
    if(!possible)
        checkPossibility(root->right, sum - root->val);
}

int Solution::hasPathSum(TreeNode* A, int B) {
    possible = false;
    checkPossibility(A, B);
    return possible;
}
```

More Elegant Solution

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
int Solution::hasPathSum(TreeNode* A, int B) {
    // Reached the end and required 0 more then we've achived B
    if(!A)
        return B == 0;
    
    // the sub tree should have B - val as current node contributes val.        
    int subSum = B - A->val;    
    // if either left or right fulfils then reutrn true
    return hasPathSum(A->left, subSum) || hasPathSum(A->right, subSum);
}

```
