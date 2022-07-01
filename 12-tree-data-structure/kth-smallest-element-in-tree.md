# Kth Smallest Element in Tree

{% embed url="https://www.interviewbit.com/problems/kth-smallest-element-in-tree/" %}

## Get all nodes and traverse

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
vector<int> nodes;

void getNodes(TreeNode *root) {
    if(!root) return;
    
    getNodes(root->left);
    nodes.push_back(root->val);
    getNodes(root->right);
}

int Solution::kthsmallest(TreeNode* A, int B) {
    nodes.clear();
    getNodes(A);
    sort(nodes.begin(), nodes.end());
    return nodes[B - 1];
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(n)$$​

## Creating an inorder array though traversal

{% hint style="success" %}
Inorder traversal of BST is always sorted
{% endhint %}

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
int Solution::kthsmallest(TreeNode* A, int B) {
    inorder.clear();
    getInorder(A);
    
    return inorder[B - 1];
}
```

Space Complexity: $$O(n)$$

Time Complexity: $$O(n)$$

## Using Recursive Traversal and a counter

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
int res;
void getNodes(TreeNode *root, int &counter, int B) {
    if(!root) return;
    
    getNodes(root->left, counter, B);
    
    counter++;
    if(counter == B) 
        res = root->val;
    
    getNodes(root->right, counter, B);
}

int Solution::kthsmallest(TreeNode* A, int B) {
    int counter = 0;
    getNodes(A, counter, B);
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​ for the stack

## Using Morris Traversal

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
int Solution::kthsmallest(TreeNode* A, int B) {
    int counter = 0;
    
    TreeNode *current, *prev;
    
    current = A;
    while(current) {
        if(!current->left) {
            if(++counter == B) 
                return current->val;
            current = current->right;
        } else {
            prev = current->left;
            while(prev->right && prev->right != current) 
                prev = prev->right;
                
            if(!prev->right) {
                prev->right = current;
                current = current->left;
            } else {
                prev->right = NULL;
                if(++counter == B)
                    return current->val;
                current = current->right;
            }
        }
    }
}
```

Time Complexity: $$O(k)$$​

Space Complexity: $$O(1)$$​
