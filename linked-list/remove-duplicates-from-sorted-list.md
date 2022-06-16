# Remove Duplicates from Sorted List

{% embed url="https://www.interviewbit.com/problems/remove-duplicates-from-sorted-list/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::deleteDuplicates(ListNode* A) {
    ListNode *ptr = A;
    
    while(ptr && ptr -> next) {
        while(ptr && ptr -> next && ptr -> val == ptr -> next -> val)
            ptr -> next = ptr -> next -> next;
        if(ptr)
            ptr = ptr -> next;
    }
    
    return A;
}

```
