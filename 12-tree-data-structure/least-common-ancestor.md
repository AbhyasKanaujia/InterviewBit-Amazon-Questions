# ⭐ Least Common Ancestor

{% embed url="https://www.interviewbit.com/problems/least-common-ancestor/hints/" %}

{% embed url="https://www.youtube.com/watch?v=_-QHfMDde90" %}

{% tabs %}
{% tab title="C++" %}
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
TreeNode *getAncestor(TreeNode *A, int B, int C) {
    if(!A || A->val == B || A->val == C)
        return A;
    
    TreeNode *left = getAncestor(A->left, B, C);
    TreeNode *right = getAncestor(A->right, B, C);
    
    if(left == NULL)   
        return right;
    else if(right == NULL)
        return left;
    else 
        return A;     
}
int Solution::lca(TreeNode* A, int B, int C) {
    TreeNode *res = getAncestor(A, B, C);
    if(res)
        return res->val;
    else 
        return -1;
}
```

Not Accepted
{% endtab %}
{% endtabs %}

### Provided Solution

{% tabs %}
{% tab title="C++" %}
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
int Solution::lca(TreeNode* A, int B, int C) {
    if(!A) return -1;
    
    if(A->val == B || A->val == C) return A->val;
    
    int left = lca(A->left, B, C);
    int right = lca(A->right, B, C);
    
    if(left != -1 & right != -1) return A->val;
    
    return (left != -1 ? left : right);
}
```

Not Accpeted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(\log n)$$​
