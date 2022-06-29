# ⭐ Populate Next Right Pointers Tree

{% embed url="https://www.interviewbit.com/problems/populate-next-right-pointers-tree/hints/" %}

## Using queue

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
void Solution::connect(TreeLinkNode* A) {
    queue<TreeLinkNode*> q;
    q.push(A);
    q.push(nullptr);
    while(!q.empty()) {
        TreeLinkNode *front = q.front();
        q.pop();
        if(front) {
            front->right = q.front();
            if(front->left)
                q.push(front->left);
            if(front->right)
                q.push(front->right);
        } else if(!q.empty())
            q.push(nullptr);
    }
}
```

## Without using queue

{% embed url="https://www.youtube.com/watch?v=3MRPQFUpoA0" %}

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
void Solution::connect(TreeLinkNode* A) {
    if(!A || !A->left) return;
    for(TreeLinkNode *levelStart = A; levelStart; levelStart = levelStart->left) {
        TreeLinkNode *nodeInLevel = levelStart;
        while(nodeInLevel) {
            nodeInLevel->left->next = nodeInLevel->right;
            if(!nodeInLevel->right) break;
            nodeInLevel->right->next = nodeInLevel->right->left;
        }
    }
}
```

