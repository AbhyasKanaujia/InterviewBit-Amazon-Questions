# Remove Nth Node from List End

{% embed url="https://www.interviewbit.com/problems/remove-nth-node-from-list-end/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
int getLength(ListNode *A) {
    int count = 0;
    
    while(A) {
        count++;
        A = A -> next;
    }
    
    return count;
}

ListNode *getNode(ListNode *A, int n) {
    while(--n) 
        A = A -> next;
    
    return A;
}

ListNode* Solution::removeNthFromEnd(ListNode* A, int B) {
    int n = getLength(A);
    
    // for single element remove it regardless of value of B
    if(n == 1)
        return NULL;
        
    // If B > n || B == n i.e. first element then return next to first
    if(B >= n)
        return A -> next;
        
    // normal obvious removal
    ListNode *ptr = getNode(A, n - B);
    ptr -> next = ptr -> next -> next;
    return A;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
