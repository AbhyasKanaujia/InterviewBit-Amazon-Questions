# Covered / Uncovered Nodes

{% embed url="https://www.interviewbit.com/problems/covered-uncovered-nodes/" %}

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
long Solution::coveredNodes(TreeNode* A) {
    queue<TreeNode *> q;
    q.push(A);
    long long outer = 0, inner = 0;
    
    while(!q.empty()) {
        long long size = q.size();
        for(int i = 1; i <= size; i++) {
            TreeNode *frontNode = q.front();
            q.pop();
            if(i == 1 || i == size) 
                outer += frontNode->val;
            else
                inner += frontNode->val;
            if(frontNode->left)
                q.push(frontNode->left);
            if(frontNode->right)
                q.push(frontNode->right);
        }
    }
    return abs(outer - inner);
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

<details>

<summary>Convincing but WRONG solution</summary>

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
int getTotal(TreeNode *root) {
	if(!root) 
		return 0;
	
	return root->val + getTotal(root->left) + getTotal(root->right);
}

map<TreeNode *, bool> visited;

int getLeft(TreeNode *root) {
	// ignore non existent and leaves
	if(!root || (!root->left && !root->right)) return 0;

	
	int sum = visited[root] ? 0 : root->val;
	visited[root] = true;

	if(root->left)
	return sum + getLeft(root->left);

	return sum + root->right->val + getLeft(root->right->left);
}

int getRight(TreeNode *root) {
	// ignore non existent and leaves
	if(!root || (!root->left && !root->right)) return 0;

	
	int sum = visited[root] ? 0 : root->val;
	visited[root] = true;

	if(root->right)
	return sum + getRight(root->right);

	return sum + root->left->val + getRight(root->left->right);
}


int getLeaf(TreeNode *root) {
    if(!root)
        return 0;
        
    if(!root->left && !root->right) 
        return root->val;
        
    return getLeaf(root->left) + getLeaf(root->right);
}


long Solution::coveredNodes(TreeNode* A) {
    int total = getTotal(A);
    int outer = getLeaf(A) + getLeft(A) + getRight(A) - A->val;
    return abs(total - 2 * outer);
}

```

</details>
