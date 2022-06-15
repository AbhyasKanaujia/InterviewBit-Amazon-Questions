# Swap List Nodes in Pairs

{% embed url="https://www.interviewbit.com/problems/swap-list-nodes-in-pairs/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::swapPairs(ListNode* A) {
    ListNode* dummy = new ListNode(0);
    dummy -> next = A;
    
    ListNode* prev = dummy;    
    ListNode* current = prev -> next;;
    
    while(current != NULL && current -> next != NULL) {
        ListNode* next = current -> next;
        current -> next = next -> next;
        next -> next = current;
        prev -> next = next;
        prev = current;
        current = prev -> next;
    }
    
    return dummy -> next;
}
```
