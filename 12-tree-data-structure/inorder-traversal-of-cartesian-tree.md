# ⭐ Inorder Traversal of Cartesian Tree

{% embed url="https://www.interviewbit.com/problems/inorder-traversal-of-cartesian-tree/" %}

{% embed url="https://www.youtube.com/watch?list=PLDzeHZWIZsToMrLX5-7qNyS6Db9VwTSvm&v=NKJnHewiGdc" %}

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
 
int getMaxIndex(const vector<int> &A, int low, int high) {
    int res = -1;
    int maxm = INT_MIN;
    
    for(int i = low; i <= high; i++) 
        if(A[i] > maxm) {
            maxm = A[i];
            res = i;
        }
        
    return res;
}
TreeNode *getTree(vector<int> &A, int low, int high) {
    if(low > high) 
        return NULL;
    int maxIndex = getMaxIndex(A, low, high);
    
    TreeNode *node = new TreeNode(A[maxIndex]);
    node->left = getTree(A, low, maxIndex - 1);
    node->right = getTree(A, maxIndex + 1, high);

    return node;
}
TreeNode* Solution::buildTree(vector<int> &A) {
    return getTree(A, 0, A.size() - 1);    
}
```

Accepted Solution
{% endtab %}
{% endtabs %}
