# Merge Two Sorted Lists

{% embed url="https://www.interviewbit.com/problems/merge-two-sorted-lists/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::mergeTwoLists(ListNode* A, ListNode* B) {
    ListNode *dummy = new ListNode(0);
    ListNode *ptr = dummy;
    while(A || B) {
        if(!A) { // A exhausted. Push B.
            ptr -> next = B;
            B = B -> next;
        } else if (!B) { // B exhausted. Push A.
            ptr -> next = A;
            A = A -> next;
        } else { // Both Exists. Find Smaler
            if(A -> val < B -> val) { // A smaller. Push A.
                ptr -> next = A;
                A = A -> next;
            } else { // B smaller. Push B.
                ptr -> next = B;
                B = B -> next;
            }
        }
        
        ptr = ptr -> next; // point at the end of new list.
    }
    
    return dummy -> next;
}

```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
