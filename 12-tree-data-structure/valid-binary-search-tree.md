# Valid Binary Search Tree

{% embed url="https://www.interviewbit.com/problems/valid-binary-search-tree/" %}

```cpp
bool checkValidity(TreeNode *A, long long min = INT_MIN, long long max = INT_MAX) {
    if(!A) return true;
    
    if(A->val <= min || A->val >= max)
        return false;
        
    return checkValidity(A->left, min, A->val) && checkValidity(A->right, A->val, max);
    
}

int Solution::isValidBST(TreeNode* A) {
    return checkValidity(A) ? 1 : 0;
}
```
