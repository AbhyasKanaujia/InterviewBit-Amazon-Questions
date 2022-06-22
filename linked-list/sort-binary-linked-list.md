# ⭐ Sort Binary Linked List

{% embed url="https://www.interviewbit.com/problems/sort-binary-linked-list/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::solve(ListNode* A) {
    ListNode *zeros = new ListNode(-1);
    ListNode *ones = new ListNode(-1);
    
    ListNode *zeroPtr = zeros;
    ListNode *onePtr = ones;
    
    ListNode *ptr = A;
    
    while(ptr) {
        if(ptr->val == 0) {
            zeroPtr->next = ptr;
            zeroPtr = zeroPtr->next;
        } else {
            onePtr->next = ptr;
            onePtr = onePtr->next;
        }
        ptr = ptr -> next;
    }
    
    onePtr->next = NULL;
    zeroPtr->next = ones->next;
    return zeros->next;
}


```
