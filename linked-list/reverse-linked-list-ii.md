# ⭐ Reverse Linked List II

{% embed url="https://www.interviewbit.com/problems/reverse-link-list-ii/" %}
Reverse a linked list from position m to n. **Do it in-place and in one-pass**.
{% endembed %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::reverseBetween(ListNode* A, int B, int C) {
    ListNode *dummy = new ListNode(-1);
    dummy -> next = A;
    
    ListNode *beforeReverse = dummy;
    
    for(int i = 0; i < B - 1; i++)
        beforeReverse = beforeReverse -> next;
        
    ListNode *tail =  beforeReverse -> next;
    for(int i = B; i < C; i++) {
        ListNode *pull = tail -> next;
        tail -> next = pull -> next;
        pull -> next = beforeReverse -> next;
        beforeReverse -> next = pull;
    }
    
    return dummy -> next;
}

```
