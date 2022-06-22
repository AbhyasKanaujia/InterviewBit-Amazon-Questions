# Palindrome List

{% embed url="https://www.interviewbit.com/problems/palindrome-list/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *reverse(ListNode *ll) {
    ListNode *prev = NULL;
    ListNode *current = ll;
    
    while(current) {
        ListNode *next = current -> next;
        
        current -> next = prev;
        
        prev = current;
        current = next;
    }
    
    return prev;
}

ListNode *getMid(ListNode *ll) {
    ListNode *fast = ll, *slow  = ll;

    while(fast && fast -> next && fast -> next -> next) {
        slow = slow -> next;
        fast = fast -> next -> next;
    }
    
    return slow;
}

int Solution::lPalin(ListNode* A) {
    ListNode *mid = getMid(A);
    
    // B is 2nd half
    ListNode *B = mid -> next;
    // next of end of 1st half points to NULL
    mid -> next = NULL;
    B = reverse(B);
    
    ListNode *ptr1 = A, *ptr2 = B;
    
    // match each element in A and B
    while(ptr1 && ptr2) {
        if(ptr1 -> val != ptr2 -> val)
            return false;
        ptr1 = ptr1 -> next;
        ptr2 = ptr2 -> next;
    }
    
    // if no mismatch then true
    return true;
}

```
