# BST Iterator

{% embed url="https://www.interviewbit.com/problems/bst-iterator/" %}
Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.\
The first call to `next()` will return the smallest number in BST. Calling `next()` again will return the next smallest number in the BST, and so on.
{% endembed %}

## Using Recursive Inorder Traversal

Construct the inorder of the given tree and store it into a vector. Keep an index variable to point at the elements in this vector.&#x20;

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
vector<int>inorder;
int indx;
void getInorder(TreeNode *root) {
    if(!root) return;
    
    getInorder(root->left);
    inorder.push_back(root->val);
    getInorder(root->right);
}

BSTIterator::BSTIterator(TreeNode *root) {
    inorder.clear();
    getInorder(root);
    indx = 0;
}

/** @return whether we have a next smallest number */
bool BSTIterator::hasNext() {
    return indx < inorder.size();
}

/** @return the next smallest number */
int BSTIterator::next() {
    return inorder[indx++];
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$

### Using Stack

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
 
stack<TreeNode *> s;

BSTIterator::BSTIterator(TreeNode *root) {
    while(root) {
        s.push(root);
        root = root->left;
    }
}

/** @return whether we have a next smallest number */
bool BSTIterator::hasNext() {
    return !s.empty();
}

/** @return the next smallest number */
int BSTIterator::next() {
    int value = s.top()->val;
    TreeNode *ptr = s.top()->right;
    s.pop();
    while(ptr) {
        s.push(ptr);
        ptr = ptr->left;
    }
    return value;
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```

Time Complexity: $$O(h)$$​

Space Complexity: $$O(h)$$
